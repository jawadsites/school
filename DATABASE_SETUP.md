# Database Setup Instructions (Alternative Method)

If `npx prisma migrate dev` doesn't work, use this method to set up the database.

## Option 1: Using Docker (Recommended)

1. **Start PostgreSQL container:**
   ```powershell
   docker compose up -d postgres
   ```

2. **Run the SQL file:**
   ```powershell
   Get-Content setup-database.sql | docker exec -i postgres psql -U arwaacademy -d arwaschool
   ```

3. **Generate Prisma Client:**
   ```powershell
   npx prisma generate
   ```

## Option 2: Using psql command line

1. **Make sure PostgreSQL is running:**
   ```powershell
   docker compose up -d postgres
   ```

2. **Run the SQL file:**
   ```powershell
   docker exec -i postgres psql -U arwaacademy -d arwaschool -f /tmp/setup.sql
   ```

   Or copy and paste the content of `setup-database.sql` into psql:
   ```powershell
   docker exec -it postgres psql -U arwaacademy -d arwaschool
   ```
   Then paste the entire content of `setup-database.sql` and press Enter.

3. **Generate Prisma Client:**
   ```powershell
   npx prisma generate
   ```

## Option 3: Using DBeaver or pgAdmin

1. Open DBeaver or pgAdmin
2. Connect to PostgreSQL:
   - Host: `localhost`
   - Port: `5432`
   - Database: `arwaschool`
   - Username: `arwaacademy`
   - Password: `arwa12345678`
3. Open and execute `setup-database.sql`
4. Run `npx prisma generate` in your terminal

## Verify Setup

Check if tables were created:
```powershell
docker exec -it postgres psql -U arwaacademy -d arwaschool -c "\dt"
```

You should see all the tables listed.

## Next Steps

After the database is set up, you can:

1. **Seed the database** (optional):
   ```powershell
   npx prisma db seed
   ```

2. **Start the development server:**
   ```powershell
   npm run dev
   ```

## Troubleshooting

If you get "relation already exists" errors, drop all tables first:
```powershell
docker exec -it postgres psql -U arwaacademy -d arwaschool -c "DROP SCHEMA public CASCADE; CREATE SCHEMA public;"
```

Then run the setup-database.sql file again.
