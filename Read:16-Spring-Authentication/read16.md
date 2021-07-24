
# Spring Security Architecture

## Authentication and Access Control

-Two problems of app security:

1. authentication
2. authorization

- Authentication : AuthenticationManager is the main strategy interface for authentication.
- In its authenticate() function, AuthenticationManager can accomplish one of three things:

1. If it is unable to make a decision, it will return null. AuthenticationException is a runtime exception that is generally handled in a generic fashion by an application, depending on its style or purpose.
2. If it can verify that the input represents a genuine principal, it will return an Authentication.
3. If it feels the input represents an invalid principal, it will throw an AuthenticationException.

- Authentication Managers Can Be Customized The most popular configuration assistance provided by Spring Security is AuthenticationManagerBuilder, which allows you to easily set up basic authentication manager functionality in your application.

- AuthenticationManagerBuilder - supporting in-memory, JDBC, or LDAP user data, as well as creating a custom UserDetailsService.

- Authorization or Access Control .
- The AccessDecisionManager is the primary approach for authorization. The framework provides three implementations, each of which delegate to a chain of AccessDecisionVoter objects.
- An Authentication and a secure Object with ConfigAttributes are taken into account by AccessDecisionVoter.

# Spring Auth Cheat Sheet

1. set up a user model and repo
2. create a controller for that model
3. UserDetailsServiceImpl implements UserDetailsService (by get the user from database by his name )
4. ApplicationUser implements UserDetails

5. WebSecurityConfig extends WebSecurityConfigurerAdapter ; contain :

- UserDetailsService ,passwordEncoder bean ,configure AuthManagerBuilder
,configure HttpSecurity(cors? csrf?).

6. registration page
7. login page
