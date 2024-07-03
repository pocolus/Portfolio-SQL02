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


**CONSULTAS BASE DE DATOS ESCUELA**
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





