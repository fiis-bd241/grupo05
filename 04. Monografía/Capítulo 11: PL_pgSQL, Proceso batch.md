# Capítulo 11: PL_pgSQL, Proceso batch.

# MODULO DE ASIGNACION DE ACTIVIDADES (CREACION DE ID_ASIGNACION)
``` SQL
DROP TRIGGER IF EXISTS before_insert_asignacion ON asignacion_actividad;
DROP FUNCTION IF EXISTS asignacion_id_trigger;
DROP SEQUENCE IF EXISTS asignacion_seq;

CREATE SEQUENCE asignacion_seq;
CREATE OR REPLACE FUNCTION asignacion_id_trigger() RETURNS TRIGGER AS $$
BEGIN
    NEW.id_asignacion := gen_id('ASI', 'asignacion_seq');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Trigger for 'id_asignacion'
CREATE TRIGGER before_insert_asignacion
BEFORE INSERT ON asignacion_actividad
FOR EACH ROW
EXECUTE FUNCTION asignacion_id_trigger();


DROP TRIGGER IF EXISTS before_insert_nomina ON Nomina;
DROP FUNCTION IF EXISTS nomina_id_trigger();
DROP SEQUENCE IF EXISTS seq_id_nomina CASCADE;
```


# CAMBIO DE ESTADO ENTRE FALLO, MANTEMINIMIENTO DE HERRAMIENTA Y HERRAMIENTA EN SUS ESTADOS
``` SQL
-- Para el trigger que marca arreglado_fallo como TRUE
DROP TRIGGER IF EXISTS trigger_update_arreglado_fallo_true ON mantenimiento_herramienta;
DROP FUNCTION IF EXISTS update_arreglado_fallo_true();

-- Para el trigger que marca arreglado_fallo como FALSE
DROP TRIGGER IF EXISTS trigger_update_arreglado_fallo_false ON mantenimiento_herramienta;
DROP FUNCTION IF EXISTS update_arreglado_fallo_false();

CREATE OR REPLACE FUNCTION update_arreglado_fallo_true() 
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.id_estado_mantenimiento = 'ESTM02' THEN
        UPDATE fallo
        SET arreglado_fallo = TRUE
        WHERE id_fallo = NEW.id_fallo;
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trigger_update_arreglado_fallo_true
AFTER UPDATE ON mantenimiento_herramienta
FOR EACH ROW
EXECUTE FUNCTION update_arreglado_fallo_true();

CREATE OR REPLACE FUNCTION update_arreglado_fallo_false() 
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.id_estado_mantenimiento = 'ESTM01' THEN
        UPDATE fallo
        SET arreglado_fallo = FALSE
        WHERE id_fallo = NEW.id_fallo;
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trigger_update_arreglado_fallo_false
AFTER UPDATE ON mantenimiento_herramienta
FOR EACH ROW
EXECUTE FUNCTION update_arreglado_fallo_false();
```

# MÓDULO DE GESTION DE HERRAMIENTAS Y MAQUINARIAS

``` SQL
CREATE OR REPLACE FUNCTION adjust_seq_solicitud() RETURNS TRIGGER AS $$
BEGIN
    IF NEW.id_solicitud IS NOT NULL THEN
        PERFORM setval('seq_solicitud', GREATEST((SELECT MAX(CAST(SUBSTRING(id_solicitud, 4) AS INTEGER)) FROM solicitud_herramienta), nextval('seq_solicitud')-1));
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Crear el Trigger
CREATE TRIGGER trg_adjust_seq_solicitud
BEFORE INSERT ON solicitud_herramienta
FOR EACH ROW
EXECUTE FUNCTION adjust_seq_solicitud();
```

# MÓDULO DE REGISTRO DE ACTIVIDADES

``` SQL
DROP TRIGGER IF EXISTS before_insert_asignacion ON asignacion_actividad;
DROP FUNCTION IF EXISTS asignacion_id_trigger;
DROP SEQUENCE IF EXISTS asignacion_seq;

CREATE SEQUENCE asignacion_seq;
CREATE OR REPLACE FUNCTION asignacion_id_trigger() RETURNS TRIGGER AS $$
BEGIN
    NEW.id_asignacion := gen_id('ASI', 'asignacion_seq');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Trigger for 'id_asignacion'
CREATE TRIGGER before_insert_asignacion
BEFORE INSERT ON asignacion_actividad
FOR EACH ROW
EXECUTE FUNCTION asignacion_id_trigger();
```

# MÓDULO DE SOLICITUD DE PEDIDOS DE INSUMOS

``` SQL
DROP TRIGGER IF EXISTS before_insert_solicitud_insumo ON Solicitud_insumo;
DROP FUNCTION IF EXISTS solicitud_insumo_id_trigger();
DROP SEQUENCE IF EXISTS seq_id_solicitud_insumo;

CREATE SEQUENCE seq_id_solicitud_insumo;
CREATE OR REPLACE FUNCTION solicitud_insumo_id_trigger() RETURNS TRIGGER AS $$
BEGIN
    NEW.id_solicitud_insumo := 'ISI' || LPAD(nextval('seq_id_solicitud_insumo')::TEXT, 3, '0');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
-- Trigger for 'id_solicitud_insumo'
CREATE TRIGGER before_insert_solicitud_insumo
BEFORE INSERT ON Solicitud_insumo
FOR EACH ROW
EXECUTE FUNCTION solicitud_insumo_id_trigger();
```

# MÓDULO DE REPORTES

``` SQL
CREATE VIEW Reporte_Reclamos_Por_Fecha AS
SELECT Fecha_reclamo, COUNT(*) AS Numero_de_Reclamos
FROM Reclamo
GROUP BY Fecha_reclamo;
```

``` SQL
CREATE VIEW Reporte_Reclamos_Por_Estado AS
SELECT E.Nom_estado_reclamo, COUNT(*) AS Numero_de_Reclamos
FROM Reclamo R
JOIN Estado_Reclamo E ON R.Id_estado_reclamo = E.Id_estado_reclamo
GROUP BY E.Nom_estado_reclamo;
```
``` SQL
CREATE VIEW Reporte_Reclamos_Por_Operario AS
SELECT O.Id_operario, COUNT(*) AS Numero_de_Reclamos
FROM Reclamo R
JOIN Operario O ON R.Id_operario = O.Id_operario
GROUP BY O.Id_operario;
```

``` SQL
INSERT INTO Reporte_herramienta (categoria, valor, cantidad)
SELECT 'Nombre de herramienta' AS categoria, nombre_herramienta AS valor, COUNT(*) AS cantidad
FROM herramienta
GROUP BY nombre_herramienta;
INSERT INTO Reporte_herramienta (categoria, valor, cantidad)
SELECT 'Proveedor de herramienta' AS categoria, nombre_proveedor AS valor, COUNT(*) AS cantidad
FROM herramienta
GROUP BY nombre_proveedor;
INSERT INTO Reporte_herramienta (categoria, valor, cantidad)
SELECT 'Modelo de herramienta' AS categoria, modelo AS valor, COUNT(*) AS cantidad
FROM herramienta
GROUP BY modelo;
```

# MÓDULO DE RECLAMOS

``` SQL
DROP TRIGGER IF EXISTS before_insert_reclamo ON Reclamo;
DROP FUNCTION IF EXISTS reclamo_id_trigger();
DROP SEQUENCE IF EXISTS seq_id_reclamo;

CREATE SEQUENCE seq_id_reclamo;
CREATE OR REPLACE FUNCTION reclamo_id_trigger() RETURNS TRIGGER AS $$
BEGIN
    NEW.Id_reclamo := 'REC' || LPAD(nextval('seq_id_reclamo')::TEXT, 3, '0');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Trigger for 'id_reclamo'
CREATE TRIGGER before_insert_reclamo
BEFORE INSERT ON Reclamo
FOR EACH ROW
EXECUTE FUNCTION reclamo_id_trigger();
```

# MÓDULO DE CALIDAD DE HERRAMIENTAS Y MAQUINARIA
``` SQL
DROP TRIGGER IF EXISTS before_insert_mantenimiento ON mantenimiento_herramienta;
DROP FUNCTION IF EXISTS mantenimiento_id_trigger();
DROP SEQUENCE IF EXISTS seq_id_mantenimiento;

CREATE SEQUENCE seq_id_mantenimiento;
CREATE OR REPLACE FUNCTION mantenimiento_id_trigger() RETURNS TRIGGER AS $$
BEGIN
    NEW.id_mantenimiento := 'MNT' || LPAD(nextval('seq_id_mantenimiento')::TEXT, 3, '0');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
-- Trigger for 'id_mantenimiento'
CREATE TRIGGER before_insert_mantenimiento
BEFORE INSERT ON mantenimiento_herramienta
FOR EACH ROW
EXECUTE FUNCTION mantenimiento_id_trigger();
```

```

DROP TRIGGER IF EXISTS before_insert_fallo ON fallo;
DROP TRIGGER IF EXISTS before_insert_fallo ON fallo;
DROP SEQUENCE IF EXISTS seq_id_fallo CASCADE;

CREATE SEQUENCE seq_id_fallo;
CREATE OR REPLACE FUNCTION fallo_id_trigger()
RETURNS TRIGGER AS $$
BEGIN
    NEW.id_fallo := 'FL' || LPAD(nextval('seq_id_fallo')::TEXT, 3, '0');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
-- Trigger for 'id_fallo'
CREATE TRIGGER before_insert_fallo
BEFORE INSERT ON fallo
FOR EACH ROW
EXECUTE FUNCTION fallo_id_trigger();
```

```
-- TRIGGERS PARA FALLOS Y HERRAMIENTA---

DROP TRIGGER IF EXISTS trigger_update_herramienta_after_insert ON fallo;
DROP FUNCTION IF EXISTS update_herramienta_disponible_after_insert();
DROP TRIGGER IF EXISTS trigger_update_herramienta_after_update ON fallo;
DROP FUNCTION IF EXISTS update_herramienta_disponible_after_update();
DROP TRIGGER IF EXISTS trigger_update_herramienta_after_delete ON fallo;
DROP FUNCTION IF EXISTS update_herramienta_disponible_after_delete();

CREATE OR REPLACE FUNCTION update_herramienta_disponible_after_insert() 
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.arreglado_fallo = FALSE THEN
        UPDATE herramienta
        SET disponible = FALSE
        WHERE id_herramienta = NEW.id_herramienta;
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trigger_update_herramienta_after_insert
AFTER INSERT ON fallo
FOR EACH ROW
EXECUTE FUNCTION update_herramienta_disponible_after_insert();

CREATE OR REPLACE FUNCTION update_herramienta_disponible_after_update() 
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.arreglado_fallo = TRUE THEN
        -- Verificar si hay otros fallos no arreglados
        IF NOT EXISTS (
            SELECT 1
            FROM fallo
            WHERE id_herramienta = NEW.id_herramienta AND arreglado_fallo = FALSE
        ) THEN
            UPDATE herramienta
            SET disponible = TRUE
            WHERE id_herramienta = NEW.id_herramienta;
        END IF;
    ELSE
        -- Si un fallo no está arreglado, marcar herramienta como no disponible
        UPDATE herramienta
        SET disponible = FALSE
        WHERE id_herramienta = NEW.id_herramienta;
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trigger_update_herramienta_after_update
AFTER UPDATE ON fallo
FOR EACH ROW
EXECUTE FUNCTION update_herramienta_disponible_after_update();

CREATE OR REPLACE FUNCTION update_herramienta_disponible_after_delete() 
RETURNS TRIGGER AS $$
BEGIN
    IF NOT EXISTS (
        SELECT 1
        FROM fallo
        WHERE id_herramienta = OLD.id_herramienta AND arreglado_fallo = FALSE
    ) THEN
        UPDATE herramienta
        SET disponible = TRUE
        WHERE id_herramienta = OLD.id_herramienta;
    END IF;
    RETURN OLD;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trigger_update_herramienta_after_delete
AFTER DELETE ON fallo
FOR EACH ROW
EXECUTE FUNCTION update_herramienta_disponible_after_delete();
```
```
-- TRIGGERS PARA MANTENIMIENTO Y FALLOS---
-- Para el trigger que marca arreglado_fallo como TRUE
DROP TRIGGER IF EXISTS trigger_update_arreglado_fallo_true ON mantenimiento_herramienta;
DROP FUNCTION IF EXISTS update_arreglado_fallo_true();

-- Para el trigger que marca arreglado_fallo como FALSE
DROP TRIGGER IF EXISTS trigger_update_arreglado_fallo_false ON mantenimiento_herramienta;
DROP FUNCTION IF EXISTS update_arreglado_fallo_false();

CREATE OR REPLACE FUNCTION update_arreglado_fallo_true() 
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.id_estado_mantenimiento = 'ESTM02' THEN
        UPDATE fallo
        SET arreglado_fallo = TRUE
        WHERE id_fallo = NEW.id_fallo;
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trigger_update_arreglado_fallo_true
AFTER UPDATE ON mantenimiento_herramienta
FOR EACH ROW
EXECUTE FUNCTION update_arreglado_fallo_true();

CREATE OR REPLACE FUNCTION update_arreglado_fallo_false() 
RETURNS TRIGGER AS $$
BEGIN
    IF NEW.id_estado_mantenimiento = 'ESTM01' THEN
        UPDATE fallo
        SET arreglado_fallo = FALSE
        WHERE id_fallo = NEW.id_fallo;
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trigger_update_arreglado_fallo_false
AFTER UPDATE ON mantenimiento_herramienta
FOR EACH ROW
EXECUTE FUNCTION update_arreglado_fallo_false();
```


# MÓDULO DE REMUNERACIÓN DEL OPERARIO

```
UPDATE Nomina
SET Total_pago = (
    SELECT 
        Tipo_Sueldo_Base.Monto_sueldo_base + 
        Bonificacion.Monto_bonificacion - 
        Deduccion.Monto_deducido
    FROM 
        Tipo_Sueldo_Base, Bonificacion, Deduccion
    WHERE 
        Nomina.Id_sueldo_base = Tipo_Sueldo_Base.Id_sueldo_base
        AND Nomina.Id_bonificacion = Bonificacion.Id_bonificacion
        AND Nomina.Id_deduccion = Deduccion.Id_deduccion
);
```

``` SQL
DROP TRIGGER IF EXISTS before_insert_nomina ON Nomina;
DROP FUNCTION IF EXISTS nomina_id_trigger();
DROP SEQUENCE IF EXISTS seq_id_nomina CASCADE;

CREATE SEQUENCE seq_id_nomina;
CREATE OR REPLACE FUNCTION nomina_id_trigger() RETURNS TRIGGER AS $$
BEGIN
    NEW.id_nomina := 'NOM' || LPAD(nextval('seq_id_nomina')::TEXT, 3, '0');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Trigger for 'id_nomina'
CREATE TRIGGER before_insert_nomina
BEFORE INSERT ON Nomina
FOR EACH ROW
EXECUTE FUNCTION nomina_id_trigger();
```

``` SQL
DROP TRIGGER IF EXISTS before_insert_deduccion ON Deduccion;
DROP FUNCTION IF EXISTS deduccion_id_trigger();
DROP SEQUENCE IF EXISTS seq_id_deduccion;

CREATE SEQUENCE seq_id_deduccion;
CREATE OR REPLACE FUNCTION deduccion_id_trigger() RETURNS TRIGGER AS $$
BEGIN
    NEW.Id_deduccion := 'DER' || LPAD(nextval('seq_id_deduccion')::TEXT, 3, '0');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

-- Trigger for 'id_deduccion'
CREATE TRIGGER before_insert_deduccion
BEFORE INSERT ON Deduccion
FOR EACH ROW
EXECUTE FUNCTION deduccion_id_trigger();
```

``` SQL
DROP TRIGGER IF EXISTS before_insert_bonificacion ON Bonificacion;
DROP FUNCTION IF EXISTS bonificacion_id_trigger();
DROP SEQUENCE IF EXISTS seq_id_bonificacion;

CREATE SEQUENCE seq_id_bonificacion;
CREATE OR REPLACE FUNCTION bonificacion_id_trigger()
RETURNS TRIGGER AS $$
BEGIN
    NEW.id_bonificacion := 'BOD' || LPAD(nextval('seq_id_bonificacion')::TEXT, 3, '0');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
CREATE TRIGGER before_insert_bonificacion
BEFORE INSERT ON Bonificacion
FOR EACH ROW
EXECUTE FUNCTION bonificacion_id_trigger();
```

## Explicación Detallada del Proceso Batch:

- El proceso batch presentado es una función en PL/pgSQL para calcular el total a pagar en una tabla de nómina. Se procede a brindar una explicación paso a paso de cómo funciona este proceso:
  
``` SQL
CREATE OR REPLACE FUNCTION calcular_total_pago() RETURNS VOID AS $$
```

1. Creación de la función:  Esta línea crea o reemplaza una función llamada calcular_total_pago que no devuelve ningún valor (RETURNS VOID).
  
``` SQL
DECLARE
    rec RECORD;
    sueldo_base FLOAT;
    total_bonificaciones FLOAT;
    total_deducciones FLOAT;
    total_pago FLOAT;

```

2. Declaración de las variables:

``` SQL
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

``` SQL
   BEGIN
```
Inicia el bloque de código de la función.


4. Cursor para Iterar sobre la Tabla nomina

``` SQL
FOR rec IN SELECT * FROM nomina LOOP

```
Se utiliza un cursor para iterar sobre todos los registros de la tabla nomina.


5. Obtener el Sueldo Base

``` SQL
SELECT monto_sueldo_base INTO sueldo_base
FROM tipo_sueldo_base
WHERE id_sueldo_base = rec.id_sueldo_base;

```
Para cada registro en la tabla nomina, se obtiene el monto_sueldo_base de la tabla tipo_sueldo_base basado en el id_sueldo_base del registro actual y se almacena en la variable sueldo_base.

6. Obtener el Total de Bonificaciones

``` SQL
SELECT SUM(monto_bonificacion) INTO total_bonificaciones
FROM bonificacion
WHERE id_bonificacion = rec.id_bonificacion;

```
Se calcula la suma de todas las bonificaciones asociadas al id_bonificacion del registro actual y se almacena en la variable total_bonificaciones.

7. Obtener el Total de Deducciones

``` SQL
SELECT SUM(monto_deducido) INTO total_deducciones
FROM deduccion
WHERE id_deduccion = rec.id_deduccion;

```
Se calcula la suma de todas las deducciones asociadas al id_deduccion del registro actual y se almacena en la variable total_deducciones.

8. Calcular el Total a Pagar


``` SQL
total_pago = sueldo_base + total_bonificaciones - total_deducciones;

```
Se calcula el total a pagar sumando el sueldo base y las bonificaciones, y restando las deducciones.


9. Actualizar la Tabla nomina

``` SQL
UPDATE nomina
SET total_pago = total_pago
WHERE id_nomina = rec.id_nomina;

```
Se actualiza el campo total_pago de la tabla nomina con el valor calculado para el registro actual.


10. Fin del Bucle

``` SQL
END LOOP;
END;
$$ LANGUAGE plpgsql;

```
Se cierra el bucle y se finaliza el bloque de código de la función.


11. Ejecutar la Función

``` SQL
SELECT calcular_total_pago();

```
Se ejecuta la función calcular_total_pago.


## ¿Por Qué es un Proceso Batch?
Un proceso batch se caracteriza por:

Procesamiento de Lotes de Datos: El proceso iterativamente maneja todos los registros en la tabla nomina.
Automatización: Realiza múltiples operaciones de manera automatizada sin intervención manual.
Operaciones Programadas: Puede ser programado para ejecutarse a intervalos específicos, por ejemplo, al final del mes o semana.
Manejo de Grandes Volúmenes de Datos: Está diseñado para procesar un gran número de registros en una única ejecución.

