# Spring Data JPA

## Overview

Spring Data JPA simplifies the development of data access layers by providing a repository abstraction on top of JPA. It supports the creation of repository beans by simply extending predefined repository interfaces.

### Hibernate

Hibernate is an ORM (Object-Relational Mapping) tool used in Java programming. It simplifies data manipulation, querying, and retrieval in relational databases.

### Annotations

Annotations in Hibernate are used to define relationships between entities, specify mapping details, and configure various aspects of the entity behavior:

- **OneToOne:** Defines a one-to-one relationship between two entities. This annotation is used to map a single-valued association between two entities.

- **OneToMany:** Defines a one-to-many relationship between two entities. This annotation is used on the parent entity to refer to a collection of child entities.

- **ManyToOne:** Defines a many-to-one relationship between two entities. This annotation is used on the child entity to reference the parent entity.

- **ManyToMany:** Defines a many-to-many relationship between two entities. This annotation is used to map the association between two collections of entities.
