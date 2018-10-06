El algotimo hi/lo

El algoritmo hi/lo divide el dominio de las secuencias en grupos “hi”. Un valor “hi” es asignado de forma sincrona. Cada grupo “hi” esta compuesta po un numero maximo de entradas “lo”, los cuales pueden ser asignadas sin necesidad de preocuparnos por duplicidad debido a entornos concurrentes.

    El token “hi” es asignado por la base de datos, y de esta forma se garantiza que dos llamadas concurrentes obtengan valores consecutivos unicos
    Una vez que el token “hi” es obtenido lo unico que necesitamos es el "tamaño de incremento" (cantidad de entradas “lo”)
    El rango de identificadores esta dado por la formula:

    [(hi -1) * incrementSize) + 1, (hi * incrementSize) + 1)

    y el valor “lo” se obtendra de:

    [0, incrementSize)

    iniciando desde:

    [(hi -1) * incrementSize) + 1)
    Cuando todos los valores “lo” son usados, un nuevo valor “hi” es obtenido y el ciclo continua.


En el siguiente ejemplo se muestra la aplicacion del algoritmo con un incremento de 3.

Se insertan 12 usuarios y solo se hacen 4 llamadas a la secuencia.


Hibernate: drop table if exists USER
Hibernate: drop table if exists ID_SEQ_HILO_SEQ
Hibernate: create table USER (ID integer not null, FIRSTNAME varchar(255), LASTNAME varchar(255), EMAIL varchar(255), USERNAME varchar(255), primary key (ID))
Hibernate: create table ID_SEQ_HILO_SEQ ( next_val bigint )
Hibernate: insert into ID_SEQ_HILO_SEQ values ( 1 )

Hibernate: select next_val as id_val from ID_SEQ_HILO_SEQ for update
Hibernate: update ID_SEQ_HILO_SEQ set next_val= ? where next_val=?
Hibernate: insert into USER (FIRSTNAME, LASTNAME, EMAIL, USERNAME, ID) values (?, ?, ?, ?, ?)
Hibernate: insert into USER (FIRSTNAME, LASTNAME, EMAIL, USERNAME, ID) values (?, ?, ?, ?, ?)
Hibernate: insert into USER (FIRSTNAME, LASTNAME, EMAIL, USERNAME, ID) values (?, ?, ?, ?, ?)
Hibernate: select next_val as id_val from ID_SEQ_HILO_SEQ for update
Hibernate: update ID_SEQ_HILO_SEQ set next_val= ? where next_val=?
Hibernate: insert into USER (FIRSTNAME, LASTNAME, EMAIL, USERNAME, ID) values (?, ?, ?, ?, ?)
Hibernate: insert into USER (FIRSTNAME, LASTNAME, EMAIL, USERNAME, ID) values (?, ?, ?, ?, ?)
Hibernate: insert into USER (FIRSTNAME, LASTNAME, EMAIL, USERNAME, ID) values (?, ?, ?, ?, ?)
Hibernate: select next_val as id_val from ID_SEQ_HILO_SEQ for update
Hibernate: update ID_SEQ_HILO_SEQ set next_val= ? where next_val=?
Hibernate: insert into USER (FIRSTNAME, LASTNAME, EMAIL, USERNAME, ID) values (?, ?, ?, ?, ?)
Hibernate: insert into USER (FIRSTNAME, LASTNAME, EMAIL, USERNAME, ID) values (?, ?, ?, ?, ?)
Hibernate: insert into USER (FIRSTNAME, LASTNAME, EMAIL, USERNAME, ID) values (?, ?, ?, ?, ?)
Hibernate: select next_val as id_val from ID_SEQ_HILO_SEQ for update
Hibernate: update ID_SEQ_HILO_SEQ set next_val= ? where next_val=?
Hibernate: insert into USER (FIRSTNAME, LASTNAME, EMAIL, USERNAME, ID) values (?, ?, ?, ?, ?)
Hibernate: insert into USER (FIRSTNAME, LASTNAME, EMAIL, USERNAME, ID) values (?, ?, ?, ?, ?)
Hibernate: insert into USER (FIRSTNAME, LASTNAME, EMAIL, USERNAME, ID) values (?, ?, ?, ?, ?)
Hibernate: select user0_.ID as ID1_0_, user0_.FIRSTNAME as FIRSTNAM2_0_, user0_.LASTNAME as LASTNAME3_0_, user0_.EMAIL as EMAIL4_0_, user0_.USERNAME as USERNAME5_0_ from USER user0_
1 Frank Johnson frank.che88@gmail.com Jonislla 
2 Henry Johnson henry.gustavo@gmail.com fuentes 
3 Frank Johnson frank.che88@gmail.com Jonislla 
4 Henry Johnson henry.gustavo@gmail.com fuentes 
5 Frank Johnson frank.che88@gmail.com Jonislla 
6 Henry Johnson henry.gustavo@gmail.com fuentes 
7 Frank Johnson frank.che88@gmail.com Jonislla 
8 Henry Johnson henry.gustavo@gmail.com fuentes 
9 Frank Johnson frank.che88@gmail.com Jonislla 
10 Henry Johnson henry.gustavo@gmail.com fuentes 
11 Frank Johnson frank.che88@gmail.com Jonislla 
12 Henry Johnson henry.gustavo@gmail.com fuentes 