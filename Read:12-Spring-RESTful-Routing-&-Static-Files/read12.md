# Spring RequestMapping

## @RequestMapping Basics

1. @RequestMapping — by Path like

```Java
@RequestMapping(value = "/ex/foos", method = RequestMethod.GET)
```

- we can test the mapping is work or not by type in command line

```java
curl -i http://localhost:8080/spring-rest/ex/foos
```

2. @RequestMapping — the HTTP Method

- The HTTP method parameter has no default,without specify a value it will map to any HTTP request.

```Java
@RequestMapping(value = "/ex/foos", method = POST)
```

- we can test the mapping is work or not by type in command line

```java
curl -i -X POST http://localhost:8080/spring-rest/ex/foos
```

## RequestMapping and HTTP Headers

1. @RequestMapping With the headers Attribute

- by adding a header will decrease the size of mapping.

```Java
@RequestMapping(value = "/ex/foos", headers = "key=val", method = GET)
```

- we can test the mapping is work or not by type in command line

```java
curl -i -H "key:val" http://localhost:8080/spring-rest/ex/foos
```

- We can use multiple headers .

```Java
@RequestMapping(
  value = "/ex/foos", 
  headers = { "key1=val1", "key2=val2" }, method = GET)
  ```

- we can test the mapping is work or not by type in command line

```java
curl -i -H "key1:val1" -H "key2:val2" http://localhost:8080/spring-rest/ex/foos

```

2. @RequestMapping Consumes and Produces

- Mapping media types produced by a controller method is worth special attention.
- we should map request if its based on accept header.

```java
@RequestMapping(
  value = "/ex/foos", 
  method = GET, 
  headers = "Accept=application/json")
  ```

- test

```java
curl -H "Accept:application/json,text/html" 
  http://localhost:8080/spring-rest/ex/foos
  ```

## RequestMapping With Path Variables

- Parts of the mapping URI can be bound to variables via the @PathVariable annotation.

1. Single @PathVariable

```
@RequestMapping(value = "/ex/foos/{id}", method = GET)
```

- we can use @PathVariable  without the value if the name of method parameter matcher  the name of the path exactly.

2. Multiple @PathVariable

- we can use multiple value

```
 (@PathVariable long fooid, @PathVariable long barid)
 ```

- test 

```
curl http://localhost:8080/spring-rest/ex/foos/1/bar/2
```

3. @PathVariable With Regex

- we can regex in the pathVariable

```
@PathVariable long numericId
```

this will matches this :
```
http://localhost:8080/spring-rest/ex/bars/1
```

## RequestMapping With Request Parameters

- @RequestMapping allows easy mapping of URL parameters with the @RequestParam annotation.

```java
http://localhost:8080/spring-rest/ex/bars?id=100
@RequestMapping(value = "/ex/bars", method = GET)
@ResponseBody
public String getBarBySimplePathWithRequestParam(
  @RequestParam("id") long id) {
    return "Get a specific Bar with id=" + id;
}
```

- we extract and use value id from URL

## RequestMapping Corner Cases

1. @RequestMapping — Multiple Paths Mapped to the Same Controller Method

- there some case the mapping need more than one controller .

```java
@RequestMapping(
  value = { "/ex/advanced/bars", "/ex/advanced/foos" }, 
  method = GET)
@ResponseBody
public String getFoosOrBarsByPath() {
    return "Advanced - Get some Foos or Bars";
}

-curl commands should hit the same method:

curl -i http://localhost:8080/spring-rest/ex/advanced/foos
curl -i http://localhost:8080/spring-rest/ex/advanced/bars
```

2. @RequestMapping — Multiple HTTP Request Methods to the Same Controller Method

- multiple request can be mapping at the same controller. 

```
@RequestMapping(
  value = "/ex/foos/multiple", 
  method = { RequestMethod.PUT, RequestMethod.POST }
)
@ResponseBody
public String putAndPostFoos() {
    return "Advanced - PUT and POST within single method";
}
With curl, both of these will now hit the same method:

curl -i -X POST http://localhost:8080/spring-rest/ex/foos/multiple
curl -i -X PUT http://localhost:8080/spring-rest/ex/foos/multiple
```

3. @RequestMapping — a Fallback for All Requests

- To implement a simple fallback for all requests using a particular HTTP method

- for a single request.

```java
@RequestMapping(value = "*", method = RequestMethod.GET)
@ResponseBody
public String getFallback() {
    return "Fallback for GET Requests";
}
```

- for multiple requests.

```java
@RequestMapping(
  value = "*", 
  method = { RequestMethod.GET, RequestMethod.POST ... })
@ResponseBody
public String allFallback() {
    return "Fallback for All Requests";
}
```

4. Ambiguous Mapping Error

- is Error happened when Spring evaluates two or more request mappings to be the same for different controller methods.

- like:

```java
@GetMapping(value = "foos/duplicate" )
public String duplicate() {
    return "Duplicate";
}

@GetMapping(value = "foos/duplicate" )
public String duplicateEx() {
    return "Duplicate";
}
```

##  New Request Mapping Shortcuts

- Spring Framework 4.3 introduced a few new HTTP mapping annotations, all based on @RequestMapping:

@GetMapping/
@PostMapping/
@PutMapping/
@DeleteMapping/
@PatchMapping

## Spring Configuration

- we just need class to handle the all process.

# Accessing Data with JPA

- to add that we need to add dependencies Spring Data JPA and then H2 Database.

-  The default constructor exists only for the sake of JPA

## Build an executable JAR

- you can run the application by using ./gradlew bootRun
- can build the JAR file by using <./gradlew build> and then <-jar build/libs/gs-accessing-data-jpa-0.1.0.jar>

# CrudRepository, JpaRepository, and PagingAndSortingRepository in Spring Data

## Spring Data Repositories

- JpaRepository – which extends PagingAndSortingRepository and, in turn, the CrudRepository.

- CrudRepository provides CRUD functions.
- PagingAndSortingRepository provides methods to do pagination and sort records.
- JpaRepository provides JPA related methods such as flushing the persistence context and delete records in a batch.

- the JpaRepository contains the full API of CrudRepository and PagingAndSortingRepository.

```java
@Entity
public class Product {

    @Id
    private long id;
    private String name;

    // getters and setters
}
```

- And let's implement a simple operation – find a Product based on its name:

```java
@Repository
public interface ProductRepository extends JpaRepository<Product, Long> {
    Product findByName(String productName);
}
```

## CrudRepository

- CrudRepository interface:

```java
public interface CrudRepository<T, ID extends Serializable>
  extends Repository<T, ID> {

    <S extends T> S save(S entity);

    T findOne(ID primaryKey);

    Iterable<T> findAll();

    Long count();

    void delete(T entity);

    boolean exists(ID primaryKey);
}
```

- CRUD functionality:

1. save(…) – save an Iterable of entities. Here, we can pass multiple objects to save them in a batch.
2. findOne(…) – get a single entity based on passed primary key value
3. findAll() – get an Iterable of all available entities in database
4. count() – return the count of total entities in a table
5. delete(…) – delete an entity based on the passed object
6. exists(…) – verify if an entity exists based on the passed primary key value

## PagingAndSortingRepository

- repository interface, which extends CrudRepository:

```java
public interface PagingAndSortingRepository<T, ID extends Serializable> 
  extends CrudRepository<T, ID> {

    Iterable<T> findAll(Sort sort);

    Page<T> findAll(Pageable pageable);
}
```

- we  using Pageable  to specify at least :

1. Page size
2. Current page number
3. Sorting

## JpaRepository

- JpaRepository interface:

```java
public interface JpaRepository<T, ID extends Serializable> extends
  PagingAndSortingRepository<T, ID> {

    List<T> findAll();

    List<T> findAll(Sort sort);

    List<T> save(Iterable<? extends T> entities);

    void flush();

    T saveAndFlush(T entity);

    void deleteInBatch(Iterable<T> entities);
}
```

- its have the following methods :

1. findAll() – get a List of all available entities in database
2. findAll(…) – get a List of all available entities and sort them using the provided condition
3. save(…) – save an Iterable of entities. Here, we can pass multiple objects to save them in a batch
4. flush() – flush all pending task to the database
5. saveAndFlush(…) – save the entity and flush changes immediately
6. deleteInBatch(…) – delete an Iterable of entities. Here, we can pass multiple objects to delete them in a batch

## Downsides of Spring Data Repositories

1. we couple our code to the library and to its specific abstractions, such as `Page` or `Pageable`; that's of course not unique to this library – but we do have to be careful not to expose these internal implementation details.

2. by extending e.g. CrudRepository, we expose a complete set of persistence method at once. This is probably fine in most circumstances as well but we might run into situations where we'd like to gain more fine-grained control over the methods exposed, e.g. to create a ReadOnlyRepository that doesn't include the save(…) and delete(…) methods of CrudRepository.

