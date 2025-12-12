Author: Timothee Frily, you're beloved Tech Lead.
# Introduction
This code guideline is here to help follow the principles and design pattern I found useful in order to make clean, reliable, testable and maintainable during the transcendence project.

I tried to review as carefully as I can,  some architectures and patterns.  My general choice was it is compatible with OOP and web apps (as transcendence). Also I didn't want concepts that strayed too far from what we already know.

Finally, I didn't want to choose too much rules or principles as the overload of informations can be daunting during development phase. I tried to keep as simple as possible.

# Use the MVC architecture.
My choice for the MVC (Model View Controller) architecture is based on, that this architecture have been [created for making user interfaces and it is used to make web applications](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller).

It divide the program logic into three interconnected elements:
- **model**, data, logic and rules of the application.
- **view**, show the data no logic in it.
- **controller**, accepts input and converts t to commands for the model.

On my opinion it combines well with the next point.
# Use the SOLID principles.
-  **S** - Single-Responsibility Principle 
	- *A class should have one and only one reason to change, meaning that a class should have only one job.*
- **O** -  Open/Closed Principle
	- *Objects or entities should be open for extension but closed for modification.*
- **L** -  Liskov's Substitution Principle
	- *Derived or child classes must be substitutable for their base or parent classes*
- **I** -Interface Segregation Principle
	- *do not force any client to implement an interface which is irrelevant to them*
- **D** - Dependency Inversion Principle
	- *High-level modules should not depend on low-level modules. Both should depend on abstractions*

Check the links in the sources they give good example and inside about the architecture and principles.
# Sources
[Medium MVC, MVP, MVVM - lue le 10.12.2025](https://medium.com/@ankit.sinhal/mvc-mvp-and-mvvm-design-pattern-6e169567bbad)
[DigitalOcean - SOLID Design Principles Explained - lue le 10.12.2025](https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#frequently-asked-questions-faqs)
[GeekforGeeks SOLID - lue le 11.12.2025](https://www.geeksforgeeks.org/system-design/solid-principle-in-programming-understand-with-real-life-examples/)
