# Castlewood-Records
ERD for a music shop

```mermaid

erDiagram
    CUSTOMER {
        int id PK
        string name
        string email
        string phone
        datetime created_at
    }

    ALBUM {
        int id PK
        string title
        string artist
        string genre
        datetime release_date
        float price
        int available_stock
    }

    SONG {
        int id PK
        int album_id FK
        string title
        string artist
        float price
        datetime release_date
        int available_stock
    }

    PURCHASE {
        int id PK
        int customer_id FK
        int album_id FK
        int song_id FK
        datetime purchase_date
        float total_price
        string purchase_method
    }

    EMPLOYEE {
        int id PK
        string name
        string email
        string role
    }

    INVENTORY_UPDATE {
        int id PK
        int employee_id FK
        int album_id FK
        int song_id FK
        string update_type
        datetime update_time
        float new_price
    }

    MANAGER {
        int id PK
        string name
        string email
    }

    REPORT {
        int id PK
        int manager_id FK
        datetime report_date
        string report_type
        text content
    }

    CUSTOMER ||--o{ PURCHASE : "makes"
    ALBUM ||--o{ PURCHASE : "part of"
    SONG ||--o{ PURCHASE : "part of"
    EMPLOYEE ||--o{ INVENTORY_UPDATE : "makes"
    INVENTORY_UPDATE ||--o{ ALBUM : "updates"
    INVENTORY_UPDATE ||--o{ SONG : "updates"
    MANAGER ||--o{ REPORT : "generates"
