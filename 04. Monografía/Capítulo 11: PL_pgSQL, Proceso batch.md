## Explicación Detallada del Proceso Batch:

- El proceso batch presentado es una función en PL/pgSQL para calcular el total a pagar en una tabla de nómina. Se procede a brindar una explicación paso a paso de cómo funciona este proceso:
  
```
CREATE OR REPLACE FUNCTION calcular_total_pago() RETURNS VOID AS $$
```

1. Creación de la función:  Esta línea crea o reemplaza una función llamada calcular_total_pago que no devuelve ningún valor (RETURNS VOID).
  
```
DECLARE
    rec RECORD;
    sueldo_base FLOAT;
    total_bonificaciones FLOAT;
    total_deducciones FLOAT;
    total_pago FLOAT;

```

2. Declaración de las variables:

```
DECLARE
    rec RECORD;
    sueldo_base FLOAT;
    total_bonificaciones FLOAT;
    total_deducciones FLOAT;
    total_pago FLOAT;
```
Se declaran variables para almacenar temporalmente los datos durante la ejecución de la función:

rec: Registro para iterar sobre la tabla nomina.
sueldo_base, total_bonificaciones, total_deducciones, total_pago: Variables para almacenar los valores necesarios para calcular el total a pagar.

3. Inicio del Bloque de Código

```
   BEGIN
```
Inicia el bloque de código de la función.


4. Cursor para Iterar sobre la Tabla nomina

```
FOR rec IN SELECT * FROM nomina LOOP

```
Se utiliza un cursor para iterar sobre todos los registros de la tabla nomina.


5. Obtener el Sueldo Base

```
SELECT monto_sueldo_base INTO sueldo_base
FROM tipo_sueldo_base
WHERE id_sueldo_base = rec.id_sueldo_base;

```
Para cada registro en la tabla nomina, se obtiene el monto_sueldo_base de la tabla tipo_sueldo_base basado en el id_sueldo_base del registro actual y se almacena en la variable sueldo_base.

6. Obtener el Total de Bonificaciones

```
SELECT SUM(monto_bonificacion) INTO total_bonificaciones
FROM bonificacion
WHERE id_bonificacion = rec.id_bonificacion;

```
Se calcula la suma de todas las bonificaciones asociadas al id_bonificacion del registro actual y se almacena en la variable total_bonificaciones.

7. Obtener el Total de Deducciones

```
SELECT SUM(monto_deducido) INTO total_deducciones
FROM deduccion
WHERE id_deduccion = rec.id_deduccion;

```
Se calcula la suma de todas las deducciones asociadas al id_deduccion del registro actual y se almacena en la variable total_deducciones.

8. Calcular el Total a Pagar


```
total_pago = sueldo_base + total_bonificaciones - total_deducciones;

```
Se calcula el total a pagar sumando el sueldo base y las bonificaciones, y restando las deducciones.


9. Actualizar la Tabla nomina

```
UPDATE nomina
SET total_pago = total_pago
WHERE id_nomina = rec.id_nomina;

```
Se actualiza el campo total_pago de la tabla nomina con el valor calculado para el registro actual.


10. Fin del Bucle

```
END LOOP;
END;
$$ LANGUAGE plpgsql;

```
Se cierra el bucle y se finaliza el bloque de código de la función.


11. Ejecutar la Función

```
SELECT calcular_total_pago();

```
Se ejecuta la función calcular_total_pago.


## ¿Por Qué es un Proceso Batch?
Un proceso batch se caracteriza por:

Procesamiento de Lotes de Datos: El proceso iterativamente maneja todos los registros en la tabla nomina.
Automatización: Realiza múltiples operaciones de manera automatizada sin intervención manual.
Operaciones Programadas: Puede ser programado para ejecutarse a intervalos específicos, por ejemplo, al final del mes o semana.
Manejo de Grandes Volúmenes de Datos: Está diseñado para procesar un gran número de registros en una única ejecución.

