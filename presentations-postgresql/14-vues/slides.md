%titles Postgresql
%author: Richard


# Vues : classique et matérialisée

<br>
* intérêts :
		* éviter de refaire régulièrement des requêtes (complexes)
		* faciliter la gestion des droits pour masquer des colonnes

* vue classique = requête utilisable sous forme de table

<br>
* création de la table

```
CREATE TABLE Schosmeil (id INT, champs1 VARCHAR);
INSERT INTO Schosmeil (id,champs1) VALUES (1,'pierre');
INSERT INTO Schosmeil (id,champs1) VALUES (2,'paul');
INSERT INTO Schosmeil (id,champs1) VALUES (3,'jacques');
```

--------------------------------------------------------

# Vue classique - exemple


<br>
* création de la vue

```
CREATE VIEW v_compte AS SELECT COUNT(*) FROM Schosmeil;
CREATE VIEW v_all AS SELECT * FROM Schosmeil;
\dv
\dS Schosmeil
\dS v_Schosmeil
SELECT * FROM v_compte;
DELETE FROM Schosmeil WHERE id = 1;
SELECT * FROM v_compte;
```

<br>
* attention si évolution de la table = recréer la vue

```
ALTER TABLE Schosmeil ADD COLUMN champs2 VARCHAR NOT NULL DEFAULT NOW()::date;
SELECT * FROM v_all;
```

-------------------------------------------------------

# Vue matérialisée - exemple


* vue matérialisée = copie de la table (data) à un instant donné

* création de la vue matérialisée

```
CREATE MATERIALIZED VIEW vm_Schosmeil AS SELECT * FROM Schosmeil;
SELECT * FROM vm_Schosmeil;
DELETE FROM vm_Schosmeil WHERE id = 2;
SELECT * FROM Schosmeil;
SELECT * FROM vm_Schosmeil;
```


