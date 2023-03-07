## Installation
```bash
sudo apt install postgresql postgresql-contrib
```

Ensure that service is started:
```bash
sudo systemctl start postgresql.service
```

## Creating a new user:
```sql
psql -U postgres -c "CREATE USER new_user CREATEDB PASSWORD 'my_password'"

```

### Creating a new project db:

```bash
createdb [db_name] --owner=[postgers_user]
```

### Exporting a database

```
 $ pg_dump -Fc [db_name] > [filename].[archive_format]
```

### Importing a database
```bash
pg_restore -U [postgres_user] --dbname=[db_name] --format=[archive_format]
```
`--format` options: 

 - `d` / `directory`
 - `t` / `tar`
 - `c` / `custom` format.