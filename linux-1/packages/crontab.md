# crontab

\# Edit this file to introduce tasks to be run by cron.

\#

\# For example, you can run a backup of all your user accounts

\# at 5 a.m every week with:

\# 0 5 \* \* 1 tar -zcf /var/backups/home.tgz /home/

\#

\# For more information see the manual pages of crontab(5) and cron(8)

\#

\# m h dom mon dow command

\#

00 \* \* \* \* cd /home/directory && command args > /dev/null

* Use **&&** to chain commands
* Use **cd** to change directories, and use the system absolute path.
* **/dev/null** is supposed to block sends to **mail**, but so far it keeps doing it.
