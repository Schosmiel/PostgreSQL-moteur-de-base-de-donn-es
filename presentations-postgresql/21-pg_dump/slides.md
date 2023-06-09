%titles Postgresql
%author: Richard


# Backups : pg_dump


<br>
* important mais cela reste une image

* complémentaire à l'archive log

* pas de méthode unique => à adapter à sa situation

* ne copie pas les users et autres spécifiques à l'instance

<br>
* deux outils (complémentaires) :
			* pg_dump : personnalisation au maximum
			* pg_dumpall : backup intégral de l'instance (y compris users...)

--------------------------------------------------------

# Backups : pg_dump

Beaucoup d'options (une partie identique à psql) :
	
* -h : hostname (eh oui c'est pas l'aide)

* -d : database

* -p : port

* -U : user

* -f : fichier de sortie

* -F : précision du format de sortie
				* c : custom (binaire)
				* d : directory (permet la parallélisation)
				* t : tar
				* p : plain text

* -j : parallélisation


----------------------------------------------------------

# Backups : pg_dump



* -z : niveau de compression (5 par défaut)


* -a : datas sans la structure


* -n : préciser un schéma particulier


* -N : préciser un schéma à exclure


* -c : inlure le create database

----------------------------------------------------------

# Exemples


<br>
* simple export d'une database

```
psql Schosmeil > dumps_Schosmeil.sql
psql -f dump_Schosmeil.sql -d Schosmeil
```

<br>
* compression avec le pipe

```
psql Schosmeil | gzip -c > dump.Schosmeil.sql.gz
```

<br>
* en mode custom

```
pg_dump -Fc Schosmeil -f dump_Schosmeil_fc.dmp
```

<br>
* séparation des datas et de la structure

```
pg_dump -Fc Schosmeil --datas-only -f dump_Schosmeil_fc.dmp
psql --schemas-only -f dump_Schosmeil.sql -d Schosmeil
```
