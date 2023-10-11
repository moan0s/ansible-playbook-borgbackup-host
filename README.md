# BorgBackup repository setup playbook

This is an [Ansible](https://www.ansible.com/) playbook which allows you to configure a borg-backup host reproduciably.

## Getting started

Create an file listing the repository host in `inventory/hosts`

```
[borgbackup_servers]
backup.example.org
```

Create the directory `ìnventory/<hostname>/` and then create `ìnventory/<hostname>/vars.yml`. In there you will configure your backup server, specifically which repositories should be created.

```yaml

# Adjust this if you want the repository to be hosted on a different path, e.g. on a mounted drive
# borgbackup_server_base_path: /home/borgbackup

borgbackup_server_auth_users:
  - host: host_1.example.org
    key: "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMOREPUBLICKEYINFO host_1"
  - host: host_2.example.org
    key: "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMOREPUBLICKEYINFO host_2"
```

Now deploy by running

```zsh
just install-all
```

In the end you only need to point your clients to the repositories. The repository should look like this

```
ssh://borgbackup@<hostname>/./
```
