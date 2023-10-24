# 🍜 Case Study #1: Danny's Diner
<img src="https://8weeksqlchallenge.com/images/case-study-designs/1.png" width="40%" height="40%">

---

## 📚 Table of Contents
- [Introduction](#introduction)
- [Business Task](#business-task)
- [Entity Relationship Diagram](#entity-relationship-diagram)
- [Datasets](#datasets)
- [Case Study Questions and Solutions](#case-study-questions-and-solutions)

Please note that all the information regarding the case study has been sourced from the following [link](https://8weeksqlchallenge.com/case-study-1/).

---

## Introduction
Danny seriously loves Japanese food so in the beginning of 2021, he decides to embark upon a risky venture and opens up a cute little restaurant that sells his 3 favourite foods: sushi, curry and ramen.

Danny’s Diner is in need of your assistance to help the restaurant stay afloat - the restaurant has captured some very basic data from their few months of operation but have no idea how to use their data to help them run the business.

---

## Business Task
Danny wants to use the data to answer a few simple questions about his customers, especially about their visiting patterns, how much money they’ve spent and also which menu items are their favourite.

---

## Entity Relationship Diagram
Danny has shared 3 key datasets for this case study: sales, menu & members.

You can inspect the entity relationship diagram below.

<img src="https://github.com/5ifar/8-Week-SQL-Challenge/assets/146955609/8e73b555-65cd-499d-ab5f-5d5dabff326a" width="50%" height="50%">

---

## Datasets
All datasets exist within the dannys_diner database schema on the linked DB Fiddle below.

**Table 1: sales**

The sales table captures all customer_id level purchases with an corresponding order_date and product_id information for when and what menu items were ordered.

**Table 2: menu**

The menu table maps the product_id to the actual product_name and price of each menu item.

**Table 3: members**

The final members table captures the join_date when a customer_id joined the beta version of the Danny’s Diner loyalty program.

---

## Case Study Questions and Solutions
The following queries have been executed using PostgreSQL v13 on [DB Fiddle](https://www.db-fiddle.com/f/2rM8RAnq7h5LLDTzZiRWcd/138).

**1. What is the total amount each customer spent at the restaurant?**
#### Code:
```sql
SELECT
  sales.customer_id,
  SUM(menu.price) AS total_sales
FROM dannys_diner.sales
INNER JOIN dannys_diner.menu
  ON sales.product_id = menu.product_id
GROUP BY sales.customer_id
ORDER BY sales.customer_id ASC;
```
#### Steps:
- Implement INNER JOIN to merge `dannys_diner.sales` and `dannys_diner.menu` tables based on `product_id` as we need `sales.customer_id` and `menu.price` values from the tables.
- Group the results by `sales.customer_id`.
- Perform `SUM` Aggregation to calculate the total sales contributed by each customer.

#### Answer:
|customer_id|total_sales|
|-|-|
|A|76|
|B|74|
|C|36|
- Customer A spent $76.
- Customer B spent $74.
- Customer C spent $36.

---

**2. How many days has each customer visited the restaurant?**
#### Code:
```sql
SELECT
  customer_id,
	COUNT(DISTINCT(order_date)) AS visit_count
FROM dannys_diner.sales
GROUP BY customer_id
ORDER BY customer_id ASC;
```
#### Steps:
- Group the results by `customer_id`.
- To determine the unique number of visits for each customer, we implement the `COUNT(DISTINCT ))` aggregation on `order_date` values.
- It's important to apply the DISTINCT keyword while calculating `visit_count` to avoid duplicate counting of days. For instance if Customer A visited the restaurant twice on '2021–01–01', counting without DISTINCT would result in 2 days instead of the accurate count of 1 day.

#### Answer:
|customer_id|visit_count|
|-|-|
|A|4|
|B|6|
|C|2|
- Customer A visited 4 times.
- Customer B visited 6 times.
- Customer C visited 2 times.

---

**3. What was the first item from the menu purchased by each customer?**
#### Code:
```sql
Yet to study CTEs.
```
#### Steps:


#### Answer:


---

**4. What is the most purchased item on the menu and how many times was it purchased by all customers?**
#### Code:
```sql
SELECT
  menu.product_name,
  COUNT(sales.order_date) AS purchase_count
FROM dannys_diner.sales
INNER JOIN dannys_diner.menu
	ON sales.product_id = menu.product_id
GROUP BY menu.product_name
ORDER BY purchase_count DESC
LIMIT 1;
```
#### Steps:
- Implement INNER JOIN to merge `dannys_diner.sales` and `dannys_diner.menu` tables based on `product_id` as we need `menu.product_name` and `sales.order_date` values from the tables.
- Group the results by `menu.product_name`.
- Perform a `COUNT` aggregation on the `sales.order_date` column and `ORDER BY` the result in descending order using the `purchase_count` alias.
- Apply the LIMIT 1 clause to filter and retrieve the highest `purchase_count` item.

#### Answer:
|product_name|purchase_count|
|-|-|
|ramen|8|
- Ramen is the Most purchased item (8 times) on the menu.

---

**5. Which item was the most popular item for each customer?**
#### Code:
```sql

```
#### Steps:


#### Answer:


---

**6. Which item was purchased first by the customer after they became a member?**
#### Code:
```sql

```
#### Steps:


#### Answer:


---

**7. Which item was purchased just before the customer became a member?**
#### Code:
```sql

```
#### Steps:


#### Answer:


---

**8. What is the total items and amount spent for each member before they became a member?**
#### Code:
```sql

```
#### Steps:


#### Answer:


---

**9. If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?**
#### Code:
```sql

```
#### Steps:


#### Answer:


---

**10. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?**
#### Code:
```sql

```
#### Steps:


#### Answer:


---
