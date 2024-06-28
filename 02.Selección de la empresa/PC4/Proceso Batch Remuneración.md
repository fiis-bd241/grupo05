```SQL
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

-- Creación de la función batch para calcular el total a pagar en la tabla de nomina
CREATE OR REPLACE FUNCTION calcular_total_pago() RETURNS VOID AS $$
DECLARE
    rec RECORD;
    sueldo_base FLOAT;
    total_bonificaciones FLOAT;
    total_deducciones FLOAT;
    total_pago FLOAT;
BEGIN
    -- Cursor para iterar sobre todos los registros de la tabla nomina
    FOR rec IN SELECT * FROM nomina LOOP
        -- Obtener el monto del sueldo base
        SELECT monto_sueldo_base INTO sueldo_base
        FROM tipo_sueldo_base
        WHERE id_sueldo_base = rec.id_sueldo_base;

        -- Obtener el total de bonificaciones
        SELECT SUM(monto_bonificacion) INTO total_bonificaciones
        FROM bonificacion
        WHERE id_bonificacion = rec.id_bonificacion;

        -- Obtener el total de deducciones
        SELECT SUM(monto_deducido) INTO total_deducciones
        FROM deduccion
        WHERE id_deduccion = rec.id_deduccion;

        -- Calcular el total a pagar
        total_pago = sueldo_base + total_bonificaciones - total_deducciones;

        -- Actualizar el campo total_pago en la tabla nomina
        UPDATE nomina
        SET total_pago = total_pago
        WHERE id_nomina = rec.id_nomina;
    END LOOP;
END;
$$ LANGUAGE plpgsql;

-- Ejecutar la función batch
SELECT calcular_total_pago();
