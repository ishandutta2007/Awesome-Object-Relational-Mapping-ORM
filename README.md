# Awesome-Object-Relational-Mapping-ORM

# Top Object-Relational Mapping (ORM) Tools Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Data Mapper Patterns, Unit of Work & Type-Safe Query Building*  
**Last updated: March 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Object-Relational Mapping (ORM)**. These tools bridge the gap between object-oriented code and relational databases — mapping tables to classes, rows to objects, and foreign keys to references — while managing transactions, lazy loading, and schema migrations so you don't hand-write SQL for every CRUD operation.

**Examples** include Hibernate, TypeORM, Prisma, Drizzle, MikroORM, MyBatis, jOOQ, GORM, SQLAlchemy, and Entity Framework Core (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, type safety, and transparent query generation — ideal for backend engineers choosing between ORM abstraction and SQL control, and teams migrating away from abandoned libraries.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **Prisma Data Platform** — Managed services for Prisma ORM including **Accelerate** (global connection pooling and query caching for serverless) and **Pulse** (change data capture). **Best for teams using Prisma on serverless platforms** where direct database connections are problematic. The ORM itself is open source; the platform is the commercial layer.

- **PlanetScale** — Managed MySQL-compatible database with branching workflows that pair well with ORM migration systems. Not an ORM itself, but the database layer many TypeScript ORMs target.

## Open-Source GitHub Projects

- **[Hibernate](https://github.com/hibernate/hibernate-orm)**  
  **The reference ORM for Java and the JPA standard** — LGPL-2.1 licensed. **Implements the Java Persistence API (JPA)** with the most mature Data Mapper, Unit of Work, and Identity Map patterns in the Java ecosystem. **Handles complex object graphs, lazy loading, caching (first and second level), and dirty checking** automatically. **Hibernate 7.x** modernized the codebase for Jakarta EE 11 and improved query compilation. **Trade-offs**: **steep learning curve** and **notorious N+1 query problems** if you don't understand fetch strategies; abstraction leaks when you need database-specific features. **Best for enterprise Java applications** where the JPA standard and mature tooling outweigh the complexity.

- **[TypeORM](https://github.com/typeorm/typeorm)**  
  **The most established TypeScript ORM** — MIT licensed, **36,000+ GitHub stars** . **Supports Data Mapper and ActiveRecord patterns**, with decorators for entities and relations. **Works across PostgreSQL, MySQL, MariaDB, SQLite, SQL Server, Oracle, and MongoDB** from one API. **The largest ecosystem of tutorials and StackOverflow answers** — but much of that content is outdated (2018-2020 best practices are superseded) . **Development velocity has slowed** compared to its peak, though critical bugs are fixed and TypeScript 5.x is supported . **Trade-offs**: **not recommended for new projects in 2026** — Prisma and Drizzle offer better type safety and performance . **Best for teams maintaining existing TypeORM codebases** where migration cost exceeds the benefits of switching.

- **[Prisma](https://github.com/prisma/prisma)**  
  **The most downloaded ORM for Node.js and TypeScript** — Apache 2.0 licensed, **55.3 million npm downloads in the 30 days ending July 2026** — more than any other Node.js ORM, a position held since 2024 . **Schema-first workflow**: define models in a `.prisma` file, run `prisma generate`, and get a fully type-safe client with autocompletion. **Prisma Studio** provides a polished visual database browser for debugging and data exploration . **Prisma Migrate** has the smoothest migration workflow — diffs schema, generates SQL, prompts for name, and applies in one command . **Trade-offs**: **query engine binary adds 100-300ms to Lambda cold starts** — Prisma Accelerate moves the engine server-side for serverless; **requires raw SQL for complex queries** (window functions, recursive CTEs, lateral joins) that Drizzle handles natively . **Best for teams prioritizing developer experience and type safety** over raw SQL expressiveness.

- **[Drizzle ORM](https://github.com/drizzle-team/drizzle-orm)**  
  **The SQL-native TypeScript ORM for edge and serverless** — Apache 2.0 licensed, **48.1 million npm downloads in the 30 days ending July 2026** . **Zero binary dependency** — ~7kb bundle size and zero cold start overhead, making it the default choice for **Vercel Edge, Cloudflare Workers, and AWS Lambda** . **"If you know SQL, you know Drizzle"** — the API is SQL-like, so anything SQL can express, Drizzle can express, including window functions, recursive CTEs, and lateral joins without raw SQL escape hatches . **Drizzle Kit** handles migrations and schema management, with Drizzle Studio for visual browsing . **Native support for Cloudflare D1 (SQLite at the edge) and Turso** . **Best for edge/serverless deployments** and teams wanting SQL control without sacrificing type safety.

- **[MikroORM](https://github.com/mikro-orm/mikro-orm)**  
  **The architecturally rigorous TypeScript ORM** — MIT licensed, **8,800+ GitHub stars** . **The only mainstream TS ORM implementing Unit of Work + Identity Map + Data Mapper together** — foundational for DDD-style applications and complex domain models . **Unit of Work automatically batches inserts/updates into single transactions**, consistently outperforming manual transaction management in bulk operations . **Lowest open issue count relative to user base** (148 issues on 8.8K stars) — signals strong maintenance quality and responsive maintainers . **Supports PostgreSQL, MySQL, MariaDB, SQLite, libSQL, MS SQL Server, and MongoDB** from one API . **Trade-offs**: **class instantiation overhead and larger bundle** make it a harder sell for edge/serverless; **steeper learning curve** with decorators + entities + `em.flush()` pattern . **Best for teams building DDD-style applications** where architectural rigor matters more than edge deployment.

- **[MyBatis](https://github.com/mybatis/mybatis-3)**  
  **The SQL-first persistence framework for Java** — Apache 2.0 licensed. **You write the SQL, MyBatis maps results to objects** — no hidden query generation, no abstraction leaks. **XML or annotation-based mapping** with dynamic SQL support. **The choice when you need full control over queries** and don't want Hibernate's magic. **MyBatis-Plus** adds CRUD conveniences, pagination, and code generation for the MyBatis ecosystem . **Best for Java teams wanting SQL control** without abandoning object mapping.

- **[jOOQ](https://github.com/jOOQ/jOOQ)**  
  **The type-safe SQL builder for Java** — Apache 2.0 licensed (OSS edition). **Generates Java classes from your database schema**, giving you **compile-time checked SQL** — if you rename a column, the build breaks before runtime. **The sweet spot between ORM abstraction and raw SQL** — you write SQL-like code with full type safety. **Supports advanced SQL constructs** (window functions, CTEs, lateral joins) that ORMs struggle with. **Trade-offs**: **steep learning curve** and **code generation from schema is mandatory**. **Best for teams wanting SQL expressiveness with compile-time safety** and no ORM magic.

- **[GORM](https://github.com/go-gorm/gorm)**  
  **The most popular Go ORM** — MIT licensed, **39,900+ GitHub stars** . **"The fantastic ORM library for Golang, aims to be developer friendly"** . **Auto-migration, associations (has one, has many, belongs to, many to many), hooks, transactions, and raw SQL support**. **The default choice for Go web applications** using frameworks like Gin or Echo . **Best for Go developers** wanting Rails-like ORM ergonomics.

- **[SQLAlchemy](https://github.com/sqlalchemy/sqlalchemy)**  
  **The Python SQL toolkit and ORM** — MIT licensed. **Two layers**: the **Core** (SQL expression language with schema definition and query building) and the **ORM** (declarative models, sessions, relationships). **The most flexible Python database toolkit** — you can drop to raw SQL at any layer. **Alembic** handles migrations. **Best for Python teams wanting ORM convenience with SQL control** when needed.

### Additional Strong Open-Source Options

- **Entity Framework Core** — Microsoft's ORM for .NET with LINQ queries, change tracking, and migrations. MIT licensed. The default for .NET applications.
- **Sequelize** — The oldest JavaScript ORM. Still widely used but TypeScript support is retrofitted, not native . Best for legacy Node.js projects.
- **Objection.js** — SQL-friendly ORM built on Knex.js. **Author stopped active development in 2022**; a contributor took over but hadn't found time as of April 2026 . Not recommended for new projects.
- **Bookshelf.js** — ORM built on Knex.js. **No release in six years** and a maintainer question unanswered since March 2022 . Avoid for new projects.
- **Waterline** — The Sails.js ORM. **No release or commit since December 2022** . Avoid for new projects.
- **Beego ORM** — Built into the Beego web framework for Go. 32,400+ stars .
- **sqlc** — Generates type-safe Go code from SQL. Not a traditional ORM — you write SQL, it generates the Go. 18,300+ stars .
- **ent** — An entity framework for Go with schema-as-code and graph traversal. 17,200+ stars .

**Frameworks for building custom systems**: Combine **Prisma** for TypeScript projects prioritizing developer experience with the smoothest migrations, **Drizzle** for edge/serverless deployments and SQL-native control, **MikroORM** for DDD-style applications needing Unit of Work and Identity Map, **Hibernate** for enterprise Java on the JPA standard, **jOOQ** for Java teams wanting compile-time-checked SQL, **GORM** for Go web applications, and **SQLAlchemy** for Python teams wanting ORM convenience with SQL escape hatches — to build a persistence layer tailored to your language ecosystem, deployment target, and tolerance for abstraction.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- ORMs differ significantly in abstraction level, query control, and deployment characteristics. **Prisma leads in npm downloads (55.3M/month) but its engine binary adds 100-300ms to Lambda cold starts** — Prisma Accelerate moves the engine server-side for serverless . **Drizzle avoids cold starts entirely with zero binary dependency** and handles complex SQL that Prisma requires raw queries for . **MikroORM is the only mainstream TS ORM with Unit of Work + Identity Map + Data Mapper**, but its bundle size and class instantiation overhead make it harder for edge deployments . **TypeORM is actively maintained but not recommended for new projects** — development velocity has slowed and Prisma/Drizzle offer better type safety . **Several Node.js ORMs are effectively abandoned**: Bookshelf (no release in 6 years), Waterline (no commit since 2022), Objection (author stepped back in 2022) — do not start new projects on these . **ORMs are not always the answer** — jOOQ and MyBatis exist because abstraction leaks when you need database-specific features.
- Self-hosted open-source solutions require proper migration workflows (committed to version control alongside schema changes), connection pooling configuration for serverless, and awareness that N+1 queries can silently destroy performance if fetch strategies aren't understood.

---

**Made for backend engineers, database architects, and teams choosing persistence layers that match their language, deployment target, and SQL tolerance.**
Let's make object-relational mapping more open, type-safe, and workload-appropriate.
