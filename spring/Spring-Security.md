**Spring Security**
--------------------

**Basic Concepts**

**Principal** - means a user, device or some other system which can perform an action in your application

**Authentication** - who are you? The process of establishing a principal is who they claim to be.

**Authorization** - what are you allowed to do? The process of deciding whether a principal is allowed to perform an action within your application.

Spring Security provides comprehensive security services for Java EE-based enterprise software applications. 

**Getting spring security**
```
artifactId>spring-security-web
artifactId>spring-security-config
```
OR
```
artifactId>spring-boot-starter-security
```

**Configuration**

Configuration could be done using WebSecurityConfigurerAdapter
If spring security is not auto configured then use @EnableWebSecurity for a class extending WebSecurityConfigurerAdapter.
If its auto configured then annotation is not needed for configuration class.

**springSecurityFilterChain**:
Spring Security's web infrastructure is based entirely on standard servlet filters. It doesn't use servlets or any other servlet-based frameworks (such as Spring MVC) internally, so it has no strong links to any particular web technology. Spring Security maintains a filter chain internally where each of the filters has a particular responsibility and filters are added or removed from the configuration depending on which services are required. springSecurityFilterChain is responsible for all the security (protecting the application URLs, validating submitted username and passwords, redirecting to the log in form, etc) within your application. 

**FilterChainProxy**:
Spring Security's web infrastructure should only be used by delegating to an instance of FilterChainProxy. The security filters should not be used by themselves. FilterChainProxy lets us add a single entry to web.xml and deal entirely with the application context file for managing our web security beans. It is wired using a DelegatingFilterProxy.

**HttpSecurity**:
How does Spring Security know that we want to require all users to be authenticated? How does Spring Security know we want to support form based authentication? The reason for this is that the WebSecurityConfigurerAdapter provides a default configuration in the configure(HttpSecurity http) method.

- All users to be authenticated:- ```.authorizeRequests().anyRequest().authenticated()```

- Enable form authentication:- ```.formLogin()```

- Enable basic authentication:- ```.httpBasic()```

- Allow some resource without authentication:- ```.antMatchers("/resources/**", "/signup", "/about").permitAll()```

- Restrict access to specific role:- ```.antMatchers("/db/**").access("hasRole('ADMIN') and hasRole('DBA')")```

- Login:- ```.formLogin().loginPage("/login").failureUrl("/login?error").usernameParameter("email").permitAll()```

- Logout:- ```.logout().logoutUrl("/my/logout").logoutSuccessUrl("/my/index")```

**Getting current logged in user**:
```java
Object principal = SecurityContextHolder.getContext().getAuthentication().getPrincipal();
```

**Getting user role**:
Method provided by Authentication is getAuthorities(). This method provides an array of GrantedAuthority objects. A GrantedAuthority is, not surprisingly, an authority that is granted to the principal. Such authorities are usually "roles", such as ROLE_ADMINISTRATOR or ROLE_HR_SUPERVISOR.

**Creating current user**:
UserDetails is used to build the Authentication object that is stored in the SecurityContextHolder by implementing interface UserDetailsService.
```java
UserDetails loadUserByUsername(String username) throws UsernameNotFoundException;
```

**Custom authenticator:**
```java
class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    public void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth
                .userDetailsService(userDetailsService)
                .passwordEncoder(new BCryptPasswordEncoder());
    }
}
```
**Add custom filter:**
Implement the org.springframework.web.filter.GenericFilterBean.
The GenericFilterBean is a simple javax.servlet.Filter implementation implementation that is Spring aware.
On to the implementation – we only need to implement a single method:

```java
	public class CustomFilter extends GenericFilterBean {
		@Override
		public void doFilter(
		  ServletRequest request, 
		  ServletResponse response,
		  FilterChain chain) throws IOException, ServletException {
			chain.doFilter(request, response);
		}
	}
	
	@Override
    protected void configure(HttpSecurity http) throws Exception {
        http.addFilterAfter(
          new CustomFilter(), BasicAuthenticationFilter.class);
    }
```
