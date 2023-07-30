# What is Hexagonal Architecture?

- **Alistair Cockburn** introduced the hexagonal software architecture in [a blog article](https://alistair.cockburn.us/hexagonal-architecture/) in 2005.
- The application should be equally controllable by users, other applications, or automated tests. For the business logic, it makes no difference whether it is invoked from a user interface, a REST API, or a test framework.
- The business logic should be able to be developed and tested in isolation from the database, other infrastructure, and third-party systems. From a business logic perspective, it makes no difference whether data is stored in a relational database, a NoSQL system, XML files, or proprietary binary format.
- Infrastructure modernization (e.g., upgrading the database server, adapting to changed external interfaces, upgrading insecure libraries) should be possible without adjustments to the business logic.



# Ports and Adapters

![Hexagonal architecture with business logic in the core (“application”), ports, adapters, and external components](https://www.happycoders.eu/wp-content/uploads/2023/01/hexagonal-architecture.v2-600x431.png)

- Business logic (“application”) is at the core of the architecture.
- Business logic communicates with the outside world through well-defined interfaces (“ports”).
- Ports for make others control core:
  - API
  - User Interface
  - Other Applications
- Ports for controlling others through core:
  - Database
  - External interfaces
  - Other infrastructure
- All port and its use-cases are implemented exclusively against the specifications of the ports (Designated by the business logic)





![Hexagonal architecture with control flow](https://www.happycoders.eu/wp-content/uploads/2023/01/hexagonal-architecture-with-control-flow.v4-800x474.png)

The above illustration shows an exemplary application which:

1. is controlled by a user via a user interface,
2. is controlled by a user via a REST API,
3. is controlled by an external application via the same REST API,
4. controls a database and
5. controls an external application.

## Ingoing vs. Outgoing Ports

![Hexagonal architecture: port with user interface and REST adapter](https://www.happycoders.eu/wp-content/uploads/2023/01/hexagonal-architecture-driving-ports-and-adapters-600x348.png)

![Hexagonal architecture: port with a database adapter](https://www.happycoders.eu/wp-content/uploads/2023/01/hexagonal-architecture-driven-port-and-adapter-600x348.png)



# Big Picture

This is a big picture of this architecture, you can see how hexagonal architecture utilizes the port & adapter capability to seperate the technical concerns and implies being loosely coupled

![Hexagonal Architecture Map](https://raw.githubusercontent.com/mohammadhb/awesome-architecture/main/hexagonal-architecture.webp)



Sources:

https://www.happycoders.eu/software-craftsmanship/hexagonal-architecture/
