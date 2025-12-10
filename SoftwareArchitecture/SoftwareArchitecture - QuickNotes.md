
What Pattern and design principles to use ?
- MVC -> j'aime bien.
- CQRS -> NOPE parce que pas utile pour notre use case.
- Actors -> fonctionel, mais differ trop de ce qu'on a fait.
- ACID CAP -> Bon pattern pour des base de donner critique mais notre cas n'est pas necessaire.
- SOLID -> 
- TDD 
- DDD

Things to keep in mind in my choice:
- Must apply to OOP.
- Must be good with web apps.

## MVC
- model = the data taht is required to display in the view and business logic, it defines the business rules for data means as how the data can be changed and manipulated.
- view = the UI components, display he data that is received from the controller. It monitors the model for any state change and display updated model.
- Controller = process incoming requests, mediator between the view and the model.
## MVP
- model = same as [MVC](##MVC) .
- view = UI componements, Does not containe any logic.
- presenter = manipulates the model and also updates the view.

## CQRS
Separating read and write operations into two distinct logical processes.

## Actors
Functionall patterns. Interesting 
## ACID and CAP
- Cap : for distributed databases.
## SOLID
- 'S'- Single-responsibility principle.
- 'O' - Open-Closed Principle.
- 'L' - Liskov Substitution Principle. need more info for clarification.
- 'I' - Interface Segregation Principle.
- 'D' - Dependency Inversion Principle.

# Sources
[Medium MVC, MVP, MVVM - lue le 10.12.2025](https://medium.com/@ankit.sinhal/mvc-mvp-and-mvvm-design-pattern-6e169567bbad)
[Stackoverflow What are MVP and MVC and what is the difference - lue le 10.12.2025](https://stackoverflow.com/questions/2056/what-are-mvp-and-mvc-and-what-is-the-difference)
[Microsoft - CQRS pattern - lue le 10.12.2025](https://learn.microsoft.com/en-us/azure/architecture/patterns/cqrs)
[CAP theorem - lue le 10.12.2025](https://www.bmc.com/blogs/cap-theorem/)
[DigitalOcean - SOLID Design Principles Explained - lue le 10.12.2025](https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design#frequently-asked-questions-faqs)

#SoftwareArchitecture #QuickNotes
