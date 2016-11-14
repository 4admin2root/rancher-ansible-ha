### Rancher in HA - no database dump needed

Ansible 2 required

mysql service requires systemd.

the rest can be run on any os with bash and curl

You need 3, 5 server hosts running docker 1.10 +

Mysql db, or use docker container provided.

Agent nodes are not automated. Included a playbook that would allow you to copy paste the commands and run them on all hosts.

Caveats: you need to edit the system ssl and add your correct cert after the install this needs to be done on port 80.

happy to take pr for cert upload automation: https://github.com/andreimc/rancher-ha-auto

in global vars you have the following:

```
rancher_db_port: 3306
rancher_db_host: 172.16.222.1
rancher_db_name: cattle
rancher_db_user: rancher
rancher_db_pass: password

rancher_server_image: rancher/server
rancher_server_image_tag: v1.2.0-pre3
rancher_ha_url: rancher.example.com
```


To run this:

ansible-playbook playbook.yml -e @global_vars.yml
