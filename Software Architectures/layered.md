# Disadvantages

- Business logic directly depends on the database
- Presentation layer has a transitive dependency
- All entities, repositories, and ORM libraries are also available in the presentation layer
- The coupling also makes it unnecessarily difficult to upgrade the database or data access layer (e.g., to a new database version or a new version of the O/R mapper) this affects not only the database almost any kind of infrastructure the application accesses
- The weakening of layer boundaries also makes it impossible to test individual components in isolation – e.g., the business logic without a user interface and database.

All of above tempts developers to let the boundaries between the layers weaken, especially when they are pressed for time.

### examples:

- It is not uncommon for errors to occur because an attempt is made in the presentation layer to iterate over an uninitialized one-to-many collection of a JPA entity.

## we have to worry about:

**technical** issues such as transactions and lazy and eager loading in the **business layer**.


