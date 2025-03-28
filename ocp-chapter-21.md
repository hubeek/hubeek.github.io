# OCP Chapter 21

_Status: Published_
_Created: 2024-08-21 15:36:27_
_Tags: ocp, java_

# JDBC

Java Database Connectivity Language (JDBC): Accesses data as rows and columns.  

Java Persistence API (JPA): Accesses data through Java objects using a concept called object‐relational mapping (ORM).  

A relational database is accessed through Structured Query Language (SQL). SQL is a programming language used to interact with database records. JDBC works by sending a SQL command to the database and then processing the response.  
SQL keywords are case insensitive.  

In addition to relational databases, there is another type of database called a NoSQL database. This is for databases that store their data in a format other than tables, such as key/value, document stores, and graph‐based databases. NoSQL is out of scope for the exam as well.  

interfaces in the JDK:
- Driver: Establishes a connection to the database
- Connection: Sends commands to a database
- PreparedStatement: Executes a SQL query
- CallableStatement: Executes commands stored in the database
- ResultSet: Reads results of a query

```
public class MyFirstDatabaseConnection {
   public static void main(String[] args) throws SQLException
   {
    String url = "jdbc:derby:zoo";
    try (Connection conn = DriverManager.getConnection(url);
        PreparedStatement ps = conn.prepareStatement( "SELECT name FROM animal");
        ResultSet rs = ps.executeQuery()) {
        while (rs.next())
        System.out.println(rs.getString(1));
    }
   }
}

```



## GETTING A DATABASE CONNECTION
There are two main ways to get a Connection: **DriverManager** or **DataSource**. DriverManager is the one covered on the exam. Do not use a DriverManager in code someone is paying you to write. A DataSource has more features than DriverManager. For example, it can pool connections or store the database connection information outside the application.

```
Connection conn = DriverManager.getConnection("jdbc:derby:zoo");
System.out.println(conn);
```
It does not actually execute the query yet!  




## JDBC URL
Unlike web URLs, a JDBC URL has a variety of formats. They have three parts in common, as shown in Figure 21.3. The first piece is always the same. It is the protocol jdbc. The second part is the subprotocol, which is the name of the database such as derby, mysql, or postgres. The third part is the subname, which is a database‐specific format. Colons ( :) separate the three parts.

Notice the three parts. It starts with jdbc and then comes the subprotocol derby, and it ends with the subname, which is the database name. The location is not required, because Derby is an in‐memory database.
```
jdbc:derby:zoo // The location is not required, because Derby is an in‐memory database.


jdbc:postgresql://localhost/zoo
jdbc:oracle:thin:@123.123.123.123:1521:zoo
jdbc:mysql://localhost:3306
jdbc:mysql://localhost:3306/zoo?profileSQL=true
```


## Statement, CallableStatement, PreparedStatement


<pre>
            ┌───────────────────┐
            │     Statement     │
            └─────────▲─────────┘
          ┌───────────┴────────────┐
          │                        │
          │                        │
┌───────────────────┐    ┌───────────────────┐
│ PreparedStatement │    │ CallableStatement │
└───────────────────┘    └───────────────────┘


</pre>



While it is possible to run SQL directly with Statement, you shouldn't. PreparedStatement is far superior for the following reasons:
- **Performance**: In most programs, you run similar queries multiple times. A PreparedStatement figures out a plan to run the SQL well and remembers it.
- **Security**: As you will see in Chapter 22, “Security,” you are protected against an attack called SQL injection when using a PreparedStatement correctly
- **Readability**: It's nice not to have to deal with string concatenation in building a query string with lots of parameters.
- **Future use**: Even if your query is being run only once or doesn't have any parameters, you should still use a PreparedStatement. That way future editors of the code won't add a variable and have to remember to change to PreparedStatement then.

Using the Statement interface is also no longer in scope for the JDBC exam, so we do not cover it in this book.


## Prepared Statement

Passing a SQL statement when creating the object is mandatory.  
```
try (var ps = conn.prepareStatement()) { // DOES NOT COMPILE }
```
correct:
```
try (
    PreparedStatement ps = conn.prepareStatement( "SELECT * FROM exhibits")) {
        // work with ps
}
```

### Modifying Data with executeUpdate()

```
10: var insertSql = "INSERT INTO exhibits VALUES(10, 'Deer',
3)";
11: var updateSql = "UPDATE exhibits SET name = '' " +
12:    "WHERE name = 'None'";
13: var deleteSql = "DELETE FROM exhibits WHERE id = 10"; 14:
15: try (var ps = conn.prepareStatement(insertSql)) {
16: int result = ps.executeUpdate();
17:    System.out.println(result); // 1
18: }
19:
20: try (var ps = conn.prepareStatement(updateSql)) {
21: int result = ps.executeUpdate();
22:    System.out.println(result); // 0
23: }
24:
25: try (var ps = conn.prepareStatement(deleteSql)) {
26: int result = ps.executeUpdate();
27:    System.out.println(result); // 1
28: }
```

### Reading Data with executeQuery()
```
30: var sql = "SELECT * FROM exhibits";
31: try (var ps = conn.prepareStatement(sql); 32: ResultSet rs = ps.executeQuery() ) { 33:
34: // work with rs
35: }
```



### Processing Data with execute()
```
boolean isResultSet = ps.execute();
if (isResultSet) {
    try (ResultSet rs = ps.getResultSet()) {
        System.out.println("ran a query");
    }
} else {
    int result = ps.getUpdateCount();
    System.out.println("ran an update");
}
```



## PreparedStatment Methods
|Method|DELETE| INSERT |SELECT| UPDATE|Return Type| What is returned for SELECT | What is returned for DELETE/INSERT/UPDATE|
|-|-|-|-|-|-|-|-|
|ps.execute()|Yes|Yes|Yes|Yes|boolean |true|false|
|ps.executeQuery()|No|No|Yes|No|ResultSet|The rows and columns returned|n/a|
|ps.executeUpdate()|Yes|Yes|No|Yes|int|n/a|Number of rows added/changed/removed|

## WORKING WITH PARAMETERS
**let op**: conn.prepareStatment(sql) VS PreparedStatement ps = conn.prepareStatement(sql)  


```
String sql = "INSERT INTO names VALUES(?, ?, ?)";


public static void register(Connection conn, int key,int type, String name) throws SQLException {

    String sql = "INSERT INTO names VALUES(?, ?, ?)";
    try (PreparedStatement ps = conn.prepareStatement(sql)) {
        ps.setInt(1, key);
        ps.setString(3, name);
        ps.setInt(2, type);
        ps.executeUpdate(); // GEEN SQL meesturen!!!
    }
}
```
**Remember that JDBC starts counting columns with 1 rather than 0. A common exam (and interview) question tests that you know this!**  


When not having all parameters defined: The code compiles, and you get a SQLException. The message may vary based on your database driver.  

## PreparedStatments Methods
- setBoolean
- setDouble
- setInt
- setLong
- setObject (Any type)
- setString

### COMPILE VS. RUNTIME ERROR WHEN EXECUTING
```
ps.setObject(1, key);
ps.setObject(2, type);
ps.setObject(3, name);
ps.executeUpdate(sql);  // INCORRECT
```

The problem is that the last line passes a SQL statement. With a PreparedStatement, we pass the SQL in when creating the object.
More interesting is that this does not result in a compiler error. Remember that PreparedStatement extends Statement. The Statement interface does accept a SQL statement at the time of execution, so the code compiles. Running this code gives SQLException. The text varies by database.



### UPDATING MULTIPLE TIMES

```
var sql = "INSERT INTO names VALUES(?, ?, ?)";
try (var ps = conn.prepareStatement(sql)) {
   ps.setInt(1, 20);
   ps.setInt(2, 1);
   ps.setString(3, "Ester");
   ps.executeUpdate();

   ps.setInt(1, 21);
   ps.setString(3, "Elias");
   ps.executeUpdate();
}// WORKS!!
```

### BATCHING STATEMENTS
JDBC supports batching so you can run multiple statements in fewer trips to the database. 
For example, if you need to insert 1,000 records into the database, then inserting them as a single network call (as opposed to 1,000 network calls) is usually a lot faster.
You don't need to know the addBatch() and executeBatch() methods for the exam, but they are useful in practice.

```
   public static void register(Connection conn, int firstKey, int type, String... names) throws SQLException {
      var sql = "INSERT INTO names VALUES(?, ?, ?)";
      var nextIndex = firstKey;
      try (var ps = conn.prepareStatement(sql)) {
         ps.setInt(2, type);
        for(var name: names) {
            ps.setInt(1, nextIndex);
            ps.setString(3, name);
            ps.addBatch();
            nextIndex++;
        }
        int[] result = ps.executeBatch();
        System.out.println(Arrays.toString(result));
      }
}

register(conn, 100, 1, "Elias", "Ester");
```


## Getting Data from a ResultSet

begin met rs.next()  

-> 0 leeg  
   * row1
   * row2

daarom:
 `while(rs.next()`

```
String sql = "SELECT id, name FROM exhibits";
Map<Integer, String> idToNameMap = new HashMap<>();

try (var ps = conn.prepareStatement(sql);
    ResultSet rs = ps.executeQuery()) {
    while (rs.next()) {
        int id = rs.getInt("id");
        String name = rs.getString("name");
        idToNameMap.put(id, name);
    }
    System.out.println(idToNameMap);

}
// results: {1=African Elephant, 2=Zebra}
```
kan ook met index column. LET OP begint met 1!!!
```
    int id = rs.getInt(1);
    String name = rs.getString(2);
```
Attempting to access a column name or index that does not exist throws a SQLException, as does getting data from a ResultSet when it isn't pointing at a valid row.
```
var sql = "SELECT * FROM exhibits where name='Not in table'";
try (var ps = conn.prepareStatement(sql);
   var rs = ps.executeQuery()) {
   rs.next();
   rs.getInt(1); // SQLException
}
```

```
// fout: staat rs.next() staaat nog op 0
var sql = "SELECT count(*) FROM exhibits";
try (var ps = conn.prepareStatement(sql);
   var rs = ps.executeQuery()) {
   rs.getInt(1); // SQLException
}
// fout column 0 bestaat NIET
var sql = "SELECT count(*) FROM exhibits";
try (var ps = conn.prepareStatement(sql);
   var rs = ps.executeQuery()) {
   if (rs.next())
      rs.getInt(0); // SQLException
}

var sql = "SELECT name FROM exhibits";
try (var ps = conn.prepareStatement(sql);
   var rs = ps.executeQuery()) {
   if (rs.next())
   rs.getInt("badColumn"); // SQLException
}
```


To sum up this section, it is important to remember the following: 
- Always use an if statement or while loop when calling rs.next().
- Column indexes begin with 1.



## ResultSet Return from getObject

```
16: var sql = "SELECT id, name FROM exhibits";
17: try (var ps = conn.prepareStatement(sql);
18:    var rs = ps.executeQuery()) {
19:
20:    while (rs.next()) {
21: Object idField = rs.getObject("id");
22: Object nameField = rs.getObject("name");
23:       if (idField instanceof Integer) {
24:          int id = (Integer) idField;
25:          System.out.println(id);
26: }
27:       if (nameField instanceof String) {
28:          String name = (String) nameField;

```

### USING BIND VARIABLES
Wanneer er vars gezet moeten worden en uitgepakt dan nesten met try.

```
30: var sql = "SELECT id FROM exhibits WHERE name = ?";
31:
32: try (var ps = conn.prepareStatement(sql)) {
        ps.setString(1, "Zebra");
        try (var rs = ps.executeQuery()) {
           while (rs.next()) {
              int id = rs.getInt("id");
              System.out.println(id);
           }
        }
41: }

```


## Calling a CallableStatement

Sometimes you want your SQL to be directly in the database instead of packaged with your Java code. This is particularly useful when you have many queries and they are complex. A stored procedure is code that is
compiled in advance and stored in the database. Stored procedures are commonly written in a database‐specific variant of SQL, which varies among database software providers.

### CALLING A PROCEDURE WITHOUT PARAMETERS
A stored procedure is called by putting the word call and the procedure name in braces ( {}).
```
12: String sql = "{call read_e_names()}";
13: try (CallableStatement cs = conn.prepareCall(sql);
14: ResultSet rs = cs.executeQuery()) {
15:
16:    while (rs.next()) {
17:       System.out.println(rs.getString(3));
18: }
19: }
```
### PASSING AN IN PARAMETER
We have to pass a ? to show we have a parameter. This should be familiar from bind variables with a PreparedStatement.
```
25: var sql = "{call read_names_by_letter(?)}"; 26: try (var cs = conn.prepareCall(sql)) {
        cs.setString("prefix", "Z");
        try (var rs = cs.executeQuery()) {
           while (rs.next()) {
              System.out.println(rs.getString(3));
           }
        }
}

// => cs.setString(1, "Z"); === cs.setString("prefix", "Z");

```

### RETURNING OUT PARAM
```
40: var sql = "{?= call magic_number(?) }";
41: try (var cs = conn.prepareCall(sql)) {
42: cs.registerOutParameter(1, Types.INTEGER);
43: cs.execute();
44:    System.out.println(cs.getInt("num"));
45: }
``` 
On line 40, we included two special characters ( ?=) to specify that the stored procedure has an output value. This is optional since we have the OUT parameter, but it does aid in readability.  

On line 42, we register the OUT parameter. This is important. It allows JDBC to retrieve the value on line 44. Remember to always call registerOutParameter() for each OUT or INOUT parameter (which we will cover next).

### WORKING WITH AN INOUT PARAMETER

```
50: var sql = "{call double_number(?)}"; 51: try (var cs = conn.prepareCall(sql)) {
52: cs.setInt(1, 8);
53: cs.registerOutParameter(1, Types.INTEGER);
54: cs.execute();
55:    System.out.println(cs.getInt("num"));
56: }
```

## COMPARING CALLABLE STATEMENT PARAMETERS

| Stored procedure parameter types |IN|OUT|INOUT|
|-|-|-|-|
|Used for input|Yes| No |Yes|
|Used for output|No |Yes |Yes|
|Must set parameter value|Yes |No |Yes|
|Must call registerOutParameter() |No |Yes |Yes|
|Can include ?=|No |Yes |Yes|







## Closing Database Resources

it is important to close resources when you are finished with them. This is true for JDBC as well. JDBC resources, such as a Connection, are expensive to create. Not closing them creates a resource leak that will eventually slow down your program.

Closing a JDBC resource should close any resources that it created. In particular, the following are true:
- Closing a Connection also closes PreparedStatement (or CallableStatement) and ResultSet.
- Closing a PreparedStatement (or CallableStatement) also closes the ResultSet


 you learned that it is possible to declare a type before a try‐with‐resources statement. Do you see why this method is bad?
 ```
40: public void bad() throws SQLException {
41:    var url = "jdbc:derby:zoo";
42:    var sql = "SELECT not_a_column FROM names";
43:    var conn = DriverManager.getConnection(url);
44:    var ps = conn.prepareStatement(sql);
45:    var rs = ps.executeQuery();
46:
47:    try (conn; ps; rs) {
48:       while (rs.next())
49:          System.out.println(rs.getString(1));
50: }
51: }
```
Suppose an exception is thrown on line 45. The try‐with‐resources block is never entered, so we don't benefit from automatic resource closing. That means this code has a resource leak if it fails. Do not write code like this.


There's another way to close a ResultSet. JDBC automatically closes a ResultSet when you run another SQL statement from the same Statement. This could be a PreparedStatement or a CallableStatement.

How many are closed?
```
14: var url = "jdbc:derby:zoo";
15: var sql = "SELECT count(*) FROM names where id = ?";
16: try (var conn = DriverManager.getConnection(url);
17:    var ps = conn.prepareStatement(sql)) {
18:
19:    ps.setInt(1, 1);
20:
21:    var rs1 = ps.executeQuery();
22:    while (rs1.next()) {
23:       System.out.println("Count: " + rs1.getInt(1));
24: }
25:
26:    ps.setInt(1, 2);
27:
28:    var rs2 = ps.executeQuery();
29:    while (rs2.next()) {
30:       System.out.println("Count: " + rs2.getInt(1));
31: }
32:    rs2.close();

```
!!!The correct answer is four!!! On line 28, rs1 is closed because the same PreparedStatement runs another query. On line 32, rs2 is closed in the method call. Then the try‐with‐resources statement runs and closes the PreparedSatement and Connection objects.


[prev](http://hjh.devsnips.nl/ocp20)
[next](http://hjh.devsnips.nl/ocp22)