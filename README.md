# Sistema de registro de cargos empleado - empleador
Un programa de contabilidad que contiene información de empleados, empleadores y registros de las relaciones entre ellos.
---

# Propuesta de Proceso de Modernización

las funciones que vamos a poner como alcance en las funcionalidades a modernizar son las siguientes:

  *	Registro de empleador
  *	Registro de empleado
  * Búsqueda de empleados
  * Registro de pagos al empleador

El escenario de modernización que vamos a trabajar para aplicar en la aplicación es la siguiente:

1. **Ingeniería inversa dirigida por modelos**. El objetivo de este escenario consiste en la extracción y repre-sentación conceptual del conocimiento de la aplicación monolítica. En este sentido, se definen dos líneas diferentes de acción:
   
a. **Análisis estáticos y dinámicos**. Su misión consiste en generar consultas a los diferentes formularios que permitan explorar toda la aplicación y extraer información de las mismas. En el caso de apli-caciones desarrolladas con frameworks basados en el patrón MVC, se deben analizar los diferentes artefactos que permiten especificar la vistas, el modelo y los controladores. 
  
b. **Minería de datos de los registros de ejecución de la aplicación**. Su misión consiste en encontrar información que pueda apoyar decisiones de diseño posteriores dentro del proceso de modernización, como por ejemplo, qué datos o qué lógica de negocio puede moverse a cliente y de qué forma, también como se puede desacoplar las dependencia de los datos y objetos entre sí. 

---
# v1 branch
## Screenshot
<p align="center"><strong>Login</strong></p>
<p align="center"><img src="https://user-images.githubusercontent.com/71611710/157845415-c8f293df-5e1a-4ac5-a066-1971ee3ab6ae.png"></p>

| **Homepage**            | **Employer registration**|  **Worker registration**
:------------------------:|:------------------------:|:-------------------------:
![2-home_page](https://user-images.githubusercontent.com/71611710/157845986-0b99502d-ec6a-411c-999c-d37859dcf47e.png) | ![3-new_employer](https://user-images.githubusercontent.com/71611710/157849241-2a4ea23f-f195-4152-ab57-b2da20a1ea87.png)  |  ![3-new_worker](https://user-images.githubusercontent.com/71611710/157849850-5c6cfda1-05cd-4164-8287-474496cd189e.png)

| **Search Box**  | **Registration document**
:----------------:|:-------------------------:
![5-view_worker](https://user-images.githubusercontent.com/71611710/157850829-c03944a1-bd1b-41d6-875b-61f8d8ce4d62.png) | ![7-new_record_optionpane](https://user-images.githubusercontent.com/71611710/158039292-30c103d1-bdaa-4f3f-bd36-342815fd6efd.png)

---

## Requirements
Postgresql is used in this program. You can find the necessary jar file for postgresql java connection here:

> https://jdbc.postgresql.org/download.html

Or you can use a different database but for this to work, change:
```
DriverManager.getConnection("jdbc:database://host:port/database-name", "user-name", "password");
```
for postgresql:
```
DriverManager.getConnection("jdbc:postgresql://localhost:5432/db", "postgres", "password");
```
---

**And finally, in order not to get a database error, you should add the following tables to the database:**
```
CREATE TABLE admin(id smallserial primary key not null, username varchar, password varchar);
CREATE TABLE employer(employer_id serial primary key not null, name varchar not null, surname varchar not null, business varchar, phonenumber varchar);
CREATE TABLE employer(employer_id serial primary key not null, name varchar not null, surname varchar not null, business varchar, phonenumber varchar);
CREATE TABLE worker(worker_id serial primary key not null, name varchar not null, surname varchar not null, phone_number varchar);
CREATE TABLE worker_record(worker_record_id serial primary key not null, worker_id integer references worker(worker_id), employer_id integer references employer(employer_id), date varchar(10) not null, wage smallint not null);
CREATE TABLE employer_record(employer_record_id serial primary key not null, employer_id integer references employer(employer_id), date varchar(10) not null, note varchar(255), number_worker smallint not null, wage smallint not null);
CREATE TABLE worker_payment(worker_payment_id serial primary key not null, worker_id integer references worker(worker_id), employer_id integer references employer(employer_id), date varchar(10), not null, paid integer not null);
CREATE TABLE employer_payment(employer_payment_id serial primary key not null, employer_id integer references employer(employer_id), date varchar(10) not null, paid integer not null);
```

