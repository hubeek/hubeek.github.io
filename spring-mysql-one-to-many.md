# Spring Mysql One to Many....

_Status: Published_
_Created: 2020-12-07 12:24:53_
_Tags: java, spring, mysql, maven, xml, onetomany_

pom.xml  
- lombok  
- spring-boot-starter-data-jpa  
- mysql-connector-java  


application.properties  
```
# MySQL connection properties
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.username=username
spring.datasource.password=password
spring.datasource.url=jdbc:mysql://localhost:3306/testspring

# Log JPA queries
# Comment this in production
spring.jpa.show-sql=true

# Drop and create new tables (create, create-drop, validate, update)
# Only for testing purpose - comment this in production
spring.jpa.hibernate.ddl-auto=create-drop

# Hibernate SQL dialect
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5InnoDBDialect
```
ResApplication.java
```
public class RestApplication {

	public static void main(String[] args) {
		SpringApplication.run(RestApplication.class, args);
	}

	@Bean
	public CommandLineRunner mappingDemo(BookRepository bookRepository,
										 PageRepository pageRepository) {
		return args -> {

			// create a new book
			Book book = new Book("Java 101", "John Doe", "123456");

			// save the book
			bookRepository.save(book);
			pageRepository.save(new Page(65, "Java 8 contents", "Java 8", book));
			pageRepository.save(new Page(95, "Concurrency contents", "Concurrency", book));
		};
	}
}
```
Book.java
```

@Entity
@Table(name = "books")
@Getter
@Setter
public class Book implements Serializable {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;
    private String author;
    @Column(unique = true)
    private String isbn;

    ```**```@JsonManagedReference```**```
    @OneToMany(mappedBy = "book", fetch = FetchType.LAZY,
            cascade = CascadeType.ALL)
    private List<Page> pages = new ArrayList<Page>();

    public Book() {
    }

    public Book(String title, String author, String isbn) {
        this.title = title;
        this.author = author;
        this.isbn = isbn;
    }

    // getters and setters, equals(), toString() .... (omitted for brevity)

    @Override
    public String toString() {
        return "Book{" +
                "id=" + id +
                ", title='" + title + '\'' +
                ", author='" + author + '\'' +
                ", isbn='" + isbn + '\'' +
                ", number of pages=" + pages.size() +
                '}';
    }
}
```
Pages.java
```

@Entity
@Table(name = "pages")
@Setter
@Getter
public class Page implements Serializable {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private int number;
    private String content;
    private String chapter;

    @JsonBackReference
    @ManyToOne(fetch = FetchType.LAZY, optional = false)
    @JoinColumn(name = "book_id", nullable = false)
    private Book book;

    public Page() {
    }

    public Page(int number, String content, String chapter, Book book) {
        this.number = number;
        this.content = content;
        this.chapter = chapter;
        this.book = book;
    }

    // getters and setters, equals(), toString() .... (omitted for brevity)

    @Override
    public String toString() {
        return "Page{" +
                "id=" + id +
                ", number=" + number +
                ", content='" + content + '\'' +
                ", chapter='" + chapter + '\'' +
                ", book=" + book.toString() +
                '}';
    }
}
```
BookRepository.java
```
public interface BookRepository extends CrudRepository<Book, Long> {

    Book findByIsbn(String isbn);
}

```
PageRepository.java
```
public interface PageRepository extends CrudRepository<Page, Long> {

    List<Page> findByBook(Book book, Sort sort);
}

```
BooksController.java
```

@RestController
@RequestMapping(value = "/books", produces = MediaType.APPLICATION_JSON_VALUE)
public class BooksController {

    private final BookRepository bookRepository;
    private final PageRepository pageRepository;
    public BooksController(BookRepository bookRepository, PageRepository pageRepository) {
        this.bookRepository = bookRepository;
        this.pageRepository = pageRepository;
    }

    @GetMapping(value = "/pages", produces = MediaType.APPLICATION_JSON_VALUE)
    @ResponseStatus(HttpStatus.OK)
    public List<Page> pages(){
        List<Page> result = (List<Page>) pageRepository.findAll();
        System.out.println(result);
        System.out.println(result.get(0));
        return result;
    }
    @GetMapping("/")
    public List<Book> books(){
        return (List<Book>)bookRepository.findAll();
    }
}
```
http://localhost:8080/books/
```
[
{
"id": 1,
"title": "Java 101",
"author": "John Doe",
"isbn": "123456",
"pages": [
{
"id": 1,
"number": 1,
"content": "Introduction contents",
"chapter": "Introduction"
},
{
"id": 2,
"number": 65,
"content": "Java 8 contents",
"chapter": "Java 8"
},
{
"id": 3,
"number": 95,
"content": "Concurrency contents",
"chapter": "Concurrency"
}
]
}
]
```

http://localhost:8080/books/pages
```
[
{
"id": 1,
"number": 1,
"content": "Introduction contents",
"chapter": "Introduction"
},
{
"id": 2,
"number": 65,
"content": "Java 8 contents",
"chapter": "Java 8"
},
{
"id": 3,
"number": 95,
"content": "Concurrency contents",
"chapter": "Concurrency"
}
]
```

