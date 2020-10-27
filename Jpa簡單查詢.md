JPA簡單操作-增刪改查



```
src
├───main
│   ├───java
│   │   └───com.udemy.me.demo
│   │       └───domain
│   │           │   Book.java
│   │           │   BookRepository.java
│   │       └───sevice
│   │           │   BookSevice.java
│   │       └───web
│   │           │   BookApp.java
```


```BookRepository.java
public interface BookRepository extends JpaRepository<Book,Long> {
}
```

```BookService
@Service
public class BookService {
    @Autowired
    private BookRepository bookRepository;


    public List<Book> findAll(){

        return bookRepository.findAll();
    }

    public Book save(Book book){
        return bookRepository.save(book);
    }

    public Book findOne(long id){
        return bookRepository.findById(id).get();
    }

    public void deleteOne(long id){
        bookRepository.deleteById(id);
    }
}
```

```BookApp
@RestController
@RequestMapping("/api/v1")
public class BookApp {
    @Autowired
    private BookService bookService;
    /*查詢
    */
    @GetMapping("/books")
    public List<Book> getAll(){
        return bookService.findAll();
    }
    /*新增
    */
    @PostMapping("/books")
    public Book post(Book book
                    /*@RequestParam String name,
                     @RequestParam String author,
                     @RequestParam String description,
                     @RequestParam int status*/){
    /*    Book book = new Book();
        book.setName(name);
        book.setAuthor(author);
        book.setDescription(description);
        book.setStatus(status);
*/        return bookService.save(book);
    }
    /*查詢一筆
    */
    @GetMapping("/books/{id}")
    public Book getOne(@PathVariable long id){
        return bookService.findOne(id);
    }
    /*更改一筆
    */
    @PutMapping("/books")
    public Book update(@RequestParam long id,
                       @RequestParam String name,
                       @RequestParam String author,
                       @RequestParam String description,
                       @RequestParam int status){
        Book book = new Book();
        book.setId(id);
        book.setName(name);
        book.setAuthor(author);
        book.setDescription(description);
        book.setStatus(status);
        return bookService.save(book);
    }
    /*刪除
    */
    @DeleteMapping("/books/{id}")
    public void deleteOne(@PathVariable long id){
        bookService.deleteOne(id);
    }
}
```