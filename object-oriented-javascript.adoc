```
//--JS Object--//
var Customer = {
	name:"Sumit",
	speak: function(){
		return "Hello " + this.name;
	},
	address:{
		city:"Pune"
	}
}

alert(Customer.speak())
alert(Customer.address.city)

Customer.name="Rashmi"
Customer.LastName="Bhoyar"
Customer.greet = function(){
	return "Good Morning " + Customer.name + Customer.LastName;
}

alert(Customer.greet())

//--Class--//
function Person(name, city){
	this.name = name;
	this.city=city;
	this.info = function(){
		return this.name + " lives at " + this.city;
	}
}

alert(new Person("Sumit", "Pune").info())

Person.prototype.hobby = function(hobby){
	return "My Hobby is " + hobby
}

var rashmi = new Person("Rashmi", "Pune")
alert(rashmi.hobby("Reading"))

//------------------------------------//
```
