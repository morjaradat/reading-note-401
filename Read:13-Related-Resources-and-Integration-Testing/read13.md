# Working with Relationships in Spring Data REST

## One-to-One Relationship

- Two entity classes can have a one to one relationship using the @OneToOne annotation.

- the association will be owned by the first entity class by the end of the association.

- @RestResource annotation is optional and can be used to customize the endpoint.

- Make sure to have different names for each association resource.

- To expose these entities as resources, we need to create two repository interfaces for each of them, by extending the CrudRepository interface.

- To create the resources:

1. add an instance, and have the API return the JSON object.
2. Next send a GET request to the endpoint, which will return an empty object.
3. Create the association using the HTTP method PUT and a body containing the URI of the resource to bind to the association.
4. If you need to remove an association, we can call the endpoint with DELETE method.

## One-to-Many Relationship

- using the @OneToMany and @ManyToOne annotations and can have the optional @RestResource annotation to customize the association resource

## Many-to-Many Relationship

- using @ManyToMany annotation, to which we can add @RestResource.

## Testing the Endpoints With TestRestTemplate

- Create a test class that injects a TestRestTemplate instance and defines the constants we will use.

- Testing the One-to-One Relationship :

1. create a @Test method that saves objects by making POST requests to the collection resources.
2. Then save the relationship with a PUT request to the association resource and verifies that it has been established with a GET request to the same resource.

- Testing the One-to-Many Relationship :

1. create a @Test method that saves a instance and two other instances.
2. send a PUT request to each object's association resource, and verify that the relationship has been saved.

- Testing the Many-to-Many Relationship:

1. create a test method that saves one record and two other records.
2. Then it sends a PUT request to the association resource with the two URIs and verifies that the relationship has been established.

## Integration Testing in Spring

- Integration testing plays an important role in the application development cycle by verifying the end-to-end behavior of a system.

- Maven dependencies are required for running the integration tests:

1. junit-jupiter-engine
2. junit-jupiter-api
3. Spring test dependencies

- To assert results use Hamcrest and JSON path.

- Spring MVC Test Configuration - JUnit 5 enables the extension by adding the @ExtendWith annotation to our test classes and specifying the extension class to load, and to run the Spring test use SpringExtension.class.
-Also need the @ContextConfiguration annotation to load the context configuration and bootstrap the context that our test will use.
- Annotate the test with @WebAppConfiguration, which will load the web application context.

- WebApplicationContext : provides a web application configuration, and it loads all the application beans and controllers into the context.

- MockMvc : provides support for Spring MVC testing, and it encapsulates all web application beans and makes them available for testing. Initialize the mockMvc object in the @BeforeEach annotated method so that we don't have to initialize it inside every test.

- Writing Integration Tests :

1. First verify view name.
2. verify response body.
3. Send GET request with path variable and a query parameters.
4. send a POST request.

### MockMvc Limitations

1. MockMvc provides an elegant and easy-to-use API to call web endpoints and to inspect and assert their response at the same time, but has limitations.

2. It uses a subclass of the DispatcherServlet to handle test requests, which is responsible for calling controllers and performing all of the familiar Spring magic. The MockMvc class wraps this TestDispatcherServlet internally, so every time we send a request using the perform() method, MockMvc will use the underlying .

3. TestDispatcherServlet directly. Therefore, there are no real network connections made, and won't test the whole network stack.

4. Spring prepares a fake web application context to mock the HTTP requests and responses, it may not support all features of a full-blown Spring application.
