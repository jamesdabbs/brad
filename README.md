# Instructions

### Install Ansible

E.g.

```
$ virtualenv .env
$ source .env/bin/activate
$ pip install ansible
```

### Configure

Configuration _should_ be localized inside `config.yml` and ensuring that the target machine is listed in `hosts` as a `server`.

### Running

If you're using the included `Vagrantfile`, run `vagrant up server`.

If not, ensure your `hosts` and `config.yml` files look reasonable and then:

```
$ ansible-playbook server.yml
```

## TODO

* Verify backup job structure
* Setup monit
* Setup mailserver (for e.g. monit notifications)
* No rdoc on gem installs

### Other Notes

**Backups / Data Export**

Getting data out of Heroku and into Keter was a bit convoluted since both make some strong assumptions about your setup. Ultimately, I ended up:

* Exporting from Heroku
* Loading into a local database as usual
* Exporting _that_ database using `pg_dump --data-only -d ... > latest.pg_dump`
* Deleting vestigial tables (users, versions, schema_migrations)
* Spinning up the Yesod app and letting it create the desired schema
* Noting the created database name
* Loading the data dump using `sudo -u postgres psql [db_name] < latest.pg_dump`

Hopefully this won't be necessary in the future.
