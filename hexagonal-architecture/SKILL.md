---
name: hexagonal-architecture
description: Build and maintain clean hexagonal architectures in coding projects using any language.
---

Please abide to the following designs principles.

## Layers

Hexagonal architectured applications are composed of three layers :
- Domain
- Application
- Infrastructure

### Domain

The domain layer contains all the business logic and is the heart of domain knowledge.

#### Root Aggregate

This is the base of the domain object graph. It is the top-level aggregate that ensures consistency and encapsulates other aggregates and entities within it.

#### Aggregate

Aggregates are clusters of related domain objects (entities and value objects) that are treated as a single unit for data changes. They have a root entity (the aggregate root) and define boundaries around groups of related objects.

#### Value Object

Value objects are immutable objects that are defined by their attributes rather than a unique identity. They describe characteristics or qualities and are typically used to represent concepts like money, dates, or addresses.

#### Domain Service

Domain services contain business logic that doesn't naturally belong to a single entity or value object. They coordinate multiple domain objects and encapsulate operations that involve multiple aggregates or entities.

They differ from application use cases by the fact that they do not need any information external to the domain layer that an application use case would collect through application ports.

### Application

The application layer is used to orchestrate the communication between the domain and infrastructure layers.

#### Ports

Ports are an abstraction layer between the application layer elements and concrete infrastructure layer implementations ensuring the lowest coupling possible between layers.

**Example :**

Let's say you need to grant access to a page on your blog to a certain user and you have a `GrantAccessToPage` use case.

In the infrastructure layer, you will have :

``` 
class UserEntity:

  id: str
```

``` 
class PostgresUserRepository:

  findById(id: str) -> UserEntity:
    return db.users.find({userId: id})
```

``` 
class PageEntity:

  id: str
  allowedUsers: str[]
```

``` 
class PostgresPageRepository:

  findById(id: str) -> PageEntity:
    return db.pages.find({pageId: id})

  update(page: PageEntity) -> PageEntity:
    return db.pages.persist(page)
```

In the application layer, you will have :

```
interface UserRepositoryPort:

  findById(id) -> UserEntity
```

```
interface PageRepositoryPort:

  findById(id) -> PageEntity
  update(page: PageEntity) -> PageEntity
```

```
class GrantAccessToPage:

  constructor(userRepo: UserRepositoryPort, pageRepo: PageRepositoryPort)

  grant(pageId: str, userId: str) -> Void:
    user = userRepo.findById(userId)
    page = pageRepo.findById(pageId)

    page.allowedUsers += user.id

    pageRepo.update(page)
```

#### Use Cases

Every macroscopic task should be embodied by a use case such as CreateUser, DeleteBlogPost, GrantAccessToPage, etc.

They are in charge of calling all the domain and infrastructure objects that are envolved in the business use case.

### Infrastructure

The infrastructure layer in the inbound and outbound communication layer of your application. It is tightly coupled to the technologies your are using to interact with the outside world.

IMPORTANT: elements within the infrastructure layer shouldn't depend on each other, if those elements need to interact you should go through the application layer as a middleman through either a `Port` or a `Use Case`.

#### Repositories

Repositories are used to persist data using a specific storage technology such as databases, caches, filesystems, etc.