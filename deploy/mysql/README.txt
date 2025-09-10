MySQL on Fly.io for Ghost

App: prosora-mysql

Initial setup:
- fly apps create prosora-mysql
- fly launch --no-deploy (or copy deploy/mysql/fly.toml to app)
- fly volumes create mysql_data -a prosora-mysql -r iad -s 10
- fly secrets set MYSQL_PASSWORD=... MYSQL_ROOT_PASSWORD=... -a prosora-mysql
- fly deploy -a prosora-mysql

Notes:
- MySQL will only be reachable inside Fly private network (.internal domain)
- Connect using host prosora-mysql.internal, user ghost, db ghost, password from secret