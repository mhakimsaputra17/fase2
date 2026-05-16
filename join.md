# PostgreSQL SQL JOIN Assessment

## Database
PostgreSQL

---

# Setup Database

## DDL

```sql
CREATE TABLE users (
    id BIGSERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL
);

CREATE TABLE restaurants (
    id BIGSERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    city VARCHAR(100) NOT NULL
);

CREATE TABLE menus (
    id BIGSERIAL PRIMARY KEY,
    restaurant_id BIGINT NOT NULL,
    name VARCHAR(100) NOT NULL,
    price NUMERIC(10,2) NOT NULL,

    CONSTRAINT fk_restaurant
        FOREIGN KEY (restaurant_id)
        REFERENCES restaurants(id)
        ON DELETE CASCADE
);

CREATE TABLE orders (
    id BIGSERIAL PRIMARY KEY,
    user_id BIGINT NOT NULL,
    restaurant_id BIGINT NOT NULL,
    total_price NUMERIC(10,2) NOT NULL,
    status VARCHAR(50) NOT NULL,

    CONSTRAINT fk_user
        FOREIGN KEY (user_id)
        REFERENCES users(id),

    CONSTRAINT fk_restaurant_order
        FOREIGN KEY (restaurant_id)
        REFERENCES restaurants(id)
);
```

---

# Seed Data

```sql
INSERT INTO users (name, email) VALUES
('Andi', 'andi@mail.com'),
('Budi', 'budi@mail.com'),
('Citra', 'citra@mail.com');

INSERT INTO restaurants (name, city) VALUES
('Warung Nusantara', 'Jakarta'),
('Sushi Tokyo', 'Bandung'),
('Burger Boss', 'Surabaya');

INSERT INTO menus (restaurant_id, name, price) VALUES
(1, 'Nasi Goreng', 25000),
(1, 'Mie Ayam', 20000),
(2, 'Salmon Sushi', 50000),
(3, 'Cheese Burger', 35000);

INSERT INTO orders (user_id, restaurant_id, total_price, status) VALUES
(1, 1, 45000, 'completed'),
(1, 2, 50000, 'completed'),
(2, 1, 25000, 'pending');
```

---

# Initial Data Visualization

---

## users

| id | name  | email |
|---|---|---|
| 1 | Andi | andi@mail.com |
| 2 | Budi | budi@mail.com |
| 3 | Citra | citra@mail.com |

---

## restaurants

| id | name | city |
|---|---|---|
| 1 | Warung Nusantara | Jakarta |
| 2 | Sushi Tokyo | Bandung |
| 3 | Burger Boss | Surabaya |

---

## menus

| id | restaurant_id | name | price |
|---|---|---|---|
| 1 | 1 | Nasi Goreng | 25000 |
| 2 | 1 | Mie Ayam | 20000 |
| 3 | 2 | Salmon Sushi | 50000 |
| 4 | 3 | Cheese Burger | 35000 |

---

## orders

| id | user_id | restaurant_id | total_price | status |
|---|---|---|---|---|
| 1 | 1 | 1 | 45000 | completed |
| 2 | 1 | 2 | 50000 | completed |
| 3 | 2 | 1 | 25000 | pending |

---

# TASK 1 — INNER JOIN

## Question

Tampilkan:
- nama user
- nama restaurant
- total transaksi
- status order

untuk semua order yang ada.

---


---

## Expected Output

| user_name | restaurant_name | total_price | status |
|---|---|---|---|
| Andi | Warung Nusantara | 45000.00 | completed |
| Andi | Sushi Tokyo | 50000.00 | completed |
| Budi | Warung Nusantara | 25000.00 | pending |

---

# TASK 2 — LEFT JOIN

## Question

Tampilkan semua user beserta order mereka.

User yang belum pernah order tetap harus muncul.

---

---

## Expected Output

| user_name | order_id |
|---|---|
| Andi | 1 |
| Andi | 2 |
| Budi | 3 |
| Citra | NULL |

---

# TASK 3 — LEFT JOIN + NULL

## Question

Tampilkan user yang belum pernah order.

---


---

## Expected Output

| name |
|---|
| Citra |

---

# TASK 4 — GROUP BY

## Question

Hitung total transaksi tiap user.

---


---

## Expected Output

| name | total_transaction |
|---|---|
| Andi | 95000.00 |
| Budi | 25000.00 |

---

# TASK 5 — MULTI TABLE JOIN

## Question

Tampilkan:
- nama menu
- harga
- nama restaurant
- kota restaurant

---

## Expected Query


---

## Expected Output

| menu_name | price | restaurant_name | city |
|---|---|---|---|
| Nasi Goreng | 25000.00 | Warung Nusantara | Jakarta |
| Mie Ayam | 20000.00 | Warung Nusantara | Jakarta |
| Salmon Sushi | 50000.00 | Sushi Tokyo | Bandung |
| Cheese Burger | 35000.00 | Burger Boss | Surabaya |

---

# TASK 6 — Aggregation + JOIN

## Question

Hitung jumlah order yang dimiliki tiap restaurant.

---

## Expected Query


---

## Expected Output

| name | total_orders |
|---|---|
| Sushi Tokyo | 1 |
| Warung Nusantara | 2 |
| Burger Boss | 0 |

---

# TASK 7 — Restaurant Without Orders

## Question

Tampilkan restaurant yang belum pernah menerima order.

---

## Expected Query

---

## Expected Output

| name |
|---|
| Burger Boss |

---

# TASK 8 — Advanced JOIN

## Question

Tampilkan:
- nama user
- jumlah order
- total transaksi

Urutkan dari total transaksi terbesar.

---



---

## Expected Output

| name | total_orders | total_transaction |
|---|---|---|
| Andi | 2 | 95000.00 |
| Budi | 1 | 25000.00 |
| Citra | 0 | NULL |

---

# PostgreSQL Notes

## BIGSERIAL

Digunakan untuk:
```sql
auto increment bigint
```

---

## NUMERIC(10,2)

Digunakan untuk currency agar:
- presisi aman
- tidak floating point issue

---

# Bonus Production Question

## Question

Kenapa query JOIN bisa lambat saat table besar?

---

## Expected Discussion

Candidate should mention:
- indexing
- sequential scan
- missing index
- cardinality
- query planner
- large dataset

---

# What Interviewer Should Observe

## Technical
- JOIN fluency
- aliasing
- aggregation
- filtering NULL
- grouping

---

## Problem Solving
- memilih JOIN type yang tepat
- memahami business context

---

# Evaluation Guide

## Incapable
- syntax JOIN tidak jalan

## Capable
- basic INNER JOIN bisa

## Decent
- memahami LEFT JOIN dan aggregation

## Proficient
- query clean
- reasoning bagus
- memahami production impact
