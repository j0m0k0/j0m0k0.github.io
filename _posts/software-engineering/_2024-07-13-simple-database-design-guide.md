---
title: A Simple Guide to Database Design
date: 2024-07-13 17:20:00 -0500
categories: [Software Engineering, Database Design]
tags: [database, database-design]     # TAG names should always be lowercase
image: /assets/img/posts/database-design/cover.png
alt: "A Practical Introduction to Cybersecurity"
---
As a guy who works in the computer science area, there will be a lot of times that you come up with a small idea for a program and you want to do it by yourself. One of the important parts of each computer software is its data. How do you design this data system? Do we really need a system or database for storing data? In this post, I will introduce a step-by-step approach that helps you in designing a database for your software.

> This guide is for those who want to use relational databases for their application, if you want to use a NoSQL database, most of them concepts are still useful, but this article is not tailored for non-relational databases.
{: .prompt-info}

## 0. Understanding Data Models

A **data model** is an abstract model that organizes data elements and standardizes how they relate to one another and to properties of the real world entities. Among the most important models are the relational model, the document model, and the entity-relationship model. These models are essential because they help us structure our data in a way that makes it both efficient and meaningful for specific applications.

## 1. Ask Yourself: Do You Need a Database?

Deciding whether you need a database depends on the scale and purpose of your application. For small, single-user applications with non-critical data, simple file storage or even manual record-keeping might be sufficient. However, for applications that require handling complex queries, multiple users, data integrity, and security, a database is essential. **In other words, there are some questions that you can ask yourself and if their answer is YES, it means you need to use a database**:
- Do you need to run complex queries? (yes/no)
- Does your data will change frequently? (yes/no)
- Does you data size will increase over time? (yes/no)

## 2. Design Your Entity-Relationship Diagram

An **Entity-Relationship (ER) Diagram** is a type of structural diagram for use in database design. It provides a graphical representation of the entities, the relationships between them, and their attributes.
> ER Diagram, is not an standard. This means that there is not only true way of drawing an ER diagram. This is very important. Because sometimes, you just come up with an ER diagram and another person comes with another ER for the same problem. **THIS IS TOTALLY OK**. The only thing that matters is that which one is more  close to what you want?
{: .prompt-warning}

When it comes to designing an ER diagram, you have many options. You can have a `top-down strategy`, `bottom-up strategy` or other strategies.

Start by identifying the entities and their relationships. Then, determine the attributes of each entity. Also, determine the cardinality of the relationships.

## 3. Map It to Relational Model

To translate your ER diagram into a **relational model**, you convert entities into tables, relationships into foreign keys, and attributes into columns within these tables. The mappings of relationships is something you should consider.

## 4. Implement Your Relational Schema using a RDBMS

Once you have your relational model, the next step is to implement it in a relational database management system (RDBMS) like Oracle Database. This involves creating the tables according to the relational schema and then writing SQL queries to interact with the data.

## 5. Test Your Database Before Interacting With The Application
Before porting your database into your application, try to insert some data (can be fake) into your tables and run some queries to see if it works the same way that you want. If it was fine, you can proceed. Otherwise, You probably need to step back.

## 6. Improve your Database Design

To improve the database's efficiency and reduce data redundancy, apply **normalization** techniques. Normalization involves decomposing a table into less redundant (and more independent) tables but still containing the same information. It helps in maintaining data integrity and optimizing query performance. However, normalization at very high levels (e.g., 5NF) can introduce a performance overhead that you should be careful about it in real-world applications.

## 7. Backup is Important
Backup your data with a robust backup system. You can use the RDBMS itself for doing the backup, or use external services for that. Whatever it is, you should have a backup schedule for your database. Otherwise, you are developing an unstable software!

By following these steps, you can design a robust database system tailored to your software’s specific needs.
