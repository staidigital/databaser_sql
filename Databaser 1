# Komplett MariaDB Kurs

## Introduksjon

MariaDB er et populært open-source relasjonsdatabasesystem som er kompatibelt med MySQL. Dette kurset vil ta deg gjennom alt fra installasjon til grunnleggende databaseoperasjoner.

## 1. Installasjon med Homebrew

Homebrew er den enkleste måten å installere MariaDB på macOS.

### Installer MariaDB

```bash
brew install mariadb
```

### Start MariaDB-tjenesten

```bash
brew services start mariadb
```

For å stoppe tjenesten senere:

```bash
brew services stop mariadb
```

### Første gangs sikkerhetskonfigurasjon

Kjør sikkerhetsskriptet for å sette opp root-passord og fjerne testdatabaser:

```bash
mariadb-secure-installation
```

Følg instruksjonene på skjermen. Du vil bli bedt om å:
- Sette et root-passord
- Fjerne anonyme brukere
- Deaktivere ekstern root-tilgang
- Fjerne testdatabasen

## 2. Koble til MariaDB

### Koble til som root

```bash
mariadb -u root -p
```

Du vil bli bedt om å skrive inn passordet du opprettet under sikkerhetskonfigurasjonen.

### Koble til uten passord (hvis ikke satt opp)

```bash
mariadb -u root
```

## 3. Opprette ny bruker med rettigheter

### Opprette en ny bruker

```sql
CREATE USER 'brukernavn'@'localhost' IDENTIFIED BY 'sikker_passord';
```

Eksempel:

```sql
CREATE USER 'johndoe'@'localhost' IDENTIFIED BY 'MittPassord123!';
```

### Gi alle rettigheter til en bruker

```sql
GRANT ALL PRIVILEGES ON *.* TO 'brukernavn'@'localhost';
```

### Gi spesifikke rettigheter til en database

```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON database_navn.* TO 'brukernavn'@'localhost';
```

### Oppdatere rettighetene

Etter å ha gitt rettigheter, må du kjøre:

```sql
FLUSH PRIVILEGES;
```

### Vise brukerrettigheter

```sql
SHOW GRANTS FOR 'brukernavn'@'localhost';
```

### Eksempel på komplett brukeropprettelse

```sql
CREATE USER 'webapp'@'localhost' IDENTIFIED BY 'WebApp2024!';
GRANT ALL PRIVILEGES ON webshop.* TO 'webapp'@'localhost';
FLUSH PRIVILEGES;
```

## 4. Avslutte MariaDB

For å avslutte MariaDB-klienten, bruk en av følgende kommandoer:

```sql
EXIT;
```

eller

```sql
QUIT;
```

eller bare trykk `Ctrl + D`

## 5. Opprette en database

### Vise eksisterende databaser

```sql
SHOW DATABASES;
```

### Opprette en ny database

```sql
CREATE DATABASE database_navn;
```

Eksempel:

```sql
CREATE DATABASE webshop;
```

### Opprette database med tegnsett

```sql
CREATE DATABASE webshop CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

### Velge en database å jobbe med

```sql
USE database_navn;
```

Eksempel:

```sql
USE webshop;
```

### Slette en database

```sql
DROP DATABASE database_navn;
```

## 6. Opprette tabeller

### Grunnleggende tabellopprettelse

```sql
CREATE TABLE tabell_navn (
    kolonne1 datatype,
    kolonne2 datatype,
    kolonne3 datatype
);
```

### Eksempel: Opprette en kundetabell

```sql
CREATE TABLE kunder (
    kunde_id INT AUTO_INCREMENT PRIMARY KEY,
    fornavn VARCHAR(50) NOT NULL,
    etternavn VARCHAR(50) NOT NULL,
    epost VARCHAR(100) UNIQUE,
    telefon VARCHAR(20),
    registrert_dato TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Forklaring av datatyper

- `INT`: Heltall
- `VARCHAR(n)`: Tekst med maksimal lengde n
- `TEXT`: Lengre tekst
- `DATE`: Dato (YYYY-MM-DD)
- `TIMESTAMP`: Dato og tid
- `DECIMAL(p,s)`: Desimaltall (p=totalt antall sifre, s=desimaler)
- `BOOLEAN`: Sant/usant verdi

### Eksempel: Opprette en produkttabell

```sql
CREATE TABLE produkter (
    produkt_id INT AUTO_INCREMENT PRIMARY KEY,
    produkt_navn VARCHAR(100) NOT NULL,
    beskrivelse TEXT,
    pris DECIMAL(10, 2) NOT NULL,
    lager_antall INT DEFAULT 0,
    kategori VARCHAR(50)
);
```

### Vise tabeller i databasen

```sql
SHOW TABLES;
```

### Vise tabellstruktur

```sql
DESCRIBE tabell_navn;
```

eller

```sql
SHOW COLUMNS FROM tabell_navn;
```

## 7. INSERT - Sette inn data

### Sette inn én rad

```sql
INSERT INTO tabell_navn (kolonne1, kolonne2, kolonne3)
VALUES (verdi1, verdi2, verdi3);
```

### Eksempel: Sette inn kunde

```sql
INSERT INTO kunder (fornavn, etternavn, epost, telefon)
VALUES ('Ola', 'Nordmann', 'ola@example.com', '12345678');
```

### Sette inn flere rader samtidig

```sql
INSERT INTO produkter (produkt_navn, beskrivelse, pris, lager_antall, kategori)
VALUES 
    ('Laptop', 'Kraftig bærbar PC', 12999.00, 15, 'Elektronikk'),
    ('Mus', 'Trådløs mus', 299.00, 50, 'Tilbehør'),
    ('Tastatur', 'Mekanisk tastatur', 899.00, 30, 'Tilbehør');
```

### Sette inn uten å spesifisere kolonnenavn

Hvis du setter inn verdier for alle kolonner i riktig rekkefølge:

```sql
INSERT INTO kunder VALUES (NULL, 'Kari', 'Hansen', 'kari@example.com', '87654321', NOW());
```

## 8. SELECT - Hente data

### Hente alle rader og kolonner

```sql
SELECT * FROM tabell_navn;
```

Eksempel:

```sql
SELECT * FROM kunder;
```

### Hente spesifikke kolonner

```sql
SELECT kolonne1, kolonne2 FROM tabell_navn;
```

Eksempel:

```sql
SELECT fornavn, etternavn, epost FROM kunder;
```

### Begrense antall resultater

```sql
SELECT * FROM produkter LIMIT 5;
```

### Sortere resultater

Stigende rekkefølge (standard):

```sql
SELECT * FROM produkter ORDER BY pris;
```

Synkende rekkefølge:

```sql
SELECT * FROM produkter ORDER BY pris DESC;
```

### Unike verdier

```sql
SELECT DISTINCT kategori FROM produkter;
```

## 9. WHERE - Filtrere data

### Grunnleggende WHERE-klausul

```sql
SELECT * FROM tabell_navn WHERE betingelse;
```

### Eksempler med ulike operatorer

#### Likhet

```sql
SELECT * FROM produkter WHERE kategori = 'Elektronikk';
```

#### Ulikhet

```sql
SELECT * FROM produkter WHERE kategori != 'Tilbehør';
```

eller

```sql
SELECT * FROM produkter WHERE kategori <> 'Tilbehør';
```

#### Større enn / mindre enn

```sql
SELECT * FROM produkter WHERE pris > 1000;
SELECT * FROM produkter WHERE lager_antall <= 20;
```

#### BETWEEN - Verdier mellom to grenser

```sql
SELECT * FROM produkter WHERE pris BETWEEN 500 AND 2000;
```

#### IN - Flere mulige verdier

```sql
SELECT * FROM kunder WHERE fornavn IN ('Ola', 'Kari', 'Per');
```

#### LIKE - Mønstermatching

Finn kunder med fornavn som starter med 'O':

```sql
SELECT * FROM kunder WHERE fornavn LIKE 'O%';
```

Finn produkter med 'mus' i navnet (case-insensitive):

```sql
SELECT * FROM produkter WHERE produkt_navn LIKE '%mus%';
```

Wildcards:
- `%` matcher null eller flere tegn
- `_` matcher nøyaktig ett tegn

#### IS NULL / IS NOT NULL

```sql
SELECT * FROM kunder WHERE telefon IS NULL;
SELECT * FROM kunder WHERE epost IS NOT NULL;
```

### Kombinere betingelser

#### AND - Begge betingelser må være sanne

```sql
SELECT * FROM produkter 
WHERE kategori = 'Elektronikk' AND pris < 5000;
```

#### OR - Minst én betingelse må være sann

```sql
SELECT * FROM produkter 
WHERE kategori = 'Elektronikk' OR kategori = 'Tilbehør';
```

#### Kombinere AND og OR

```sql
SELECT * FROM produkter 
WHERE (kategori = 'Elektronikk' OR kategori = 'Datautstyr') 
AND pris > 1000;
```

### NOT - Negering

```sql
SELECT * FROM produkter WHERE NOT kategori = 'Tilbehør';
```

## Praktiske øvelser

### Øvelse 1: Sett opp database

```sql
CREATE DATABASE butikk;
USE butikk;

CREATE TABLE ansatte (
    ansatt_id INT AUTO_INCREMENT PRIMARY KEY,
    navn VARCHAR(100) NOT NULL,
    stilling VARCHAR(50),
    lonn DECIMAL(10, 2),
    ansatt_dato DATE
);
```

### Øvelse 2: Sett inn data

```sql
INSERT INTO ansatte (navn, stilling, lonn, ansatt_dato) VALUES
    ('Per Hansen', 'Butikksjef', 45000.00, '2020-01-15'),
    ('Line Berg', 'Selger', 35000.00, '2021-03-20'),
    ('Tom Johansen', 'Lagersjef', 40000.00, '2019-11-01'),
    ('Nina Olsen', 'Selger', 36000.00, '2022-06-10');
```

### Øvelse 3: Hent og filtrer data

```sql
-- Alle ansatte
SELECT * FROM ansatte;

-- Kun navn og stilling
SELECT navn, stilling FROM ansatte;

-- Ansatte med lønn over 35000
SELECT * FROM ansatte WHERE lonn > 35000;

-- Ansatte som er selgere
SELECT * FROM ansatte WHERE stilling = 'Selger';

-- Sorter etter lønn, høyest først
SELECT * FROM ansatte ORDER BY lonn DESC;

-- Ansatte ansatt etter 2020
SELECT * FROM ansatte WHERE ansatt_dato > '2020-01-01';
```

## Nyttige kommandoer - Oppsummering

```sql
-- Koble til MariaDB
mariadb -u brukernavn -p

-- Opprette bruker
CREATE USER 'bruker'@'localhost' IDENTIFIED BY 'passord';
GRANT ALL PRIVILEGES ON database.* TO 'bruker'@'localhost';
FLUSH PRIVILEGES;

-- Database-operasjoner
SHOW DATABASES;
CREATE DATABASE navn;
USE navn;
DROP DATABASE navn;

-- Tabell-operasjoner
SHOW TABLES;
DESCRIBE tabell;
CREATE TABLE tabell (...);
DROP TABLE tabell;

-- Data-operasjoner
INSERT INTO tabell (...) VALUES (...);
SELECT * FROM tabell;
SELECT kolonner FROM tabell WHERE betingelse;

-- Avslutte
EXIT;
```

## Tips og beste praksis

1. **Bruk sterke passord** for databasebrukere
2. **Gi kun nødvendige rettigheter** til brukere (prinsippet om minste privilegium)
3. **Bruk AUTO_INCREMENT** for primærnøkler
4. **Spesifiser alltid kolonnenavn** i INSERT-setninger for bedre vedlikehold
5. **Test spørringer med LIMIT** først når du jobber med store tabeller
6. **Bruk DESCRIBE** for å sjekke tabellstruktur før du skriver spørringer
7. **Ta regelmessige backups** av databasene dine

## Videre læring

Nå som du har lært grunnleggende, kan du utforske:

- JOIN-operasjoner for å kombinere data fra flere tabeller
- UPDATE og DELETE for å endre og slette data
- Indekser for å forbedre ytelse
- Transaksjoner for å sikre dataintegritet
- Fremmednøkler (FOREIGN KEY) for relasjoner mellom tabeller
- Visninger (VIEWS) for komplekse spørringer
- Stored procedures og triggers for avansert funksjonalitet

Lykke til med MariaDB!
