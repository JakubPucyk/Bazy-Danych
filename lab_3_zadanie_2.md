Zadanie 1
```sql
SELECT dzial.nazwa, MIN(pracownik.pensja), MAX(pracownik.pensja), AVG(pracownik.pensja)
FROM pracownik 
INNER JOIN dzial ON pracownik.dzial = dzial.id_dzialu
GROUP BY dzial.id_dzialu;
```
Zadanie 2
```sql
SELECT klient.pelna_nazwa, SUM(pozycja_zamowienia.ilosc * pozycja_zamowienia.cena) AS wartosc
FROM klient 
JOIN zamowienie ON klient.id_klienta = zamowienie.klient 
JOIN pozycja_zamowienia ON zamowienie.id_zamowienia = pozycja_zamowienia.zamowienie 
GROUP BY klient.id_klienta 
ORDER BY wartosc DESC LIMIT 10;
```

Zadanie 3
```sql
SELECT DISTINCT klient.pelna_nazwa, zamowienie.klient
FORM klient 
LEFT JOIN zamowienie on klient.id_klienta = zamowienie.klient
where zamowienie.klient IS NULL;
```

Zadanie 4
```sql
SELECT COUNT(zamowienie.id_zamowienia), SUM(pozycja_zamowienia.ilosc * pozycja_zamowienia.cena) AS wartosc
FROM zamowienie 
JOIN pozycja_zamowienia ON zamowienie.id_zamowienia = pozycja_zamowienia.zamowienie 
JOIN status_zamowienia ON zamowienie.status_zamowienia = status_zamowienia.id_statusu_zamowienia 
WHERE status_zamowienia.nazwa_statusu_zamowienia = 'anulowane';
```

Zadanie 5
```sql
SELECT adres_klienta.miejscowosc, COUNT(zamowienie.id_zamowienia) AS ilosc_zamowien, SUM(pozycja_zamowiosc * pozycja_zamowienia.cena) AS wartosc
FROM adres_klienta 
JOIN klient ON adres_klienta.klient = klient.id_klienta 
JOIN zamowienie ON klient.id_klienta = zamowienie.klient 
JOIN pozycja_zamowienia ON zamowienie.id_zamowienia = pozycja_zamowienia.zamowienie 
GROUP BY adres_klienta.miejscowosc;
```

Zadanie 6
```sql
SELECT SUM(pozycja_zamowienia.ilosc * pozycja_zamowienia.cena) AS wartosc
FROM pozycja_zamowienia 
JOIN zamowienie ON pozycja_zamowienia.zamowienie = zamowienie.id_zamowienia 
JOIN status_zamowienia ON zamowienie.status_zamowienia = status_zamowienia.id_statusu_zamowienia 
WHERE status_zamowienia.nazwa_statusu_zamowienia = 'zrealizowane';
```

Zadanie 7
```sql
SELECT YEAR(zamowienie.data_zamowienia) AS rok, (SUM(pozycja_zamowienia.ilosc * pozycja_zamowienia.cena) - SUM(towar.cena_zakupu * pozycja_zamowienia.ilosc))
JOIN pozycja_zamowienia ON zamowienie.id_zamowienia = pozycja_zamowienia.zamowienie 
JOIN towar ON pozycja_zamowienia.towar = towar.id_towaru 
GROUP BY rok;
```

Zadanie 8
```sql
SELECT kategoria.nazwa_kategori, SUM(towar.cena_zakupu * stan_magazynowy.ilosc) AS wartosc
FROM kategoria 
JOIN towar ON kategoria.id_kategori = towar.kategoria 
JOIN stan_magazynowy ON towar.id_towaru = stan_magazynowy.towar 
GROUP BY kategoria.id_kategori;
```
