**@ExceptionHandler**

The @ExceptionHandler annotated method is only active for that particular Controller, not globally for the entire application.


**HandlerExceptionResolver**

It will also allow us to implement a uniform exception handling mechanism in our REST API. Limitation is that it doesn’t set anything to the body of the Response. And for a REST API – the Status Code is really not enough information to present to the Client.


**Recommended approach**

**@ControllerAdvice**

The actual mechanism is extremely simple but also very flexible:

It allows full control over the body of the response as well as the status code

It allows mapping of several exceptions to the same method, to be handled together

It makes good use of the newer RESTful ResposeEntity response

We need to override a base method out of the ResponseEntityExceptionHandler and providing our own custom implementation.
```
public class RestResponseEntityExceptionHandler extends ResponseEntityExceptionHandler {
 
    @ExceptionHandler(value = { IllegalArgumentException.class, IllegalStateException.class })
    protected ResponseEntity<Object> handleConflict(RuntimeException ex, WebRequest request) {
        String bodyOfResponse = "This should be application specific";
        return handleExceptionInternal(ex, bodyOfResponse, 
          new HttpHeaders(), HttpStatus.CONFLICT, request);
    }
}
```

**Sample error response entity**
```
public class ApiError {
 
    private HttpStatus status;
    private String message;
    private List<String> errors;
...
}
```

**Common Errors and their method**

- ConstrainViolationException: This exception reports the result of constraint violations

- TypeMismatchException: This exception is thrown when try to set bean property with wrong type.

- MethodArgumentTypeMismatchException: This exception is thrown when method argument is not the expected type

- MethodArgumentNotValidException: This exception is thrown when argument annotated with @Valid failed validation

- HttpMessageNotReadableException: Malformed JSON request

**Handling Custom Error**

```
@ExceptionHandler(EntityNotFoundException.class)
   protected ResponseEntity<Object> handleEntityNotFound(
           EntityNotFoundException ex) {
       ApiError apiError = new ApiError(NOT_FOUND);
       apiError.setMessage(ex.getMessage());
       return buildResponseEntity(apiError);
   }
```

Reference:

http://www.baeldung.com/exception-handling-for-rest-with-spring

http://www.baeldung.com/global-error-handler-in-a-spring-rest-api

https://www.toptal.com/java/spring-boot-rest-api-error-handling
