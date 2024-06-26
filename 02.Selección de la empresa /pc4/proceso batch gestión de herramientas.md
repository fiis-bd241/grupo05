```SQL

-- Eliminar función y trigger si existen
DROP FUNCTION IF EXISTS adjust_seq_solicitud();
DROP TRIGGER IF EXISTS trg_adjust_seq_solicitud ON solicitud_herramienta;


-- Creación de la secuencia para solicitud_herramienta
CREATE SEQUENCE seq_solicitud START 1;

-- Función para generar IDs alfanuméricos
CREATE OR REPLACE FUNCTION gen_id(prefix TEXT, seq_name TEXT) RETURNS TEXT AS $$
DECLARE
    seq_val BIGINT;
BEGIN
    EXECUTE format('SELECT nextval(''%s'')', seq_name) INTO seq_val;
    RETURN prefix || LPAD(seq_val::TEXT, 3, '0');
END;
$$ LANGUAGE plpgsql;
