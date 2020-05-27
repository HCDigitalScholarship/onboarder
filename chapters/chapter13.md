---
title: '13 Python and Databases (May 27 PM)'
description:
  "How to work with databases with the Django ORM or Tortoise ORM. models.py"
prev: /chapter12
next: /chapter14
type: chapter
id: 13
---

<exercise id="1" title="That '70s Database Language">

```sql
SELECT people FROM party WHERE groove LIKE 'get Down' OR 'boogie';

```

<img src="https://img1.looper.com/img/gallery/we-finally-understand-why-that-70s-show-was-canceled/intro-1568723982.jpg" width="50%">

` SQL is like Latin for data analysts/scientists. You may not always realize you are using it, but you are probably using it.`






</exercise>

<exercise id="2" title="Relational Database Design">

Relational databases are still the most common form of data storage and management, even after all these years. They are essentially a series of tables, linked by common key values. Best practice for database design dictates that each table has a designated _primary key_ field, which acts a unique identifier for a database record.

Tables are linked through _foreign keys_, which match a field and value in one table with the primary key field and value in another table.


Relational databases are built on three types of relationships:

1. One-to-one
2. One-to-many
3. Many-to-many

<img src="er.png">

</exercise>
<exercise id="3" title="SQL">

Most relational databases use some flavor of SQL--structured query language--to query and manage the data.

[w3schools](https://www.w3schools.com/sql/default.asp)

[DigitalOcean: A Basic MySQL Tutorial](https://www.digitalocean.com/community/tutorials/a-basic-mysql-tutorial)

MySQL is one of the most longstanding and popular open-source database engines, with PostgreSQL as its more robust competition. "Postgres" has additional features like geospatial data and querying, which makes data-driven mapping possible. We use both in our projects, as MySQL is easier to use while Postgres's spatial capacity creates new project opportunities for us.

[Why should you care about PostGIS?--A Gentle Introduction to Spatial Databases](https://medium.com/@tjukanov/why-should-you-care-about-postgis-a-gentle-introduction-to-spatial-databases-9eccd26bc42b)

A long time ago, I wrote half a thing about database design principles. [Check it out!](https://docs.google.com/document/d/1TPVSVuMJk2kQ-G2rMBhBLoB5dH5ghQl0_H0IBP6FYIY/edit)

</exercise>



<exercise id="4" title="GraphQL">

GraphQL is a query language for your API, and a server-side runtime for executing queries by using a type system you define for your data. GraphQL isn't tied to any specific database or storage engine and is instead backed by your existing code and data. [src](https://graphql.org/learn/)

- [Tutorials](https://www.graphql.com/tutorials/)
- [FastAPI and GraphQL](https://fastapi.tiangolo.com/advanced/graphql/)
- [Building a graphql api with Django](https://stackabuse.com/building-a-graphql-api-with-django/)

</exercise>
