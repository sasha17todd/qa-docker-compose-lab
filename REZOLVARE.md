REZOLVARE – Exercițiu 11.7: Multi-Service Test Environment with Docker Compose



1\. Configurație

Fișierul `compose.yaml` definește următoarele servicii:

\- **db** – PostgreSQL 16 (bază de date)

\- **cache** – Redis 7 (sistem de cache)

\- **adminer** – interfață web pentru administrare baze de date



Conectivitatea între containere este automată prin rețeaua internă Docker Compose.



2\. Healthcheck și dependințe

Serviciul `db` are un healthcheck bazat pe comanda `pg\_isready`.

Serviciul `adminer` are `depends\_on` cu `condition: service\_healthy`, astfel încât să pornească doar după ce baza de date este complet inițializată.



3\. Test în Adminer

Am accesat interfața (http://localhost:8888) și m-am conectat cu:

\- **System**: PostgreSQL  

\- **Server**: db  

\- **Username**: qa\_user  

\- **Password**: qa\_pass  

\- **Database**: qa\_db  



Apoi am creat tabelul de test folosind comanda SQL:



```sql

CREATE TABLE tests (

&nbsp; id SERIAL PRIMARY KEY,

&nbsp; name VARCHAR(50)

);



