# SQL Learning & Advanced Queries - Sakila Database Study

## 📌 Project Overview
This document contains advanced SQL exercises performed on the **Sakila Sample Database** (a standard industry database for learning relational structures). While my other project focuses on business simulations, this study is dedicated to demonstrating my technical ability to handle complex relational logic, multi-table joins, and data aggregation.

## 🛠️ Technical Focus
* **Database Model:** Relational schema with 15+ linked tables.
* **Key Skills:** Complex JOINs, subqueries, and grouping data for reporting.

---

## 🔍 Advanced Query Scenarios

### 1. Multi-Table Data Retrieval (JOINs)
**Goal:** Retrieve a list of movies along with their categories by joining three different tables (`film`, `film_category`, and `category`).
* **Why this is important:** Shows the ability to navigate through "bridge" tables in a many-to-many relationship.

```sql
SELECT f.title, c.name AS category, f.release_year
FROM film f
JOIN film_category fc ON f.film_id = fc.film_id
JOIN category c ON fc.category_id = c.category_id
ORDER BY f.title ASC;
```

### 2. Identifying Customer Activity (Aggregation)
**Goal:** Find the top customers based on the total amount they spent on rentals.
* **Why this is important:** Demonstrates proficiency in using SUM, GROUP BY, and ORDER BY for financial reporting.

```sql
SELECT c.first_name, c.last_name, SUM(p.amount) AS total_spent
FROM customer c
JOIN payment p ON c.customer_id = p.customer_id
GROUP BY c.customer_id
ORDER BY total_spent DESC
LIMIT 10;
```

### 3. Inventory Availability Analysis
**Goal:** Verify which films are currently in stock and at which store locations.
* **Why this is important:** Tests the ability to link inventory data with physical store locations.

```sql
SELECT f.title, i.store_id, COUNT(i.inventory_id) as copies_available
FROM film f
JOIN inventory i ON f.film_id = i.film_id
GROUP BY f.title, i.store_id
HAVING copies_available > 1;
```

### 4. Cross-Relational Query (Customer Rental History)
**Goal:** List all movies rented by a specific customer to verify historical data integrity.

```sql
SELECT r.rental_date, f.title
FROM rental r
JOIN inventory i ON r.inventory_id = i.inventory_id
JOIN film f ON i.film_id = f.film_id
JOIN customer c ON r.customer_id = c.customer_id
WHERE c.email = 'MARY.SMITH@sakilacustomer.org'
ORDER BY r.rental_date DESC;
```
