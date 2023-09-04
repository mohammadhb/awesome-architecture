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
# Transactional Messaging
# Zero-Payload Events

