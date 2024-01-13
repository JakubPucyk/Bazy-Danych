Zadanie 1

```sql
#przed wstawieniem
DELIMITER //
CREATE TRIGGER kreatura_before_insert
BEFORE INSERT ON kreatura
FOR EACH ROW
BEGIN
IF NEW.waga <= 0
THEN
SET NEW.waga = 1;
END IF;
END
//
DELIMITER ;

#przed modyfikacja
DELIMITER //
CREATE TRIGGER kreatura_before_update
BEFORE UPDATE ON kreatura
FOR EACH ROW
BEGIN
IF NEW.waga <= 0
THEN
SET NEW.waga = 1;
END IF;
END
//
DELIMITER ;
```

Zadanie 2
```sql
CREATE TABLE archiwum_wypraw LIKE wyprawa;
ALTER TABLE archiwum_wypraw MODIFY kierownik VARCHAR(200);

DELIMITER //
CREATE TRIGGER wyprawa_before_delete
BEFORE DELETE on wyprawa
FOR EACH ROW
BEGIN
INSERT INTO archiwum_wypraw SELECT * FROM wyprawa JOIN kreatura ON wyprawa.kierownik = kreatura.idKreatury WHERE wyprawa.id_wyprawy = OLD.id_wyprawy;
END
//
DELIMITER ;
```

Zadanie 3
```sql
DELIMITER $$
CREATE PROCEDURE eliksir_sily(IN id int)
BEGIN 
UPDATE kreatura SET udzwig = udzwig*1.2 WHERE idKreatury = id;
END
$$
DELIMITER ;
CALL eliksir_sily(1);

DELIMITER $$
CREATE FUNCTION powieksz_tekst(tekst VARCHAR(255)) 
RETURNS VARCHAR(255)
BEGIN 
DECLARE wynik VARCHAR(255);
SET wynik = UPPER(tekst);
RETURN wynik;
END
$$
DELIMITER ;
SELECT powieksz_tekst('hello world')
```
