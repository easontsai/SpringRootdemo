> # Spring Boot導入Hibernate
### 1.pim.xml
```
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

### 2.application-dev.yml

```
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/kuan?user=root
    username: root
    password: PASSWORD
  jpa:
    hibernate:
      ddl-auto: create
    show-sql: true
```

url: jdbc:mysql://localhost:3306/kuan?user=root

jdbc:mysql就是protocol

localhost:3306就是[hosts]，MySQL預設的port為3306

mydb就是[/database]，也就是要連線的資料庫名稱

[?properties]為連線時的額外參數**

![](https://i.imgur.com/J08XM41.png)
schemas為DB名稱

### 3.book.java
```
@Entity
public class book {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private long id;
    private String name;
    private String author;
    private int status;
    private String description;
```
類別做成實體＠Entity
宣告主鍵＠Id
@GeneratedValue(strategy = GenerationType.AUTO)
