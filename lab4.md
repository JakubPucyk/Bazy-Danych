Zadanie 1
```sql
CREATE TABLE postac(id_postaci INT PRIMARY KEY AUTO_INCREMENT,
  nazwa VARCHAR(40),
  rodzaj ENUM('wiking', 'ptak', 'kobieta'),
  data_ur DATE,
  wiek INT UNSIGNED);
DESC postac;
```
```sql
INSERT INTO postac VALUES (NULL, 'Bjorn', 'wiking', '1623-11-22', 23),
(NULL, 'Drozd', 'ptak', '1640-04-21', 2),
(NULL, 'Tesciowa', 'kobieta', '1490-01-01', 133);
SELECT * FROM postac;
```
```sql
UPDATE postac SET wiek = 88 WHERE nazwa = 'Tesciowa';
SELECT * FROM postac;
```
Zadanie 2 
```sql
CREATE TABLE walizka(id_walizki INT PRIMARY KEY AUTO_INCREMENT,
  pojemnosc INT UNSIGNED,
  kolor ENUM('rozowy', 'czerwony', 'teczowy', 'zolty'),
  id_wlasciciela INT,
  FOREIGN KEY(id_wlasciciela) REFERENCES postac(id_postaci) ON DELETE CASCADE);
DESC walizka;
```
```sql
ALTER TABLE walizka
ALTER COLUMN kolor
SET DEFAULT 'rozowy';
DESC walizka
```
```sql
INSERT INTO walizka VALUES (NULL, 30, 'czerwony', 1);
INSERT INTO walizka(pojemnosc, id_wlasciciela) VALUES (50, 3);
SELECT * FROM walizka
```
Zadanie 3
```sql
CREATE TABLE izba(adres_budynku VARCHAR(255),
  nazwa_izby VARCHAR(255),
  metraz INT UNSIGNED,
  wlasciciel INT,
  PRIMARY KEY(adres_budynku, nazwa_izby),
  FOREIGN KEY (wlasciciel) REFERENCES postac(id_postaci) ON DELETE SET NULL);
DESC izba;
```
```sql
ALTER TABLE izba ADD kolor_izby VARCHAR(255) DEFAULT 'czarny' AFTER metraz;
DESC izba;
```
```sql
INSERT INTO izba(adres_budynku, nazwa_izby) VALUES ('Koln 33, Jogurand', 'spizarnia');
SELECT * FROM izba;
```
Zadanie 4
```sql
CREATE TABLE przetwory(
  id_przetworu INT PRIMARY KEY AUTO_INCREMENT,
  rok_produkcji INT DEFAULT 1654,
  id_wykonawcy INT,
  zawartosc VARCHAR(255),
  dodatek VARCHAR(255) DEFAULT 'papryczka chilli',
  id_konsumenta INT,
  FOREIGN KEY (id_wykonawcy) REFERENCES postac(id_postaci),
  FOREIGN KEY (id_konsumenta) REFERENCES postac(id_postaci));
```
```sql
INSERT INTO przetwory(id_wykonawcy, zawartosc, id_konsumenta) VALUES (1, 'bigos', 3);
SELECT * FROM przetwory;
```
Zadanie 5
```sql
INSERT INTO postac(nazwa, rodzaj, data_ur, wiek) VALUES
('Tyr Tyreusz', 'wiking', '1611-10-16', 29),
('Ares Mars', 'wiking', '1601-05-15', 24),
('Uwe Nebbro', 'wiking', '1622-03-20', 25),
('Ivan Ivanowic', 'wiking', '1603-11-10', 23),
('Ural Moskwa', 'wiking', '1607-07-05', 33);
```
```sql
CREATE TABLE statek(
  nazwa_statku VARCHAR(255) PRIMARY KEY,
  rodzaj_statku ENUM('Transportowy', 'Handlowy', 'Tratwa', 'Wojenny', 'Kajak'),
  data_wodowanie DATE,
  max_ladownosc INT UNSIGNED);
```
```sql
INSERT INTO statek (nazwa_statku, rodzaj_statku, data_wodowanie, max_ladownosc) VALUES
('Bismarck', 'wojenny', '1640-01-15', 100),
('Agir', 'handlowy', '1640-01-16', 400);
```
```sql
ALTER TABLE postac
  ADD funkcja VARCHAR(255);
DESC postac;
```
```sql
UPDATE postac SET funkcja = 'kapitan' WHERE nazwa = 'Bjorn';
SELECT * FROM postac;
```
```sql
ALTER TABLE postac
  ADD statek VARCHAR(255);
ALTER TABLE postac
  ADD FOREIGN KEY (statek) REFERENCES statek(nazwa_statku);
```
```sql
UPDATE postac SET statek = 'Bismarck' WHERE id_postaci IN (1,2,5,7);
UPDATE postac SET statek = 'Agir' WHERE id_postaci IN (4,6,8);
SELECT * FROM postac;
```
```sql
DELETE FROM izba WHERE nazwa_izby = 'spizarnia';
DROP TABLE izba;
SHOW TABLES;
```
