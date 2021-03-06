NgModule is a decorator function that takes a single metadata object whose properties describe the module. The most important properties are

- declarations - the view classes that belong to this module. Angular has three kinds of view classes: components, directives, and pipes.

- exports - the subset of declarations that should be visible and usable in the component templates of other modules.

- imports - other modules whose exported classes are needed by component templates declared in this module.

- providers - creators of services that this module contributes to the global collection of services; they become accessible in all parts of the app.

 - bootstrap - the main application view, called the root component, that hosts all other app views. Only the root module should set this bootstrap property.

#Component
```
AppComponent.ts
	import { Component } from '@angular/core';

	@Component({
	  selector: 'app-root',
	  templateUrl: './app.component.html',
	  styleUrls: ['./app.component.scss']
	})
	export class AppComponent {
	  title = 'app';
	}
	
app.module.ts
	declarations: [
		AppComponent,
		CalcComponent
	],
```
#Service
```
app.module.ts
	providers: [ProductService],
product.service.ts
	import { Observable } from 'rxjs/Observable';
	import { Injectable } from '@angular/core';
	import { HttpClient } from '@angular/common/http';
	
	constructor(private http: HttpClient) { }

	getProducts(): Observable<Product[]>{
		return this.http.get<Product[]>("http://localhost:3000/products");
	}
	
	products:Product[];
	
	constructor(private productService: ProductService) { }
	
	ngOnInit() {
		this.getProducts();
	}

	getProducts(){
		this.productService.getProducts()
			.subscribe(products => this.products= products);
	}
```
