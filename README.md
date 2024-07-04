# Portfolio-SQL02

**•	TITULO: SISTEMA DE GESTION DE DATOS DE LA ESCUELA.**  

**•	DESCRIPCION DEL PROYECTO:** Este proyecto tiene como objetivo diseñar y desarrollar una base de datos para una escuela que permita gestionar la información de los estudiantes, el personal (staff), las áreas académicas, las asignaturas, los encargados y las profesiones. La base de datos proporcionará una plataforma centralizada para almacenar y acceder a datos esenciales, facilitando la administración y la toma de decisiones.

**•	OBJETIVOS:**

Centralizar toda la información relevante sobre estudiantes, personal, áreas, asignaturas, encargados y profesiones en una única base de datos para mejorar la accesibilidad y la integridad de los datos.

Gestión Eficiente de Estudiantes: Facilitar el seguimiento de la información de los estudiantes, incluyendo datos personales, detalles de contacto, historial académico y asignación de docentes.

Asignación y Seguimiento del Personal: Gestionar la información del personal, incluyendo datos personales, detalles de contacto, historial laboral, asignación de áreas y asignaturas, y relación con los encargados.

Organización de Áreas Académicas y Asignaturas: Organizar y categorizar las áreas académicas y asignaturas, permitiendo una fácil asignación y seguimiento del personal y los estudiantes en cada área.

Facilitación de Informes y Análisis: Proporcionar una base de datos estructurada que permita generar informes y análisis para la toma de decisiones informadas por parte de la administración de la escuela.

**•	HERRAMIENTAS O LENGUAJES:** Básicamente para este proyecto utilizamos la herramienta MySQL, en donde hicimos creacion de tablas, insercion de datos, consultas, subconsultas y joins.

**•	CONJUNTO DE DATOS:** Basicamente esta base de datos, se compone de seis tablas que son: Estudiantes, staff, asignaturas, areas, profesiones y encargados. Con estos datos podemos hacer una nalisis detallado del comportamiento estructural de la escuela, para asi poder tomar las mejores decisiones para la misma.


**•	DESARROLLO-EJECUCION:**

![Der](https://github.com/pocolus/Portfolio-SQL02/blob/main/Der.png)


# Consultas Base De Datos Escuela

**PRIMER MODULO**

1. Indicar cuántos cursos y carreras tiene el área de Data. Renombrar la nueva columna como
cant_asignaturas.
```sql
select Area.Nombre, 
COUNT(AsignaturasID) as Cantidad_Asignaturas
from Asignaturas
inner join Area
on Asignaturas.Area = Area.AreaID
where Area.Nombre = 'Data'
group by Area.Nombre;
```
2. Se requiere saber cual es el nombre, el documento de identidad y el teléfono de los estudiantes que son
profesionales en agronomía y que nacieron entre el año 1970 y el año 2000.

OPCION 1
```sql
select Nombre, Documento, Telefono
from Estudiantes
inner join Profesiones
on Estudiantes.Profesion = Profesiones.ProfesionesID
where Profesiones.Profesiones = 'Agronomo Agronoma' and YEAR([Fecha de Nacimiento]) between 1970 and 2000;
```
OPCION 2
```sql
select Nombre, Documento, Telefono
from Estudiantes
inner join Profesiones
on Estudiantes.Profesion = Profesiones.ProfesionesID
where Profesiones.Profesiones = 'Agronomo Agronoma' and [Fecha de Nacimiento] between '1970-01-01' and '2000-12-31';
```
OPCION 3
```sql
SELECT Nombre, Documento, telefono, [Fecha de Nacimiento] 
FROM Estudiantes
WHERE (Profesion) = 6 AND
YEAR ([Fecha de Nacimiento])>=1970 AND 
YEAR ([Fecha de Nacimiento])<=2000;
```
3. Se requiere un listado de los docentes que ingresaron en el año 2021 y concatenar los campos nombre y
apellido. El resultado debe utilizar un separador: guión (-). Ejemplo: Elba-Jimenez. Renombrar la nueva
columna como Nombres_Apellidos. Los resultados de la nueva columna deben estar en mayúsculas.
```sql
select UPPER (CONCAT_WS('-', Nombre, Apellido)) as Nombres_Apellido, [Fecha Ingreso]
from Staff
where YEAR([Fecha Ingreso]) = 2021;
```
4. Indicar la cantidad de encargados de docentes y de tutores. Renombrar la columna como CantEncargados.
Quitar la palabra ”Encargado ”en cada uno de los registros. Renombrar la columna como NuevoTipo.
```sql
select COUNT(Encargado_ID) as Cantidad_Encargados,
 REPLACE(Tipo, 'Encargado', '') as Nuevo_tipo
from Encargado
group by Tipo;
```
5. Indicar cuál es el precio promedio de las carreras y los cursos por jornada. Renombrar la nueva columna
como Promedio. Ordenar los promedios de Mayor a menor.
```sql
select Jornada, tipo,
AVG (Costo) as Promedio
from Asignaturas
group by Jornada, tipo
order by Promedio desc;
```
6. Se requiere calcular la edad de los estudiantes en una nueva columna. Renombrar a la nueva columna Edad.
Filtrar solo los que son mayores de 18 años. Ordenar de Menor a Mayor.

OPCION 1
```sql
select Nombre, Apellido,
DATEDIFF(YEAR,[Fecha de Nacimiento], GETDATE()) as Edad
from Estudiantes
where DATEDIFF(YEAR,[Fecha de Nacimiento], GETDATE())  > 18
order by Edad
```
OPCION 2
```sql
SELECT Nombre, Apellido, (DATEDIFF (DAY, [Fecha de Nacimiento], GETDATE())) / 365 AS EDAD
FROM Estudiantes
WHERE (DATEDIFF (DAY, [Fecha de Nacimiento], GETDATE())) / 365 > 18
ORDER BY EDAD ASC;
```
7. Se requiere saber el Nombre,el correo, la camada y la fecha de ingreso de personas del staff que contienen
correo .edu y su DocenteID se mayor o igual que 100.

OPCION 1
```sql
select Nombre, Correo, Camada, [Fecha Ingreso]
from Staff
where Correo like '%.edu' and DocentesID >= 100;
```
OPCION 2
```sql
SELECT Nombre, Correo, Camada, [Fecha Ingreso]
FROM Staff
WHERE RIGHT (Correo, 4) = '.edu' AND DocentesID >= 100;
```
8. Se requiere conocer el documento, el domicilio, el código postal y el nombre de los
primeros estudiantes que se registraron en la plataforma.
```sql
select Nombre, Documento, Domicilio, [Codigo Postal], [Fecha Ingreso]
from Estudiantes
order by [Fecha Ingreso]
```
9. Indicar el nombre, apellido y documento de identidad de los docentes y tutores que
tienen asignaturas “UX”.
```sql
select staff.Nombre, staff.Apellido, staff.Documento, Asignaturas.Nombre as Asignatura, Encargado.Nombre, Encargado.Apellido, Encargado.Documento
from Staff
inner join Encargado
on Staff.Encargado = Encargado.Encargado_ID
inner join Asignaturas
on Staff.Asignatura = Asignaturas.AsignaturasID
where Asignaturas.Nombre like '%UX%';
```
10. Se desea calcular el 25% de aumento para las asignaturas del área de marketing de la
jornada mañana se deben traer todos los campos, mas el de los cálculos
correspondientes el porcentaje y el Nuevo costo debe estar en decimal con 3 digitos.
Renombrar el calculo del porcentaje con el nombre porcentaje y la suma del costo
mas el porcentaje por NuevoCosto.
```sql
select Asignaturas.Nombre, Jornada, Area.Nombre as Area,  Costo,
costo * 0.25 as Porcentaje,
format((costo * 0.25) + Costo, '0.000') as Nuevo_Costo 
from asignaturas
inner join area
on Asignaturas.Area = Area.AreaID 
where Area.Nombre like'%Marketing%' and Asignaturas.Jornada = 'manana';
```
**SEGUNDO MODULO**

1. Indicar por jornada la cantidad de docentes que dictan y sumar los costos. Esta información solo se desea
visualizar para las asignaturas de desarrollo web. El resultado debe contener todos los valores registrados en la
primera tabla, Renombrar la columna del cálculo de la cantidad de docentes como cant_docentes y la
columna de la suma de los costos como suma_total.
```sql
select Jornada,
COUNT(Staff.DocentesID) as Cantidad_Docentes,
SUM(Asignaturas.Costo) as Suma_total
from Asignaturas
left join Staff
on Asignaturas.AsignaturasID = Staff.Asignatura
where Asignaturas.Nombre = 'desarrollo web'
group by Jornada;
```















