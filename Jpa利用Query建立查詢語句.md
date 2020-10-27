JPA Query規則查詢   
https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods  
Query建立新的查詢規則有一定的寫法
```java=
/*BookRepository.java*/
    public interface BookRepository extends JpaRepository<Book,Long> {
    /*Query規則*/
    List<Book> findByAuthor(String Author);

    List<Book> findByAuthorAndStatus(String author,int status);

    List<Book> findByDescriptionEndsWith(String des);

    List<Book> findByDescriptionContains(String des);
}
```
``` java
/*BookService.java*/
    public List<Book> findByAuthorAndStatus(String author,int status){
        return bookRepository.findByAuthorAndStatus(author,status);
    }
    public List<Book> findByDescriptionEndsWith(String des){
        return bookRepository.findByDescriptionEndsWith(des);
    }
    public List<Book> findByDescriptionContains(String des){
        return bookRepository.findByDescriptionContains(des);
    }
```
```java=
/*BookApp.java*/
    @PostMapping("/books/byand")
    public List<Book> findByAuthorAndStatus(@RequestParam String author,@RequestParam int status){
        return bookService.findByAuthorAndStatus(author,status);
    }
    @PostMapping("/books/byandwith")
    public List<Book> findByDescriptionEndsWith(@RequestParam String description){
        return bookService.findByDescriptionEndsWith(description);
    }
    @PostMapping("/books/bycon")
    public List<Book> findByDescriptionContains(@RequestParam String description){
        return bookService.findByDescriptionContains(description);
    }
```