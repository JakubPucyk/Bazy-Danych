Zadanie 1
```sql
SELECT imie, nazwisko, YEAR(data_urodzenia) 
FROM pracownik
```
Zadanie 2
```sql
SELECT imie, nazwisko, YEAR(now()) - YEAR(data_urodzenia) as wiek 
FROM pracownik
```
Zadanie 3
```sql
SELECT dzial.nazwa, COUNT(pracownik.id_pracownika)
FROM dzial 
JOIN pracownik ON dzial.id_dzialu = pracownik.dzial
GROUP BY dzial.id_dzialu;
```
Zadanie 4
```sql
SELECT kategoria.nazwa_kategori, count(towar.id_towaru) as ilosc
FROM kategoria
JOIN towar ON kategoria.id_kategori = towar.kategoria 
GROUP BY kategoria.nazwa_kategori
```
Zadanie 5
```sql
SELECT kategoria.nazwa_kategori, group_concat(towar.nazwa_towaru,"") as nazwy_produktow
FROM kategoria, towar
WHERE kategoria.id_kategori = towar.kategoria
GROUP BY kategoria.id_kategori
```
Zadanie 6
```sql
SELECT ROUND(AVG(pensja), 2) FROM pracownik;
```
Zadanie 7
```sql
SELECT ROUND(AVG(pensja), 2)
FROM pracownik
WHERE data_zatrudnienia <= '2019-01-11';

SELECT ROUND(AVG(pensja), 2)
FROM pracownik
WHERE data_zatrudnienia <= 
SUBDATE(data_zatrudnienia, interval 5 year);
```
Zadanie 8
```sql
SELECT towar.nazwa_towaru, COUNT(pozycja_zamowienia.towar)
FROM towar 
JOIN pozycja_zamowienia ON towar.id_towaru = pozycja_zamowienia.towar 
GROUP BY pozycja_zamowienia.towar
ORDER BY count(pozycja_zamowienia.towar) DESC LIMIT 10;
```
Zadanie 9
```sql
SELECT zamowienie.id_zamowienia, zamowienie.numer_zamowienia, SUM(pozycja_zamowienia.ilosc * pozycja_zamowienia.cena)
FROM zamowienie 
JOIN pozycja_zamowienia ON zamowienie.id_zamowienia = pozycja_zamowienia.zamowienie 
WHERE quarter(zamowienie.data_zamowienia) = 1 and year(zamowienie.data_zamowienia) = 2017
GROUP BY zamowienie.id_zamowienia;
```
Zadanie 10
```sql
SELECT pracownik.imie, pracownik.nazwisko, SUM(pozycja_zamowienia.ilosc * pozycja_zamowienia.cena) AS wartosc
FROM zamowienie 
INNER JOIN pozycja_zamowienia on zamowienie.id_zamowienia = pozycja_zamowienia.zamowienie
INNER JOIN pracownik on pracownik.id_pracownika = zamowienie.pracownik_id_pracownika
GROUP BY pracownik.id_pracownika
ORDER BY wartosc DESC
```
