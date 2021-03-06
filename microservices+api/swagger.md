**What is Swagger? **

The goal of Swagger is to define a standard, language-agnostic interface to REST APIs which allows both humans and computers to discover and understand the capabilities of the service without access to source code, documentation, or through network traffic inspection.

Spring Boot makes developing RESTful services ridiculously easy — and using Swagger makes documenting your RESTful services easy.

Building a back-end API layer introduces a whole new area of challenges that goes beyond implementing just endpoints. You now have clients which will now be using your API. Your clients will need to know how to interact with your API. In SOAP-based web services, you had a WSDL to work with. This gave API developers an XML-based contract, which defined the API. However, with RESTFul web services, there is no WSDL. Thus your API documentation becomes more critical.

**Dependency**
```
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
    <version>2.6.1</version>
    <scope>compile</scope>
</dependency>
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.6.1</version>
    <scope>compile</scope>
</dependency>
```

**Application configuration**
```
@Configuration
@EnableSwagger2
public class SwaggerConfig {
    @Bean
    public Docket productApi() {
        return new Docket(DocumentationType.SWAGGER_2)
                .select()
                .apis(RequestHandlerSelectors.basePackage("guru.springframework.controllers"))
                .paths(regex("/product.*"))
                .build()
                .apiInfo(metaData());
    }
    private ApiInfo metaData() {
        ApiInfo apiInfo = new ApiInfo(
                "Spring Boot REST API",
                "Spring Boot REST API for Online Store",
                "1.0",
                "Terms of service",
                new Contact("John Thompson", "https://springframework.guru/about/", "john@springfrmework.guru"),
               "Apache License Version 2.0",
                "https://www.apache.org/licenses/LICENSE-2.0");
        return apiInfo;
    }
}
```

**URL**
```
http://localhost:8080/swagger-ui.html
```

**Customising Documentation**
```
@ApiOperation(value = "View a list of available products",response = Iterable.class)
@ApiResponses(value = {
		@ApiResponse(code = 200, message = "Successfully retrieved list"),
		@ApiResponse(code = 401, message = "You are not authorized to view the resource"),
		@ApiResponse(code = 403, message = "Accessing the resource you were trying to reach is forbidden"),
		@ApiResponse(code = 404, message = "The resource you were trying to reach is not found")
}
)
@RequestMapping(value = "/list", method= RequestMethod.GET, produces = "application/json")
public Iterable<Product> list(Model model){
	Iterable<Product> productList = productService.listAllProducts();
	return productList;
}
```

**Annotations for Model fields**
```
@ApiModel( value = "Person", description = "Person resource representation" )
public class Person {
    @ApiModelProperty( value = "Person's first name", required = true ) 
    private String email;
}	
```

**OpenAPI Specification**

The OpenAPI Specification, originally known as the Swagger Specification, is a specification for machine-readable interface files for describing, producing, consuming, and visualizing RESTful Web services. A variety of tools can generate code, documentation and test cases given an interface file. 

The OpenAPI Specification (OAS) defines a standard, language-agnostic interface to RESTful APIs which allows both humans and computers to discover and understand the capabilities of the service without access to source code, documentation, or through network traffic inspection. When properly defined, a consumer can understand and interact with the remote service with a minimal amount of implementation logic.

An OpenAPI definition can then be used by documentation generation tools to display the API, code generation tools to generate servers and clients in various programming languages, testing tools, and many other use cases.

An OAS API definition file (swagger.json or swagger.yaml) describes all the elements of a REST API. The following interactive map shows a sample API definition file in the Swagger editor and the rendered output. You can click any highlighted area to open the corresponding topic.

**OpenAPI Document**
A document (or set of documents) that defines or describes an API. An OpenAPI definition uses and conforms to the OpenAPI Specification.

**Example**
```
swagger: '2.0'

# This is your document metadata
info:
  version: "1.0.0"
  title: Emplyee Service

# Describe your paths here
paths:
  # This is a path endpoint. Change it.
  /employees:
    # This is a HTTP operation
    get:
      # Describe this verb here. Note: you can use markdown
      description: |
        Gets `Employee` objects.
        Optional query param of **size** determines
        size of returned array
      # This is array of GET operation parameters:
      parameters:
        # An example parameter that is in query and is required
        -
          name: size
          in: query
          description: Size of array
          required: true
          type: number
          format: double
      # Expected responses for this operation:
      responses:
        # Response code
        200:
          description: Successful response
          # A schema describing your response object.
          # Use JSON Schema format
          schema:
            title: ArrayOfEmployees
            type: array
            items:
              title: Employee
              type: object
              properties:
                name:
                  type: string
                single:
                  type: boolean
```

**Generating Service or Client from Open API document**

- Open the Swagger editor at: http://editor2.swagger.io
- Select everything on the left side and delete it. You’ll start from scratch
- Create your API document
- Generate Client or service using API Document. Editor supports many language and framework.
