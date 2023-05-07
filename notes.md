# java_core

Core concepts of Java SE
##
- SOLID Principles (not specific to Java)

      1- Single Responsibility for Each class -> Just one reason 
      to change the class.

		Advantages:

			Fewer tests for each class.

			Lower coupling –> fewer dependencies.

			Smaller and well-organized classes
		 
      2- Class shoud be Opened for Extension and Closed for Modification.
	
	   Otherwise -> modifying the existing code -> potential new bugs
	   
	   If fixing bugs -> extend the class

      3- Liskov Substitution: If class A is a subtype of class B, one should
      be able to replace B with A without disrupting the behavior of the program.
