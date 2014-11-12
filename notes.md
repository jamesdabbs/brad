# Backups / Data Export

Getting data out of Heroku and into Keter was a bit convoluted since both make some strong assumptions about your setup. Ultimately, I ended up:

* Exporting from Heroku
* Loading into a local database as usual
* Exporting _that_ database using `pg_dump --data-only -d ... > latest.pg_dump`
* Deleting vestigial tables (users, versions, schema_migrations)
* Spinning up the Yesod app and letting it create the desired schema
* Noting the created database name
* Loading the data dump using `sudo -u postgres psql [db_name] < latest.pg_dump`

Hopefully this won't be necessary in the future.
