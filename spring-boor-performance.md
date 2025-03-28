# Spring Boor Performance

_Status: Published_
_Created: 2024-12-03 11:09:25_
_Tags: spring, java, database_

# Logging
- hibernate.show_sql (niet in prod!)
- hibernate.format_sql
- hibernate.use_sql_comments

params:
- org.hibernate.type.descriptor.sql  level trace

P6Spy

pom.xml
```xml
<dependency>
    <groupId>p6spy</groupId>
    <artifactId>p6spy</artifactId>
    <version>3.9.1</version> <!-- You can use the latest version -->
</dependency>
```
application.properties
```properties
spring.datasource.driver-class-name=com.p6spy.engine.spy.P6SpyDriver
spring.datasource.url=jdbc:p6spy:mysql://localhost:3306/your_database
spring.datasource.username=your_username
spring.datasource.password=your_password

databaseDialectDateFormat=yyyy-MM-dd'T'HH:mm:ss.SSSZ
customLogMessageFormat=%{currentTime}|%(executionTime)ms|%(category)|connection %(connectionId)|\n%(sqlSingleLine)

modulelist=com.p6spy.engine.outage.P6OutageFactory,com.p6spy.engine.logging.P6LogFactory
logfile=spy.log
logMessageFormat=com.p6spy.engine.spy.appender.SingleLineFormat
appender=com.p6spy.engine.spy.appender.Slf4JLogger
databaseDialectDateFormat=yyyy-MM-dd HH:mm:ss.SSS
```
	•	modulelist: Specifies which P6Spy modules to enable.
	•	logfile: Defines where the log file will be created.
	•	appender: Determines where logs should be sent, such as a file or SLF4J for logging through a standard logging framework.


```

```

Datasource-proxy
```java
@Bean
public DataSource dataSource() {
	SLF4JQueryLoggingListener loggingListener = new SLF4JQueryLoggingListener();
	loggingListener.setQueryLogEntryCreator(new InlineQueryLogEntryCreator());
	
	return ProxyDataSourceBuilder.create(actualDataSource())
		.name(DATA_SOURCE_PROXY_NAME)
		.listener(loggingListener)
		.build();
}
```

- can have own cutom statement execution listeners
## FetchSize

`statement.setFetchSize(fetchSize)`
10 Oracle
120 SQL
PostreSQL MySQL whole resultset in single roundtrip

JPA2.2 getResultStream
dan wel zetten voor PostgresQL en MySQL

## Streams

### MySQL streaming
#### One Record
`statement.setFetchSize(Integer.MIN_VALUE)`
#### Multiple Records
`statement.setFetchSize(fetchSize)`

#### Oracle
`spring.jpa.properties.hibernate.jdbc.fetch_size=50`

#### MySQL Postgres

```MySQL
@Query("""
    select p
    from Post p
    where date(p.createdOn) >= :sinceDate
""")
@QueryHints(
    @QueryHint(name = AvailableHints.HINT_FETCH_SIZE, value = "25")
)
Stream<Post> streamByCreatedOnSince(
    @Param("sinceDate") LocalDate sinceDate
);
```

## Pagination
Data grows per page

- FETCH FIRST N ROWS ONLY
- FETCH NEXT N ROWS ONLY
- OFFSET M ROWS
Oracle 12c SQL2012 PostgresQL 8.4

let op ORDER BY

Top-N
```SQL
SELECT title
FROM post
ORDER BY created_on DESC, id DESC
FETCH FIRST 5 ROWS ONLY
```

Next-N
```SQL
SELECT title
FROM post
ORDER BY created_on DESC, id DESC
OFFSET 5 ROWS
FETCH NEXT 5 ROWS ONLY
```

#### PostgreSQL MySQL TOP-N
```PostgreSQL
SELECT title
FROM post
ORDER BY created_on DESC, id DESC
LIMIT 5
```

#### PostgreSQL MySQL NEXT-N
```PostgreSQL
SELECT title
FROM post
ORDER BY created_on DESC, id DESC
LIMIT 5
OFFSET 5
```
NB:  OFFSET komt NA LIMIT!!!

### JPQL Querying -Pagination

```JPQL
Page<Post> findAllByTitle(
    @Param("titlePattern") String titlePattern,
    Pageable pageRequest
);

@Query("""
    select p
    from Post p
    where p.title like :titlePattern
""")
Page<Post> findAllByTitle(
    @Param("titlePattern") String titlePattern,
    Pageable pageRequest
);
```

#### JPQL QUERY Pagination Top-N
```Java
Page<Post> posts = postRepository.findAllByTitle(
    "High-Performance Java Persistence %",
    PageRequest.of(0, 25, Sort.by("createdOn"))
);
```

```SQL
SELECT p.id, p.created_on, p.title
FROM post p
WHERE p.title LIKE 'High-Performance Java Persistence %' ESCAPE ''
ORDER BY p.created_on ASC
OFFSET 0 ROWS
FETCH FIRST 25 ROWS ONLY
```

```java
@Query(value = """
    SELECT p.id, p.title, p.created_on
    FROM post p
    WHERE p.title ilike :titlePattern
    ORDER BY p.created_on
""",
nativeQuery = true)
Page<Post> findAllByTitleLike(
    @Param("titlePattern") String titlePattern,
    Pageable pageRequest
);
```
#### Top-N
```java
Page<Post> posts = postRepository.findAllByTitle(
    "High-Performance Java Persistence %",
    PageRequest.of(0, 25)
);
```

```sql
SELECT p.id, p.title, p.created_on
FROM post p
WHERE p.title ilike 'High-Performance Java Persistence %'
ORDER BY p.created_on
FETCH FIRST 25 ROWS ONLY
```

## Offset pagination index scanning performance

```sql
CREATE INDEX idx_post_created_on ON post (created_on DESC, id DESC);

SELECT id
FROM post
ORDER BY created_on DESC
LIMIT 50;
```

```plaintext
Limit  (cost=0.28..2.51 rows=50 width=16)
  (actual time=0.013..0.022 rows=50 loops=1)
  -> Index Scan using idx_post_created_on on post p
     (cost=0.28..223.28 rows=5000 width=16)
     (actual time=0.013..0.019 rows=50 loops=1)
Planning time: 0.113 ms
Execution time: 0.055 ms
```

#### 2e en latere scan
```sql
SELECT id
FROM post
ORDER BY created_on DESC
LIMIT 50
OFFSET 50;
```
```plaintext
Limit  (cost=2.51..4.74 rows=50 width=16)
  (actual time=0.032..0.044 rows=50 loops=1)
  -> Index Scan using idx_post_created_on on post p
     (cost=0.28..223.28 rows=5000 width=16)
     (actual time=0.022..0.040 rows=100 loops=1)
Planning time: 0.198 ms
Execution time: 0.071 ms
```
Nu 100rows!!! Op de laattste pagina wordt alles gescanned... 1.190ms.....
OFFSET doesnt seek/traverse

## Seek or  keyset pagination

```sql
SELECT id, created_on
FROM post
ORDER BY created_on DESC, id DESC
LIMIT 50
```
*created_on EN id* moeten ERIN

#### Next-N
```sql
SELECT id, created_on
FROM post
WHERE (created_on, id) < ('2024-10-02 21:00:00.0', 4951)
ORDER BY created_on DESC, id DESC
LIMIT 50;
```
	•	The row value expression (a, b) < (c, d) is PostgreSQL and MySQL.
	•	It’s equivalent to a < c | (a = c & b < d).
Nu wel max 50 results in set

## Spring Data JPA - WindowIterator
Oplossing!

```java
WindowIterator<PostComment> commentWindowIterator = WindowIterator.of(
    position -> postCommentRepository.findByPost(
        post,
        PageRequest.of(
            0, pageSize,
            Sort.by(
                Sort.Order.desc(PostComment_.CREATED_ON),
                Sort.Order.desc(PostComment_.ID)
            )
        ),
        position
    )
).startingAt(ScrollPosition.keyset());

commentWindowIterator.forEachRemaining(this::processPostComment);
```

#### met Blaze Persistance Top-N

```java
// Blaze Persistence – Keyset pagination
PagedList<Post> firstPage = cbf
    .create(entityManager, Post.class)
    .orderByAsc(Post_.CREATED_ON).orderByAsc(Post_.ID)
    .page(0, pageSize)
    .withKeysetExtraction(true)
    .getResultList();
```
```sql
SELECT p.id, p.created_on, p.title,
       (SELECT count(*) FROM post)
FROM post p
ORDER BY p.created_on, p.id
OFFSET 0
ROWS FETCH FIRST 25 ROWS ONLY;
```

Next N
```java
// Blaze Persistence – Keyset pagination
PagedList<Post> nextPage = cbf
    .create(entityManager, Post.class)
    .orderByAsc(Post_.CREATED_ON).orderByAsc(Post_.ID)
    .page(postPage.getKeysetPage(),
          postPage.getPage() * postPage.getMaxResults(),
          postPage.getMaxResults())
    .getResultList();
```
```sql
SELECT p.id, p.created_on, p.title,
       (SELECT count(*) FROM post)
FROM post p
WHERE ('2024-09-09 12:10:00.0', 10) < (p.created_on, p.id)
ORDER BY p.created_on, p.id
OFFSET 0
ROWS FETCH FIRST 25 ROWS ONLY;
```

## Projections

## Fetching too many columns

### Instead of fetching all columns:
```sql
SELECT *  
FROM post_comment pc  
LEFT JOIN post p ON p.id = pc.post_id  
LEFT JOIN post_details pd ON p.id = pd.id  


```
### Fetch a custom SQL projection:
```

SELECT pc.id, pc.review  
FROM post_comment pc  
LEFT JOIN post p ON p.id = pc.post_id  
LEFT JOIN post_details pd ON p.id = pd.id  
```

(Joins zijn niet nodig... => dus tweede is dan sneller)

## Tuple projection
not type save

• The JPA Tuple wraps the default Object[] projection and
allows you to retrieve the column values via their aliases.

```java
List<Tuple> commentTuples = postRepository.findAllCommentTuplesByPostTitle(titleToken);
Tuple commentTuple = commentTuples.get(0);

long id = commentTuple.get("id", Number.class).longValue();
String title = commentTuple.get("title", String.class);
```
## Interface-based projection
• If you want a type-safe projection, Spring Data JPA provides
the option of wrapping the result in a Proxy based on a given
interface.

The Interface-based projection can be used like this:
```java
@Query("""
select
p.id as id,
p.title as title,
c.review as review
from PostComment c
join c.post p
where p.title like :postTitle
order by c.id
""")
List<PostCommentSummary> findAllCommentSummariesByPostTitle(
@Param("postTitle") String postTitle
);

// nu type safe!	   
Long id = commentSummary.getId();
String title = commentSummary.getTitle();
```

Met ingebakken (!) DTOs en Records
## DTOs

```java
properties.put(
    "hibernate.integrator_provider",  // Hibernate property for custom integrator
    (IntegratorProvider) () -> Collections.singletonList( // Lambda to provide integrator
        new ClassImportIntegrator( // Hypersistence Utils integrator
            List.of( // List of classes to register
                PostCommentDTO.class,  // First DTO class
                PostCommentRecord.class // Second DTO class
            )
        )
    )
);

String jpql = "SELECT new PostCommentDTO(pc.id, pc.comment) FROM PostComment pc WHERE pc.post.id = :postId";


```

## Records

```java
public record PostCommentDTO(Long id, String comment) {}
public record PostCommentRecord(Long id, String content) {}

properties.put(
    "hibernate.integrator_provider",
    (IntegratorProvider) () -> Collections.singletonList(
        new ClassImportIntegrator(
            List.of(
                PostCommentDTO.class,   // Register the record as a DTO
                PostCommentRecord.class // Register additional records as needed
            )
        )
    )
);

@Query(
    value = "SELECT pc.id, pc.comment FROM post_comment pc WHERE pc.post_id = :postId",
    nativeQuery = true
)
List<PostCommentDTO> findCommentsByPostId(@Param("postId") Long postId);

Long id = commentRecord.id();
String title = commentRecord.title();
```

## TupleTransformer and ResultListTransformer
The SQL projection can contain data from multiple tables, like
the post and post_comment, which form a one-to-many table
relationship.

```sql
SELECT p.id AS p_id,
p.title AS p_title,
pc.id AS pc_id,
pc.review AS pc_review
FROM post p
JOIN post_comment pc ON p.id = pc.post_id
ORDER BY pc.id
```

komt uit:

| p_id | p_title                           | pc_id | pc_review                             |
| ---- | --------------------------------- | ----- | ------------------------------------- |
| 1    | High-Performance Java Persistence | 1     | Best book on JPA and Hibernate!       |
| 1    | High-Performance Java Persistence | 2     | A must-read for every Java developer! |
| 2    | Hypersistence Optimizer           | 3     | It's like pair programming with Vlad! |


