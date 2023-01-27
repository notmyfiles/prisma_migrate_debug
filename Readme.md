Debug repository for https://github.com/prisma/prisma/issues/17558

# System

- Windows 10

# Steps

- Follow [quickstart](https://www.prisma.io/docs/getting-started/quickstart) guide steps 1-3:
  - ```
    npm install typescript ts-node @types/node --save-dev
    npm init -y
    npx tsc --init
    npm install prisma --save-dev
    npx prisma init --datasource-provider sqlite
    ```
  - Copy prisma schema
  - ```
    npx prisma migrate dev --name init
    ```
- Delete migrations folder (simulate adding to existing project)
- Follow [quickstart for existing projects](https://www.prisma.io/docs/getting-started/setup-prisma/add-to-existing-project/relational-databases/baseline-your-database-typescript-postgres) guide step "baseline your database":

  - ```
    mkdir -p prisma/migrations/0_init
    npx prisma migrate diff --from-empty --to-schema-datamodel prisma/schema.prisma --script > prisma/migrations/0_init/migration.sql
    ```
  - Observe the error with the last command `npx prisma migrate resolve --applied 0_init`:

    ```
    PS> npx prisma migrate resolve --applied 0_init
    Environment variables loaded from .env
    Prisma schema loaded from prisma\schema.prisma
    Datasource "db": SQLite database "dev.db" at "file:./dev.db"
    Error: P3017

    The migration 0_init could not be found. Please make sure that the migration exists, and that you included the whole name of the directory. (example: "20201207184859_initial_migration")
    ```
