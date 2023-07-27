## Jeffrey Palermo:

- The main premise is that it controls coupling. 
- Emphasizes separation of concerns throughout the system.
- Emphasizes the use of interfaces for behavior contracts, and it forces the externalization of infrastructure.
- This architecture is not appropriate for small websites. It is appropriate for long-lived business applications as well as applications with complex behavior.
- All code can depend on layers more central, but code cannot depend on layers further out from the core.
- The *database* is not the **center**.  It is **external**.
- Decoupling the application from the database, file system, etc, lowers the cost of maintenance for the life of the application.
