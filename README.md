# datastack

Docker Compose setups for local database development.

## Services

| Service | Image | Port |
|---|---|---|
| MySQL 9.7 | `mysql:9.7` | 3306 |
| SQL Server 2022 | `mcr.microsoft.com/mssql/server:2022-CU25-ubuntu-22.04` | 1433 |
| Oracle Free | `gvenzl/oracle-free:latest` | 1521 |

## Usage

```sh
# copy env files and set your passwords
cp mysql/.env.example mysql/.env
cp sqlserver/.env.example sqlserver/.env
cp oracle/.env.example oracle/.env

# start a database
docker compose -f mysql/compose.yml up -d
docker compose -f sqlserver/compose.yml up -d
docker compose --env-file oracle/.env -f oracle/compose.yml up -d

# check status
docker ps
```

## Connecting

**MySQL**
```sh
mysql -h 127.0.0.1 -P 3306 -u appuser -p
```

**SQL Server**
```sh
sqlcmd -S 127.0.0.1,1433 -U sa -P "your_password" -C
```

**Oracle**
```sh
sqlplus system/your_password@//127.0.0.1:1521/FREEPDB1
```

The Oracle database and application user are initialized only on the first
startup. To initialize them again, remove the `oracle_data` volume:

```sh
docker compose --env-file oracle/.env -f oracle/compose.yml down -v
```

## License

MIT License, see [LICENSE](LICENSE).
