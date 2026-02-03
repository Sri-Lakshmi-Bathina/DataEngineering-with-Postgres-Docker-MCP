<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Data Engineering with Postgres & Docker MCP

**Project Link:** [View Project](http://learn.nextwork.org/projects/mcp-data-engineer1)

**Author:** Sri Lakshmi Bathina  
**Email:** sbathina02@gmail.com

---

![Image](http://learn.nextwork.org/delighted_maroon_festive_grape/uploads/mcp-data-engineer1_er-diagram-screenshot)

---

## Introducing Today's Project!

In this project, I'm going to create and optimize a PostgreSQL database in a Docker container using MCPs within a Cursor. PostgreSQL is a relational database management system (RDBMS). Docker is used to create and manage the Postgres environment.

### Key tools and concepts

The key tools I used include MCP, Docker, and PostgreSQL. Key concepts I learnt include database optimization(index, FK, PK, scans, and more!), Docker containers, database schemas, uv Python environment, and using Cursor with data engineering MCPs.

### Challenges and wins

This project took me approximately 2 hours. The most challenging part was how database optimization works. It was most rewarding to see the improvement in database query speed. With the skills I learnt, I want to branch into learning more data engineering-focused MCPs like dbt, Airflow, Snowflake, and more!

### Why I did this project

I did this project today to learn how to use MCPs, get familiar with using Docker and PostgreSQL, and use Curso,r which helped getting better at data engineering. Another database skill I want to learn is running models on my database with the help of MCPs.

---

## Setting Up Docker and UV

In this step, I'm setting up my development environment by installing uv, a fast Python package manager, and Docker. Docker Desktop will help me create isolated environments to run containers. uv is a Python package manager, written in a compiled language (RUST), making it super fast.

![Image](http://learn.nextwork.org/delighted_maroon_festive_grape/uploads/mcp-data-engineer1_8h9i0j1k)

### What's Docker and why containers?

We are using a Docker container to minimize the trouble surrounding running containers/applications across different operating systems (OS). This is important because working in a team or with external hosting compute platforms often will not be the preferred system setup.

### Verifying installations

The dependencies I set up in my local environment were uv because it allows me to run MCP servers. Running --version for uv shows the version number and version ID, which confirms they were installed correctly, and now I'm ready to set up the MCPs.

---

## Connecting MCP Servers

In this step, I'm going to install MCP servers, which are programs that interact with external applications like Docker. Docker Without MCPs, Cursor can only interact with the codebase and use websearch, not talk directly (with API calls) to desktop apps or remotely hosted apps. With MCPs, the Cursor can run any specified API calls from the Cursor chat, based on a user's text input to interact with desktop or remotely hosted apps.

### Python project setup

The command uv init sets up a Python project because we need a Python environment to run the MCP servers. The files created include pyproject.toml which takes dependencies, .gitignore which hides specified files from git commits, README.md for project documentation, and main.py which functions as an example Python program for the environment.

### Installing Docker MCP

![Image](http://learn.nextwork.org/delighted_maroon_festive_grape/uploads/mcp-data-engineer1_mcp-config-screenshot)

---

## Building My Database

In this step, I'm going to use the Docker MCP to create a container to run a PostgreSQL database schema to hold 40K rows of e-commerce data, and the PostgreSQL MCP to create the database users so that we can run queries on the e-commerce data.

![Image](http://learn.nextwork.org/delighted_maroon_festive_grape/uploads/mcp-data-engineer1_postgres-container-screenshot)

### Database security

I created an application user called app. Every PostgreSQL database comes with a default superuser called postgres, which has admin level privilages/rights. The difference between a superuser and an application user is the execution ability level; a superuser can do everything, and an application user is only allowed to do a subset. This is a security best practice because it means that in the event of an account being compromised, the damage that can be done is very minimal(assuming they only gain access to an app user, NOT a superuser).


### Loading demo data

I loaded demo data by running a 'pip' command to pull the demo_data.sql contents into the PostgreSQL database. The demo_data.sql file contains 40K rows of e-commerce data.

### Verifying and visualizing the database

I verified my database by asking Cursor to read the database schema and sample 3 rows for each table to create a Mermaid ER diagram. The Mermaid ER diagram shows customers, orders, products, and order_items as tables and order_id, customer_id, order_date, status, total_amount, and region (for the order table) as columns. For example, the diagram shows that the products are connected to 'order_items', which are connected to orders and customers.

![Image](http://learn.nextwork.org/delighted_maroon_festive_grape/uploads/mcp-data-engineer1_er-diagram-screenshot)

---

## Performance Audit

I'm going to perform a database performance audit, which looks at slow queries that need optimizations, missing indexes that slow down searches, database health issues, bottlenecks, and inefficiencies. Database administrators care about this because slow queries in production can cause high costs because of biuld-up in query queues. This optimization helps by removing all of the pain points/bottlenecks slowing down the relational database.

### Audit findings

Cursor's audit analyzed database health, execution time, planning time, and scan types by running EXPLAIN ANALYZE, which looks into how queries execute. It found bottlenecks in missing FK (foreign keys). The recommendations included adding indexes, which will speed up scans on order.customer_id, order_items.order_id and order_items.product_id 

![Image](http://learn.nextwork.org/delighted_maroon_festive_grape/uploads/mcp-data-engineer1_performance-screenshot)

### Performance gains

I implemented the index recommendation for the query that filters orders by customer_id. After creating the index, performance improved by ~9.8x. The execution plan changed from a sequential scan to a bitmap index scan, which means constant performance around scaling.

---

---
