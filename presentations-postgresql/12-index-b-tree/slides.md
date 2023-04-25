%title: Postgresql
%author: Richard


# INDEX : B-tree


<br>

* objectif : augmente la vitesse des requêtes

* index = table structurée pour un besoin

* index = pointeur

<br>
* attention : 
		* index = entretien (réindex)
		* index = baisse performance en écriture

<br>
* postgresql dispose de plusieurs types d'index :
		* b-tree (r-tree spatial)
		* hash
		* Gist
		* Gin
		* Brin

<br>

* création d'un index :

```
CREATE INDEX idx_schos ON SCHOSMIL USING HASH (t_champs1);
```

<br>
* B-Tree : cas d'utilisation : < <= = >= > 
		* table longue
		* champs de jointures
		* peu de valeurs rapatriées
		* éviter sur les tables mises à jour régulièrement

* complément : https://fr.wikipedia.org/wiki/Arbre_B

------------------------------------------------------------

# B-Tree

* balancing tree : arbre équilibré

* créé par Rudolf Bayer qui travaillait chez Boeing

<br>
* arbre inversé : tronc + branches + feuilles

* Principe : ex: 1 2 3 4 5 6 7 8 9 10

```
                        +---------------+
                        | +---+   +---+ |
                        | | 4 |   | 9 | |  clefs
                        | +---+   +---+ |
         +---------------------------------------------+
         |                      |                      |
         |                      |                      |
 +---------------+   +-----------------------+     +-------+
 | +---+   +---+ |   | +---+   +---+   +---+ |     | +---+ |
 | | 1 |   | 3 | |   | | 5 |   | 6 |   | 8 | |     | | 10| |
 | +---+   +---+ |   | +---+   +---+   +---+ |     | +---+ |
 +---------------+   +-----------------------+     +-------+
           |                           |
     +-------+                   +-------+
     | +---+ |                   | +---+ |
     | | 2 | |                   | | 7 | |
     | +---+ |                   | +---+ |
     +-------+                   +-------+

```

--------------------------------------------------------------

# Vérification

```
CREATE TABLE Schosmiel (id int);
INSERT INTO Schosmiel SELECT * FROM GENERATE_SERIES(1,2000000);
\timing
SELECT * FROM Schosmiel WHERE id = 1555555;
EXPLAIN ANALYZE select * from Schosmiel where id =1555555;
CREATE INDEX idx_xavier_id ON Schosmiel (id);
SELECT * FROM Schosmiel WHERE id = 1555555;
EXPLAIN ANALYZE select * from Schosmiel where id =1555555;
```
