# PostgreSQL-Relationships

## This repository is about the how to effectively use relationships in PostgreSQL .

## What is Relationship?

### In a relational database, relationships are used to connect data between two or more tables. They are used to enforce data integrity, ensure data consistency, and provide a flexible and scalable data model. PostgreSQL supports three types of relationships: one-to-one, one-to-many, and many-to-many.

#### Note:- There are 3 types of table relationships in a relational database. The relationships can be enforced by defining the right foreign key constraints on the columns.
https://medium.com/@patrikstrausz17/part3-postgresql-relationships-creating-and-managing-database-relationships-5e1eaea769d8#:~:text=In%20a%20relational%20database%2C%20relationships,One%2Dto%2DOne

### 1) `One to One`

#### A one-to-one relationship exists between two tables where each record in one table is linked to only one record in another table, and vice versa. In other words, there is a one-to-one mapping between the two tables.

#### For example, let’s consider a database that stores information about countries and their capitals. Each capital is assigned only to one country, and each country can be assigned only one capital. Therefore, the capital and country tables have a one-to-one relationship.

```
CREATE TABLE capital (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100)
);

CREATE TABLE country (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  capital_id INTEGER,
  CONSTRAINT fk_capital FOREIGN KEY(capital_id) REFERENCES capital(id)
);
```

### 2) `One to Many`

#### A one-to-many relationship exists between two tables where each record in one table is linked to one or more records in another table, but each record in the other table is linked to only one record in the first table.

#### For example, let’s consider a database that stores information about customers and their orders. Each customer can have many orders, but each order is associated with only one customer. Therefore, the customer and order tables have a one-to-many relationship.

```
CREATE TABLE customer (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  address VARCHAR(100),
  email VARCHAR(100)
  );

CREATE TABLE "order" (
  id SERIAL PRIMARY KEY,
  order_date DATE,
  order_amount INTEGER,
  price DOUBLE PRECISION,
  customer_id INTEGER,
  CONSTRAINT fk_customer FOREIGN KEY(customer_id) REFERENCES customer(id)
);
```

### 2) `One to Many`

#### A many-to-many relationship exists between two tables where each record in one table is linked to one or more records in another table, and each record in the other table is linked to one or more records in the first table.

#### For example, let’s consider a database that stores information about users and their roles. Each user can have multiple roles, and each role can have multiple users. Therefore, the users and roles tables have a many-to-many relationship.

#### To implement a many-to-many relationship in PostgreSQL, you need to create a junction table that stores the relationships between the two tables. The junction table contains foreign keys from both tables and acts as a bridge between them.

```
CREATE TABLE users(
  id SERIAL PRIMARY KEY,
  firstname VARCHAR(100),
  lastname VARCHAR(100)
  );
CREATE TABLE roles(
  id SERIAL PRIMARY KEY,
  role VARCHAR(45)
);
CREATE TABLE users_roles(
id SERIAL PRIMARY KEY,
user_id INTEGER,
role_id INTEGER,
CONSTRAINT fk_users FOREIGN KEY(user_id) REFERENCES users(id),
CONSTRAINT fk_roles FOREIGN KEY(role_id) REFERENCES roles(id)
);
```

### Conclusion

#### Relationships are a fundamental aspect of relational databases and are essential for connecting data between two or more tables. PostgreSQL supports three types of relationships: one-to-one, one-to-many, and many-to-many. By understanding and implementing relationships correctly, you can create a robust and flexible database model that allows you to efficiently store and retrieve data.
