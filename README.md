# sql-select-fundamentals

Ejercicios de consultas SELECT básicas sobre una tabla de inventario.

- Motor: SQL Server
- Archivo principal: `consultas_basicas.sql`

1. ¿Por qué es mala práctica usar SELECT * en producción?

SELECT * trae todas las columnas de la tabla, se necesiten o no. En un ejercicio de práctica es cómodo, pero en un sistema real trae problemas concretos:

a) Rendimiento

Se leen y se envían por la red datos que nadie va a usar. Si la tabla tiene columnas pesadas (descripciones largas, imágenes, JSON) o millones de filas, la consulta se vuelve más lenta y consume más memoria.

b) Mantenibilidad

El resultado de SELECT * depende de cómo esté definida la tabla hoy. Si mañana alguien agrega, elimina o reordena una columna, la consulta devuelve algo distinto sin que nadie haya tocado el código, y los reportes que dependían de ese orden pueden romperse o, peor, cargar datos en la columna equivocada sin dar error.

c) Seguridad

Con * se pueden exponer columnas sensibles que no deberían salir de la base: costos internos, datos personales, contraseñas, márgenes. Si en el futuro se agrega una columna confidencial a la tabla, toda consulta con * empieza a mostrarla automáticamente.

2. ¿Por qué son importantes los alias para un stakeholder no técnico?

Los nombres de columna están pensados para la base de datos, no para las personas: suelen estar en inglés, abreviados o con guiones bajos. Un alias (AS) cambia el nombre con el que se muestra la columna en el resultado, sin modificar la tabla.

Para alguien de finanzas, ventas o dirección, eso es la diferencia entre un reporte que tiene que pedir que le expliquen y uno que puede leer y usar directamente.
