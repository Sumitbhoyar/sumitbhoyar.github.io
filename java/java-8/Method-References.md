
# Java Method References

Method reference is used to refer method of functional interface.
A method reference is a simplified form (or short-hand) of a lambda expression. It specifies the class name or the instance name followed by the method name. Instead of writing the lambda expression with all the details such as parameter and return type, a method reference lets you create a lambda expression from an existing method implementation.

Method Reference Syntax: < class or instance name>::< methodName>

## Types of Method References

#### Reference to a static method.

Syntax-

    ContainingClass::staticMethodName 

 

Example-

    interface Sayable{  
        void say();  
    }  
    public class MethodReference {  
        public static void saySomething(){  
            System.out.println("Hello, this is static method.");  
        }  
        public static void main(String[] args) {  
            Sayable sayable = MethodReference::saySomething;  
            sayable.say();  
        }  
    }  

#### Reference to an instance method.

Syntax-

    containingObject::instanceMethodName  

Example-

    interface Sayable{  
        void say();  
    }
    public class InstanceMethodReference {
        public void saySomething(){
            System.out.println("Hello, this is non-static method.");
        }
        public static void main(String[] args) {
            InstanceMethodReference methodReference = new InstanceMethodReference();
    		Sayable sayable = methodReference::saySomething;
    		sayable.say();
        }  
    }  

#### Reference to a constructor - Constructor Reference.

Syntax-

    ClassName::new  

Example-

    interface Messageable{  
        Message getMessage(String msg);  
    }  
    class Message{  
        Message(String msg){  
            System.out.print(msg);  
        }  
    }  
    public class   {  
        public static void main(String[] args) {  
            Messageable hello = Message::new;  
            hello.getMessage("Hello");  
        }  
    }  

#### Tricky example

    class Arithmetic{  
    	public static int add(int a, int b){  
    		return a+b;  
    	}  
    	public static float add(int a, float b){  
    		return a+b;  
    	}  
    	public static float add(float a, float b){  
    		return a+b;  
    	}  
    }  
    public class MethodReference {  
    	public static void main(String[] args) {  
    		BiFunction<Integer, Integer, Integer>adder1 = Arithmetic::add;  
    		BiFunction<Integer, Float, Float>adder2 = Arithmetic::add;  
    		BiFunction<Float, Float, Float>adder3 = Arithmetic::add;  
    		int result1 = adder1.apply(10, 20);  
    		float result2 = adder2.apply(10, 20.0f);  
    		float result3 = adder3.apply(10.0f, 20.0f);  
    		System.out.println(result1);  
    		System.out.println(result2);  
    		System.out.println(result3);  
    	}  
    }  
