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

```
$ ansible-playbook server.yml
```
