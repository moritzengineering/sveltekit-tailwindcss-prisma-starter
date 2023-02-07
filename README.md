# Sveltekit, Tailwind CSS & Prisma Starter

## Install

```sh
git clone https://github.com/zianwar/sveltekit-tailwindcss-prisma-starter myapp

cd myapp
pnpm i
```

```sh
cp .env.example .env
```

## Setup database

### Use [PlanetScale](https://planetscale.com/) (MySQL)

1. [schema.prisma](./prisma/schema.prisma) is already configured to use this method, to keep it, create a database on PlanetScale and copy the credentials into local `.env` file.

### Use SQLite

1. Local `.env` should already be using MySQL file.
2. Update Prisma [schema.prisma](./prisma/schema.prisma) to use SQLite:

   ```diff
   datasource db {
   - provider = "sqlite"
   + provider = "mysql"
   url = env("DATABASE_URL")
   + relationMode = "prisma"
   }
   ```

3. Create database and generate Prisma client
   ```sh
   npx prisma db push
   ```
