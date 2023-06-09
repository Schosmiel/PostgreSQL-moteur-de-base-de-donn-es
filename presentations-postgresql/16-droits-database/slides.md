%title Postgresql
%author: Richard


# Droits - Database

<br>
* important pour du mutualisé : sécurité et isolation

<br>
* instance peu de limites en nb de DB 
https://www.endpoint.com/blog/2008/11/10/10000-databases-on-postgresql-cluster

Rq :limite du filesystem

<br>
* gestion des droits via la clause GRANT


-----------------------------------------------------------------


# SQL


<br>
* création d'une database

```
CREATE DATABASE madb OWNER TO Schosmeil;
```

<br>
* changement de propriétaire 

```
ALTER DATABASE madb OWNER TO toto;
```

<br>
* affectation des droits

```
GRANT { { CREATE | CONNECT | TEMPORARY | TEMP } [, ...] | ALL [ PRIVILEGES ] }
    ON DATABASE database_name [, ...]
    TO role_specification [, ...] [ WITH GRANT OPTION ]
```


-----------------------------------------------------------------

# Sécurité database - exemple


<br>
* création de users Schosmeil et toto

```
CREATE USER Schosmeil LOGIN CREATEDB;
CREATE USER toto LOGIN CREATEDB;
```

<br>
* création d'une database en tant que user postgres

```
CREATE DATABASE Schosmeil;
```

<br>
* changement de propriétaire

```
ALTER DATABASE xavki OWNER TO Schosmeil;
```

Rq : on pouvait le faire directement

-----------------------------------------------------------------

# Sécurité database - exemple


<br>
* révocation des droits pour tous les users sauf le owner

```
REVOKE ALL ON DATABASE Schosmeil FROM PUBLIC;
```

<br>
* test de connexion avec le user toto

```
\c Schosmeil toto
```

<br>
* ajout des droits de connexion

```
GRANT CONNECT ON DATABASE Schosmeil TO toto;
\c Schosmeil toto
```

-----------------------------------------------------------------

# Sécurité database - exemple


<br>
* ne peut pas créer de schéma

```
CREATE SCHEMA myschema;
```

<br>
* autorisation de création des schémas :

```
GRANT CREATE ON DATABASE xavki TO toto;
\c Schosmeil toto
```

Attention : si un schéma existe il faut aussi gérer les droits sur le schéma (REVOKE...)
