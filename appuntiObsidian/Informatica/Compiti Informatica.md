### ESERCITAZIONE
Con l’aiuto della dispensa del DDL e dell’altra sull’ SQL(consultatela fino dove tratta
gli argomenti della lezione) provate ad eseguire questa esercitazione che segue.
1) Dare le definizioni SQL (DDL) delle tabelle
```
AUTORE (Nome, Cognome, DataNascita, Nazionalità)
LIBRO (TitoloLibro, NomeAutore, CognomeAutore, Lingua)
```

```sql
CREATE TABLE AUTORE (
  Nome VARCHAR(50),
  Cognome VARCHAR(50),
  DataNascita DATE,
  Nazionalità VARCHAR(50)
);

CREATE TABLE LIBRO (
  TitoloLibro VARCHAR(100),
  NomeAutore VARCHAR(50),
  CognomeAutore VARCHAR(50),
  Lingua VARCHAR(50)
);
```
Per il vincolo foreign key (NomeAutore, CognomeAutore di Libro) specificare una
politica di cascade sulla cancellazione e di set null sulle modifiche.

```sql
ALTER TABLE LIBRO
ADD CONSTRAINT fk_LIBRO_AUTORE
FOREIGN KEY (NomeAutore, CognomeAutore)
REFERENCES AUTORE (Nome, Cognome)
ON DELETE CASCADE
ON UPDATE SET NULL;
```

2) Dato lo schema dell'esercizio precedente, spiegare cosa può capitare con l'esecuzione dei seguenti comandi di aggiornamento: 
```
delete from AUTORE where Cognome = 'Rossi'
update LIBRO set NomeAutore= 'Umberto' where CognomeAutore = 'Eco'
insert into AUTORE(Nome,Cognome) values('Antonio';'Bianchi')
update AUTORE set Nome = 'Italo' where Cognome = 'Calvino'
```

1. delete from AUTORE where Cognome = 'Rossi': questo comando eliminerà tutti i record dalla tabella AUTORE in cui il valore della colonna Cognome è Rossi.
2. update LIBRO set NomeAutore= 'Umberto' where CognomeAutore = 'Eco': questo comando modificherà il valore della colonna NomeAutore in tutti i record della tabella LIBRO in cui il valore della colonna CognomeAutore è 'Eco' impostandolo su 'Umberto'.
3. insert into AUTORE(Nome,Cognome): questo comando inserirà un nuovo record nella tabella AUTORE con i valori 'Antonio' per la colonna Nome e 'Bianchi' per la colonna Cognome.
4. update AUTORE set Nome = 'Italo' where Cognome = 'Calvino': questo comando modificherà il valore della colonna Nome in tutti i record della tabella AUTORE in cui il valore della colonna Cognome è 'Calvino' impostandolo su 'Italo'.

3) Date le definizioni:
```
create domain Dominio as integer default 10
create table Tabella (Attributo Dominio default 5)
```
indicare cosa avviene in seguito ai comandi:
```
alter table Tabella alter column Attributo drop default
alter domain Dominio drop default
drop domain Dominio
```
1. alter table Tabella alter column Attributo drop default: questo comando rimuoverà il valore predefinito (default) per la colonna Attributo della tabella Tabella.
2. alter domain Dominio drop default: questo comando rimuoverà il valore predefinito (default) per il dominio Dominio.
3. drop domain Dominio: questo comando eliminerà completamente il dominio Dominio, insieme a tutti gli attributi delle tabelle che lo utilizzano.