# design-patterns

* ## 2PC Pattern
  ##### Why is it used?:
  2PC is used to ensure the successful completion of a transaction across multiple data sources, guaranteeing data integrity and preventing inconsistencies in the system.
  ##### How does it work?:
  2PC involves two stages, involving a coordinator and participants.
  In the first stage (voting phase), the coordinator asks all participants if they can execute the transaction.
  If all participants confirm their ability to execute the transaction, the coordinator proceeds to the second stage (commit phase) and confirms the transaction;
   otherwise, it cancels the transaction. This ensures that the transaction is only committed if all participants can complete it.
  ##### Limitations:
  2PC has some disadvantages. Particularly, if a single participant fails, it can be difficult or impossible to roll back the transaction. Additionally, there are risks such as long-term locking and performance issues.
* ## Saga Pattern
    * ### Choreography-Based Saga
      ##### Why is it used?:
      Saga Choreography is an alternative approach to managing distributed transactions in a microservices architecture, focusing on decentralized coordination without a central orchestrator. Each service in the saga is responsible for coordinating its own local transactional actions and interactions with other services.
      ##### How does it work?:
       In Saga Choreography, services collaborate through event-driven communication. Each service listens for specific events, triggers its own actions upon receiving events, and emits events to notify other services about state changes. There is no central orchestrator; instead, the saga's progression emerges from the interactions between services based on predefined choreography rules.
       ##### Limitations:
       While Saga Choreography avoids the single point of failure and potential bottlenecks of a central orchestrator, it can lead to increased complexity in managing the saga's overall behavior. Ensuring consistency and handling failures across distributed services can be challenging, requiring careful design and implementation of event-driven workflows.
    * ### Orchestration-Based Saga
      ##### Why is it used?:
      Saga Orchestration is used to manage distributed transactions in a microservices architecture by introducing a central component, known as the orchestrator, to coordinate the execution of a saga (a sequence of transactional steps involving multiple services).
      ##### How does it work?:
      In Saga Orchestration, the orchestrator is responsible for managing the saga's execution flow. It coordinates the invocation of individual service actions, monitors their progress, and handles compensating actions in case of failures. The orchestrator sends commands to the participating services and controls the overall transaction's progression.
      ##### Limitations:
      While Saga Orchestration provides centralized control and visibility over the saga's execution, it introduces a single point of failure with the orchestrator. Additionally, it can create tight coupling between services and the orchestrator, potentially impacting scalability and flexibility.

 * ## Compensating Transaction Pattern
 * ## Event Sourcing
   ##### What is it?:
   Event Sourcing is a software design pattern that involves capturing all changes to an application's state as a sequence of events. Instead of storing the current state of an entity, Event Sourcing involves storing a log of events that describe actions or state transitions that have occurred over time. These events represent the facts or changes that have happened in the system.
   ##### How does it work?:
   * Capture Events: Whenever a change occurs in the system, instead of directly updating the state of an entity, an event representing that change is appended to an event log. These events are immutable and contain all the information needed to reconstruct the state of the system.
   * Store Events: The events are stored in an event store, which is typically a persistent data store optimized for appending events. Each event is associated with a unique identifier, timestamp, and metadata, and they are stored in the order in which they occurred.
   * Replay Events: To reconstruct the current state of an entity or the entire system, all the events from the event log are replayed in sequence. By applying each event to an initial state, the system can derive the current state. This process is deterministic and idempotent, ensuring that the same state is reached regardless of how many times the events are replayed.
   * Derived Views: In addition to replaying events to reconstruct state, Event Sourcing allows for the creation of derived views or projections. These are optimized data structures or views that represent the state of the system in a format suitable for specific queries or use cases. Derived views can be updated asynchronously as events are processed, providing efficient read access to the application's data.
   ##### Benefits:
   * Full Audit Trail: The event log provides a complete audit trail of all changes to the system, enabling traceability and compliance with regulatory requirements.
   * Temporal Querying: Since events are stored over time, it's possible to query the state of the system at any point in time, allowing for temporal queries and historical analysis.
   * Resilience: The event log acts as a durable record of the system's history, making it resilient to failures and providing mechanisms for disaster recovery and replay.
   * Scalability: By decoupling command processing from query processing and leveraging asynchronous updates, Event Sourcing can scale effectively to handle high throughput and concurrent access patterns.

 * ## CQRS (Command Query Responsibility Segregation)
   ##### What is it?:
   CQRS is a pattern that separates the responsibilities of handling commands (requests that change the system state) from queries (requests that retrieve data). In a traditional architecture, reads and writes are often handled by the same components, but CQRS advocates for splitting them into separate paths.
   ##### Why is it used?:
   CQRS offers benefits such as improved scalability, performance, and flexibility. By segregating the responsibilities of commands and queries, each path can be optimized independently. For example, the write path can focus on consistency and transactionality, while the read path can focus on scalability and performance.
   ##### How does it work?:
   In a system following the CQRS pattern, commands are handled by command handlers, which update the state of the system based on the received commands. On the other hand, queries are handled by query handlers, which retrieve data from read-optimized data stores. The separation of concerns allows for better optimization and scalability of both paths.
   ##### Limitations:
   * Increased Complexity: Implementing separate paths for commands and queries adds complexity to the system architecture, leading to longer development times and higher maintenance overhead.
   * Learning Curve: Adopting CQRS requires a shift in mindset and understanding, which may result in a steeper learning curve for developers and team members.
   * Eventual Consistency Issues: Separating write and read paths can lead to eventual consistency challenges, requiring developers to address data synchronization and consistency concerns.
   * Higher Development Effort: Implementing CQRS often requires more development effort due to the need for designing and implementing command and query handlers, data models, and synchronization mechanisms.
   * Operational Overhead: Managing separate data stores for reads and writes introduces operational overhead, including monitoring, maintenance, and data synchronization tasks.
   * Potential for Over-Engineering: CQRS may not be suitable for all applications, and implementing it where unnecessary can lead to over-engineering and increased complexity without significant benefits.
