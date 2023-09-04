# Synchronous Calls
Simply calling another service synchronously, usually via REST.

- Service 1--->calls--->Service 2

- Service 1--->waits--->Service 2
  - Processes the request and returns a response

- Service 1--->processes---->Service 2’s response
  - In the same transaction that triggered the communication

> Easy to grasp
> 
> Well supported by technologies

**Netflix** has open-sourced support for synchronous communication in the form of the [Feign](https://github.com/OpenFeign/feign) and [Hystrix](https://github.com/Netflix/Hystrix) libraries.

# Simple Messaging

| Type | Title | Description |
|---|---|---|
|  |  |  |
| Con | Automatic Retry | Depending on the message broker, we get a retry mechanism for free. If Service 2 is currently not available, the message broker will try to deliver the message again until Service 2 finally gets it. “Guaranteed Delivery” is the magic keyword. |
| Pro | Loose Coupling | Along the same lines, messaging makes the services loosely coupled since Service 2 doesn’t need to be available at the time Service 1 sends the message. |
| Con | Message Broker must not fail | Using a message broker, we just introduced a piece of central infrastructure that is needed by all services that want to communicate asynchronously. If it fails, hell will break loose (and all services cease functioning). |
| Con | Pipeline contains Schema | It’s worth noting that messages (even if they are JSON) define a certain schema within the message broker. If the format of a message changes (and the change is not backward compatible), then all messages of that type must have been processed by all subscribers before the new service versions can be deployed. This contradicts independent deployments, one of the main goals of microservices. This can be mitigated by only allowing backward-compatible changes to message formats (which may not always be possible). |
| Con | Two-Phase Commit | Another caveat is that we usually send messages as part of our business logic and the business logic is usually bound to a database transaction. If the database transaction rolls back, a message may have already been sent to the message broker. This can be addressed by implementing a two-phase commit between the database transaction and the message broker. However, a two-phase commit may not be supported by the database or the message broker and even if it is, it’s often a pain to get working and even more so to test reliably. |

# Transactional Messaging

| Type | Title | Description |
|---|---|---|
| Pro | No Need for Two-Phase Commit | Since we’re writing the message to a local database table we can use the same transaction that our business logic uses. If the business logic fails, the transaction is rolled back and so is our message. We cannot accidentally send messages anymore when our local transaction has been rolled back. |
|  | Message Broker may Fail | Since we’re storing our messages in the local database on the sending and the receiving side, the message broker may fail anytime and the system will magically heal itself once it’s back online. We can just send the messages again from our message database table. |
|  | Complex Setup | The above perks aren’t for free, of course. The setup is quite complex since we need to store the messages in the database of the sending and receiving services. Also, we need to implement jobs on both sides that poll the database, looking for unprocessed messages and then processing them by sending them to the message broker (on the sending side) or calling the business logic that processes the message (on the receiving side) |

# Zero-Payload Events

| Type | Title | Description |
|---|---|---|
|  | Dumb Pipe | This scenario takes most of the message structure from the message broker, making it a dumber pipe (as is desirable in a microservice architecture). We don’t have to think that much about maintaining backward compatibility within the message structure anymore since we have almost no message structure. Note, however, that the little message structure we have left should still change in a backward-compatible fashion between the two releases. |
|  | Combinable with Transactional Messaging | Combining the zero-payload approach with the transactional messaging approach from above, we gain all the benefits of not needing a two-phase commit and gaining a retry mechanism even when the message broker fails. This adds even more complexity to the solution though, since we now also have to implement synchronous calls between the services to get the event payloads. |
