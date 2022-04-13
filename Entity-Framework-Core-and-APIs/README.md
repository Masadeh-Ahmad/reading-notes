Some things this MVC tutorial has that the Razor Pages tutorial doesn't:

Implement inheritance in the data model
Perform raw SQL queries
Use dynamic LINQ to simplify code

Some things the Razor Pages tutorial has that this one doesn't:

Use Select method to load related data
Best practices for EF.

Entity Framework (EF) Core is a lightweight, extensible, open-source, and cross-platform version of the popular Entity Framework data access technology.

EF Core can serve as an object-relational mapper (O/RM), which:

Enables .NET developers to work with a database using .NET objects.
Eliminates the need for most of the data-access code that typically needs to be written.

With EF Core, data access is performed using a model. A model is made up of entity classes and a context object that represents a session with the database. The context object allows querying and saving data

Instances of your entity classes are retrieved from the database using Language Integrated Query (LINQ). For more information

Data is created, deleted, and modified in the database using instances of your entity classes.




While EF Core is good at abstracting many programming details, there are some best practices applicable to any O/RM that help to avoid common pitfalls in production apps:

Intermediate-level knowledge or higher of the underlying database server is essential to architect, debug, profile, and migrate data in high performance production apps. For example, knowledge of primary and foreign keys, constraints, indexes, normalization, DML and DDL statements, data types, profiling, etc.
Functional and integration testing: It's important to replicate the production environment as closely as possible to:
Find issues in the app that only show up when using a specific versions or edition of the database server.
Catch breaking changes when upgrading EF Core and other dependencies. For example, adding or upgrading frameworks like ASP.NET Core, OData, or AutoMapper. These dependencies can affect EF Core in unexpected ways.
Performance and stress testing with representative loads. The naïve usage of some features doesn't scale well. For example, multiple collections Includes, heavy use of lazy loading, conditional queries on non-indexed columns, massive updates and inserts with store-generated values, lack of concurrency handling, large models, inadequate cache policy.
Security review: For example, handling of connection strings and other secrets, database permissions for non-deployment operation, input validation for raw SQL, encryption for sensitive data.
Make sure logging and diagnostics are sufficient and usable. For example, appropriate logging configuration, query tags, and Application Insights.
Error recovery. Prepare contingencies for common failure scenarios such as version rollback, fallback servers, scale-out and load balancing, DoS mitigation, and data backups.
Application deployment and migration. Plan out how migrations are going to be applied during deployment; doing it at application start can suffer from concurrency issues and requires higher permissions than necessary for normal operation. Use staging to facilitate recovery from fatal errors during migration. For more information, see Applying Migrations.
Detailed examination and testing of generated migrations. Migrations should be thoroughly tested before being applied to production data. The shape of the schema and the column types cannot be easily changed once the tables contain production data. For example, on SQL Server, nvarchar(max) and decimal(18, 2) are rarely the best types for columns mapped to string and decimal properties, but those are the defaults that EF uses because it doesn't have knowledge of your specific scenario.

Data seeding is the process of populating a database with an initial set of data.

There are several ways this can be accomplished in EF Core:

Model seed data
Manual migration customization
Custom initialization logic

