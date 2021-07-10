# Spring App Basics

- we will use it to build our backend server .
- we can create our backend automatically by the website or make it manually  

## Starting with Spring Initializr

- we will use gradle to build our backend server.

- the dependency we use :

```Java
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
	implementation 'org.springframework.boot:spring-boot-starter-web'
	developmentOnly 'org.springframework.boot:spring-boot-devtools'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
}
```

***Manual Initialization***

1. we will Navigate to <https://start.spring.io>. ,this service pulls in all the dependencies you need for an application and does most of the setup for us.

2. we will choose gradle and for the dependencies we will choose Spring Web, Thymeleaf, and Spring Boot DevTools.

3. then generate then download.

### Create a Web Controller

- @Controller  : will handled  HTTP requests by a controller .
- @GetMapping : ensures that HTTP GET requests to /greeting (the target path) are mapped to the greeting() method.
- @RequestParam :  the value of the query string parameter.
**query string parameter is not required**

## Spring Boot Devtools

- its like nodemon in the node js .
- features:

1. Enables hot swapping.

2. Switches template engines to disable caching.

3. Enables LiveReload to automatically refresh the browser.

4. Other reasonable defaults based on development instead of production.

### Run the Application

the application class :

``` 
package com.example.servingwebcontent;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class ServingWebContentApplication {

    public static void main(String[] args) {
        SpringApplication.run(ServingWebContentApplication.class, args);
    }

}
```

- @SpringBootApplication : that contain the main method you would to run and it contain:

1. @Configuration : tags this class as a source of the application
2. @EnableAutoConfiguration : Tells Spring Boot to start adding beans based on classPath settings.
3. @ComponentScan : tell the Spring to look the other component and configuration in com/example package

- The main() method uses Spring Boot’s SpringApplication.run() method to launch an application

### Build an executable JAR

- we can run the application on gradle by ./gradlew bootRun
- we can build the application on gradle by ./gradlew build
- Example:

java -jar build/libs/gs-serving-web-content-0.1.0.jar

### Test the Application

- the server url : <http://localhost:8080/greeting>

- we can provide query parameters in the url like : <http://localhost:8080/greeting?name=User>

### Add a Home Page

- we can make HTML,CSS,JavaScript but the Spring Boot application service  provide it

# Spring MVC and Thymeleaf: how to access data from templates

## Spring model attributes

- Spring MVC calls the pieces of data that can be accessed during the execution of views model attributes.
- there are many ways to add modules like :

1. Add attribute to Model via its addAttribute method:

```
 @RequestMapping(value = "message", method = RequestMethod.GET)
        public String messages(Model model) {
            model.addAttribute("messages", messageRepository.findAll());
            return "message/list";
        }
```

2. ModelAndView with model attributes included:

```
@RequestMapping(value = "message", method = RequestMethod.GET)
        public ModelAndView messages() {
            ModelAndView mav = new ModelAndView("message/list");
            mav.addObject("messages", messageRepository.findAll());
            return mav;
        }
```

3. Expose common attributes via methods annotated with @ModelAttribute:

```
@ModelAttribute("messages")
        public List<Message> messages() {
            return messageRepository.findAll();
        }
```

- we cant accessed the method without the message .

## Request parameters

- we can send request parameters in the Url or in the body with jason formatting like :
 <https://example.com/query?q=Thymeleaf+Is+Great> .
- to access q parameters we use the prefix param like :

```HTML
  <p th:text="${param.q}">Test</p>
```

## Session attributes

- mySessionAttribute : its like request parameters and we can access it by using the session. prefix

## ServletContext attributes

- The ServletContext attributes are shared between requests and sessions.
- we use the prefix #servletContext.  to access it .
- like:

```HTML
<td th:text="${#servletContext.getAttribute('myContextAttribute')}">42</td>
```

## Spring beans

- Thymeleaf allows accessing beans registered at the Spring Application Context with the @beanName syntax .

```HTML
    <div th:text="${@urlService.getApplicationUrl()}">...</div> 
```

- @urlService refers to a Spring Bean registered at your context .
