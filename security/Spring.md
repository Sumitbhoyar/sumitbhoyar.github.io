
# Spring Security

## Dependencies
org.springframework.security => spring-security-core
org.springframework.boot => spring-boot-starter-security

## Introduction
Spring Security is installed as a single Filter in the chain, and its concrete type is **FilterChainProxy**. Spring Security is a single physical Filter but delegates processing to a chain of internal filters. In a Spring Boot app the security filter is a @Bean in the ApplicationContext, and it is installed by default so that it is applied to every request.
It is the **FilterChainProxy** which contains all the security logic arranged internally as a chain (or chains) of filters. All the filters have the same API (they all implement the Filter interface from the Servlet Spec) and they all have the opportunity to veto the rest of the chain.


The @EnableWebSecurity is a marker annotation. It allows Spring to find (it's a @Configuration and, therefore, @Component) and automatically apply the class to the global WebSecurity.
The @EnableWebSecurity annotation and WebSecurityConfigurerAdapter work together to provide web based security.
By extending WebSecurityConfigurerAdapter and over-riding methods we are able to do the following:
1. Authentication - In Memory, JDBC, JPA or custom
2. Require the user to be authenticated prior to accessing any URL within our application
3. Enables HTTP Basic and Form based authentication
4. Spring Security will automatically render a login page and logout success page for you


## Task 1: Set up In-Memory Authentication

    @Configuration
    public class ApplicationSecurity extends WebSecurityConfigurerAdapter {
    @Autowired
    public void configureGlobal(AuthenticationManagerBuilder auth) 
      throws Exception {
    	auth.inMemoryAuthentication()
    	  .withUser("user").password("password").roles("USER")
    	  .and()
    	  .withUser("admin").password("password").roles("USER", "ADMIN");
    	}
    }

## Task 2: Set up JDBC Authentication

    create table users(
      username varchar_ignorecase(50) not null primary key,
      password varchar_ignorecase(50) not null,
      enabled boolean not null);
    
    create table authorities (
      username varchar_ignorecase(50) not null,
      authority varchar_ignorecase(50) not null,
      constraint fk_authorities_users foreign key(username) references users(username));
      create unique index ix_auth_username on authorities (username,authority);

    @Configuration
    public class ApplicationSecurity extends WebSecurityConfigurerAdapter {	  
    	@Autowired
    	private DataSource dataSource;
    	@Autowired
    	public void configureGlobal(AuthenticationManagerBuilder auth) 
    	  throws Exception {
    		auth.jdbcAuthentication().dataSource(dataSource)
    		  .withDefaultSchema();
    	}
    }

## Task 3: Setup custom authentication

    @Service
    public class MyUserDetailsService implements UserDetailsService {
     
        @Autowired
        private UserRepository userRepository;
     
        @Override
        public UserDetails loadUserByUsername(String username) {
            User user = userRepository.findByUsername(username);
            if (user == null) {
                throw new UsernameNotFoundException(username);
            }
            return new MyUserPrincipal(user);
        }
    }
    public class MyUserPrincipal implements UserDetails {
        private User user;
     
        public MyUserPrincipal(User user) {
            this.user = user;
        }
        //...
    }
    @Configuration
    public class ApplicationSecurity extends WebSecurityConfigurerAdapter {
    	@Autowired
    	private MyUserDetailsService userDetailsService;
    	 
    	@Override
    	protected void configure(AuthenticationManagerBuilder auth)
    	  throws Exception {
    		auth.authenticationProvider(authenticationProvider());
    	}
    	 
    	@Bean
    	public DaoAuthenticationProvider authenticationProvider() {
    		DaoAuthenticationProvider authProvider
    		  = new DaoAuthenticationProvider();
    		authProvider.setUserDetailsService(userDetailsService);
    		authProvider.setPasswordEncoder(encoder());
    		return authProvider;
    	}
    }

## Task 4: Authorize user

    @Configuration
    public class ApplicationConfigurerAdapter extends WebSecurityConfigurerAdapter {
      @Override
      protected void configure(HttpSecurity http) throws Exception {
        http.antMatcher("/foo/**")
          .authorizeRequests()
            .antMatchers("/foo/bar").hasRole("BAR")
            .antMatchers("/foo/spam").hasRole("SPAM")
            .anyRequest().isAuthenticated();
      }
    }

## Task 5: Add custom filter

    public class CustomFilter extends GenericFilterBean {
        @Override
        public void doFilter(
          ServletRequest request, 
          ServletResponse response,
          FilterChain chain) throws IOException, ServletException {
            chain.doFilter(request, response);
        }
    }
    
    @Configuration
    public class CustomWebSecurityConfigurerAdapter
      extends WebSecurityConfigurerAdapter {
        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http.addFilterAfter(
              new CustomFilter(), BasicAuthenticationFilter.class);
        }
    }

## Task 6: Method security

    @SpringBootApplication
    @EnableGlobalMethodSecurity(securedEnabled = true)
    public class SampleSecureApplication {
    }
    
    @Service
    public class MyService {
      @Secured("ROLE_USER")
      public String secure() {
        return "Hello Security";
      }
    }


