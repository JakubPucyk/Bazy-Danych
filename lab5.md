Zadanie 1
```sql
DELETE FROM postac WHERE nazwa <> 'Bjorn' AND rodzaj = 'wiking' ORDER BY wiek DESC LIMIT 2;

ALTER TABLE walizka DROP CONSTRAINT walizka_ibfk_1;
ALTER TABLE przetwory DROP CONSTRAINT przetwory_ibfk_1;
ALTER TABLE przetwory DROP CONSTRAINT przetwory_ibfk_2;
ALTER TABLE postac MODIFY id_postaci INT;
ALTER TABLE postac DROP PRIMARY KEY;
```

Zadanie 2
```sql
ALTER TABLE postac ADD pesel CHAR(11) FIRST;

UPDATE postac SET pesel = '12345678901' + id_postaci;

ALTER TABLE postac ADD PRIMARY KEY(pesel);

ALTER TABLE postac MODIFY rodzaj ENUM('wiking', 'ptak', 'kobieta', 'syrena');

INSERT INTO postac VALUES ('90112345678', 9, 'Gertruda Nieszczera', 'syrena', '1003-09-09', 145, NULL, NULL);
```
Zadanie 3
```sql
UPDATE postac SET statek = 'Bismarck' WHERE nazwa LIKE '%a%';

SELECT * FROM statek WHERE data_wodowanie BETWEEN '1901-01-01' AND '2000-12-31';

UPDATE statek SET max_ladownosc = 0.7 * max_ladownosc 
WHERE YEAR(data_wodowanie) BETWEEN 1901 AND 2000;

ALTER TABLE postac 
MODIFY wiek INT UNSIGNED CHECK (wiek < 1000);

```
Zadanie 4
```sql
ALTER TABLE postac MODIFY rodzaj ENUM('wiking', 'ptak', 'kobieta', 'syrena', 'waz');

INSERT INTO postac VALUES('89012345678', 10, 'Loko', 'waz', '1144-07-14', 23, NULL, NULL);

CREATE TABLE marynarz LIKE postac;

ALTER TABLE marynarz 
ADD FOREIGN KEY (statek) REFERENCES statek(nazwa_statku);

INSERT INTO marynarz 
SELECT * FROM postac WHERE statek IS NOT NULL;
```
Zadanie 5
```sql
UPDATE postac SET statek = NULL;

DELETE FROM postac WHERE rodzaj = 'wiking' AND id_postaci = 8;

TRUNCATE statek;

DROP TABLE statek;

CREATE TABLE zwierz(id INT AUTO_INCREMENT PRIMARY KEY,
  nazwa VARCHAR(100),
  wiek INT);

INSERT INTO zwierz(nazwa, wiek) SELECT nazwa, wiek FROM postac WHERE rodzaj IN ('ptak', 'waz');
```
