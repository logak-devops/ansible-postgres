# ansible-postgres

Command to check :

```

  su - postgres
  psql -U user1 -h localhost -d app1
  
  ![image](https://user-images.githubusercontent.com/84037413/124477492-fe3cd100-dd9b-11eb-8a70-8a53b86a8386.png)

  psql -U user
  it connects via UNIX Socket, which by default uses peer authentication, unless specified in pg_hba.conf otherwise.

  You can specify:

  host    database             user             127.0.0.1/32       md5
  host    database             user             ::1/128            md5
  to get TCP/IP connection on loopback interface (both IPv4 and IPv6) for specified database and user.

  After changes you have to restart postgres or reload it's configuration. Restart that should work in modern RHEL/Debian based distros:

  service postgresql restart
  Reload should work in following way:

  pg_ctl reload
  but the command may differ depending of PATH configuration - you may have to specify absolute path, which may be different, depending on way the postgres was installed.

  Then you can use:

  psql -h localhost -U user -d database
  to login with that user to specified database over TCP/IP. md5 stands for encrypted password, while you can also specify password for plain text passwords during authorisation.   These 2 options shouldn't be of a great matter as long as database server is only locally accessible, with no network access.
  
  Important note: Definition order in pg_hba.conf matters - rules are read from top to bottom, like iptables, so you probably want to add proposed rules above the rule:

  host    all             all             127.0.0.1/32            ident

```
