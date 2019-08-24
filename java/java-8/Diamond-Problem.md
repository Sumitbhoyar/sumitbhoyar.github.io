# Diamond Problem

**Rule 1** – Classes take higher precedence than interfaces – Any method inherited from a class or a superclass is invoked over any default method inherited from an interface.

**Rule 2** – Derived interfaces or sub-interfaces take higher precedence than the interfaces higher-up in the inheritance hierarchy

**Rule 3** – In case Rule 1 and Rule 2 are not able to resolve the conflict then the implementing class has to specifically override and provide a method with the same method definition

**Scenario 1**

    InterfaceA
    	public void print()
    	
    InterfaceB extends InterfaceA
    
    InterfaceC extends InterfaceA

Result: No conflict


**Scenario 2**

    InterfaceA
    	public void print()
    	
    InterfaceB extends InterfaceA
    	public void print()
    
    InterfaceC extends InterfaceA
    	public void print()
	
Result: print method should be overridden
 