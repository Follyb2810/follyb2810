# Platform API v2 — RBAC Entity Relationship

```mermaid
erDiagram
    User ||--o{ UserRole : has
    Role ||--o{ UserRole : assigned
    User ||--o{ UserAppProfile : owns
    User ||--o{ Festival : creates
    Orisa ||--o{ Festival : hosts
    User ||--o{ Ticket : purchases

    User {
        string id PK
        string email UK
        string name
        boolean twoFactorEnabled
        datetime createdAt
        datetime updatedAt
    }

    Role {
        string id PK
        enum name UK
    }

    UserRole {
        string id PK
        string userId FK
        string roleId FK
        enum app "YORUBA_CALENDAR | TAX_FLOW | CLEANING_SERVICE | TICKETING"
    }

    UserAppProfile {
        string id PK
        string userId FK
        enum app
        enum type "INDIVIDUAL | COMPANY | SME"
    }

    Orisa {
        int id PK
        string name UK
        string userId FK
    }

    Festival {
        int id PK
        string title
        int orisaId FK
        string userId FK
        string eventType
    }

    Ticket {
        string id PK
        string userId FK
        string status
    }
```

## Apps & roles

| App | Example roles |
|-----|---------------|
| `YORUBA_CALENDAR` | USER, CREATOR, CALENDAR_MANAGER, ADMIN |
| `CLEANING_SERVICE` | USER, CLEANING_MANAGER, ADMIN |
| `TICKETING` | USER, TICKET_MANAGER, ADMIN |
| `TAX_FLOW` | USER, TAX_MANAGER, ADMIN |
