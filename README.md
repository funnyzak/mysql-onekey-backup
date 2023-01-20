# MySQL OneKey Backup

[![GitHub license](https://img.shields.io/github/license/funnyzak/mysql-onekey-backup)](http://www.apache.org/licenses/LICENSE-2.0)
[![GitHub stars](https://img.shields.io/github/stars/funnyzak/mysql-onekey-backup)](https://github.com/funnyzak/mysql-onekey-backup/stargazers)
[![GitHub issues](https://img.shields.io/github/issues/funnyzak/mysql-onekey-backup)](https://github.com/funnyzak/mysql-onekey-backup/issues)
[![GitHub forks](https://img.shields.io/github/forks/funnyzak/mysql-onekey-backup)](https://github.com/funnyzak/mysql-onekey-backup/network/members)
[![Github Release](https://img.shields.io/github/release/funnyzak/mysql-onekey-backup)](https://github.com/funnyzak/mysql-onekey-backup/releases)

A shell script to backup mysql database and send message with pushoo.

## Features

- Backup all databases or specified databases.
- Push message with pushoo.
- Delete expired dump files.
- Support custom commands before and after the dump.
- Support custom mysqldump options.
- Support on CentOS 7+、Ubuntu 18.04+、Debian 9+.

## Requirements

You need to install the following software before using the script.

- mysqldump
- pushoo-cli
- nodejs 14+

You can install them with the following command.

```bash
# install mysqldump
bash /path/to/mysql_backup.sh do_install_mysql_client

# install pushoo-cli
bash /path/to/mysql_backup.sh do_install_pushoo_cli

# install nodejs 16
bash /path/to/mysql_backup.sh do_install_nodejs
```

Attention: `You need config pushoo-cli before use it.`

## Arguments

The script has 10 variables, you can set them in the script or pass them as arguments. following is the description of each variable.

- `dump_target_dir` - The directory where the dump file will be saved. Default: `/mnt/back/db_backups`. Required.
- `db_host` - The host of the database. Default: `127.0.0.1`. Required.
- `db_user` - The user of the database. Default: `root`. Required.
- `db_password` - The password of the database. Default is empty. Required.
- `db_names` - The names of the database. If set empty, all databases will be backed up. Required.
- `db_port` - The port of the database. Default: `3306`. Required.
- `dump_opts` - The options of the mysqldump command. Default: `--column-statistics=0 --ssl-mode=DISABLED --single-transaction --quick`. Optional.
- `expire_hours` - The dump file at the `specified directory` will be deleted after the specified number of hours. Default: `4320`. Optional.
- `before_dump_command` - The command to be executed before the dump. Default is empty. Optional.
- `after_dump_command` - The command to be executed after the dump. Default is empty. Optional.

for example:

```bash
bash mysql_backup.sh "dump_target_dir" "db_host" "db_user" "db_password" "db_names" db_port "dump_opts" expire_hours "before_dump_command" "after_dump_command"
```

## Usage

```bash
# backup "db1" and "db2" to "/mnt/back/db_backups" and the dump file will be deleted after 4320 hours.
bash /path/to/mysql_backup.sh "/mnt/back/db_backups" "127.0.0.1" "root" "examplepassword" "db1 db2" 3306 "--column-statistics=0 --ssl-mode=DISABLED --single-transaction --quick" 4320
# or
bash /path/to/mysql_backup.sh "/mnt/back/db_backups" "127.0.0.1" "root" "examplepassword" "db1 db2"

# backup "db1" and "db2" to "/mnt/back/db_backups" and the dump file will be deleted after 4320 hours. and log to /var/log/db_backup.log
bash /path/to/mysql_backup.sh "/mnt/back/db_backups" "127.0.0.1" "root" "examplepassword" "db1 db2" >> /var/log/db_backup.log 2>&1
```

## CronTab

You can use crontab to schedule the script to run periodically. For example, you can run the script every day at 3:00 AM.

```bash
0 3 * * * /path/to/mysql_backup.sh "/mnt/back/db_backups" "127.0.0.1" "root" "examplepassword" "db1 db2" >> /var/log/db_backup.log 2>&1
```

## Reference

- [MySQL Command Line Client Installation Instructions](https://dev.mysql.com/doc/refman/8.0/en/mysql-installation.html)
- [pushoo-cli](https://github.com/funnyzak/pushoo-cli) is a command line tool with Pushoo.js pushes multiple platform messages.
- [Pushoo.js](https://github.com/imaegoo/pushoo)

## Contribution

If you have any questions or suggestions, please feel free to submit an issue or pull request.

<a href="https://github.com/funnyzak/mysql-onekey-backup/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=funnyzak/mysql-onekey-backup" />
</a>

## License

MIT License © 2023 [funnyzak](https://github.com/funnyzak)
