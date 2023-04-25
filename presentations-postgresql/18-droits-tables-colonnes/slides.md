%titles Postgresql
%author: Richard

# Droits - tables et colonnes


<br>
* limitation pour les tables :
			* SELECT : sélection
			* INSERT : insertion de lignes
			* UPDATE : mise àjour de lignes
			* DELETE : suppression de lignes
			* TRUNCATE : vidéer la table
			* REFERENCES : utilisation de la table comme clef
			* TRIGGER : mise en place de déclencheurs
			* ALL

<br>
* syntax

```
GRANT ALL ON TABLE tbl1 TO <role_ou_public>;
REVOKE ALL ON TABLE tbl1 FROM <role_ou_public>;
```

----------------------------------------------------------------

# Droits - tables et colonnes


* exemple

```
\c Schosmeil Schos
CREATE TABLE tbl1 (id int,champs1 varchar);
INSERT INTO tbl1 VALUES (1, 'hello');
INSERT INTO tbl1 VALUES (2, 'world');
REVOKE ALL ON TABLE tbl1 FROM toto;
\c Schosmeil toto
INSERT INTO tbl1 VALUES (3, 'les Schosmeil !!!');
\c Schosmeil Schos
GRANT INSERT ON TABLE tbl1 TO Schos;
\c Schosmeil toto
INSERT INTO tbl1 (3, 'les Schosmeil !!!');
```

----------------------------------------------------------------


# Droits - tables et colonnes


<br>
* même principe pour les colonnes/champs de tables

* limitations possibles :
			* SELECT
			* INSERT
			* UPDATE
			* REFERENCES

<br>
* exemple

```
\c Schosmeil toto
SELECT * FROM tbl1;
\c Schosmeil Schos
REVOKE ALL ON TABLE tbl1 FROM toto;
GRANT SELECT(champs1) ON TABLE tbl1 to toto;
\c Schosmeil toto
SELECT * FROM tbl1;
```

