```SQL
		-- Eliminar tablas si existen
DROP TABLE IF EXISTS herramienta CASCADE;
DROP TABLE IF EXISTS gestor_produccion CASCADE;
DROP TABLE IF EXISTS actividad CASCADE;
DROP TABLE IF EXISTS lote CASCADE;
DROP TABLE IF EXISTS gestor_produccion_telefono CASCADE;
DROP TABLE IF EXISTS categoria_taller CASCADE;
DROP TABLE IF EXISTS estado_asignacion CASCADE;
DROP TABLE IF EXISTS taller CASCADE;
DROP TABLE IF EXISTS operario CASCADE;
DROP TABLE IF EXISTS asignacion_actividad CASCADE;
DROP TABLE IF EXISTS operario_telefono CASCADE;
DROP TABLE IF EXISTS estado_soli_herra CASCADE;
DROP TABLE IF EXISTS solicitud_herramienta CASCADE;
DROP TABLE IF EXISTS mantenimiento_herramienta CASCADE;
DROP TABLE IF EXISTS Estado_Reclamo CASCADE;
DROP TABLE IF EXISTS Descripcion_reclamo CASCADE;
DROP TABLE IF EXISTS Reclamo CASCADE;
DROP TABLE IF EXISTS Reporte_reclamo CASCADE;
DROP TABLE IF EXISTS Reporte_herramienta CASCADE;
DROP TABLE IF EXISTS Tipo_deduccion CASCADE;
DROP TABLE IF EXISTS Deduccion CASCADE;
DROP TABLE IF EXISTS Tipo_Sueldo_Base CASCADE;
DROP TABLE IF EXISTS Tipo_Bonificacion CASCADE;
DROP TABLE IF EXISTS Bonificacion CASCADE;
DROP TABLE IF EXISTS Periodo_pago CASCADE;
DROP TABLE IF EXISTS Nomina CASCADE;
DROP TABLE IF EXISTS Estado_Observacion CASCADE;
DROP TABLE IF EXISTS Descripcion_observacion CASCADE;
DROP TABLE IF EXISTS observacion CASCADE;
DROP TABLE IF EXISTS fallo CASCADE;
DROP TABLE IF EXISTS estandar_de_calidad CASCADE;
DROP TABLE IF EXISTS mantenimiento_maquinaria CASCADE;
DROP TABLE IF EXISTS Transporte CASCADE;
DROP TABLE IF EXISTS Solicitud_insumo CASCADE;
DROP TABLE IF EXISTS Transportista CASCADE;
DROP TABLE IF EXISTS Tipo_vehiculo CASCADE;
-- Eliminar el trigger
DROP TRIGGER IF EXISTS before_insert_asignacion ON asignacion_actividad;

-- Eliminar la función del trigger
DROP FUNCTION IF EXISTS asignacion_id_trigger;

-- Eliminar la secuencia
DROP SEQUENCE IF EXISTS asignacion_seq;

-- Eliminar la tabla asignacion_actividad
DROP TABLE IF EXISTS asignacion_actividad;

-- Eliminar vistas si existen
DROP VIEW IF EXISTS Reporte_Reclamos_Por_Fecha;
DROP VIEW IF EXISTS Reporte_Reclamos_Por_Descripcion;
DROP VIEW IF EXISTS Reporte_Reclamos_Por_Estado;
DROP VIEW IF EXISTS Reporte_Reclamos_Por_Operario;

-- Eliminar la secuencia
DROP SEQUENCE IF EXISTS solicitud_id_seq;
-- Eliminar el trigger
DROP TRIGGER IF EXISTS set_solicitud_id ON solicitud_herramienta;

-- Eliminar la función
DROP FUNCTION IF EXISTS generate_solicitud_id();



CREATE SEQUENCE solicitud_id_seq
    START WITH 1
    INCREMENT BY 1;


-- Función para generar IDs alfanuméricos
CREATE OR REPLACE FUNCTION gen_id(prefix TEXT, seq_name TEXT) RETURNS TEXT AS $$
DECLARE
    seq_val BIGINT;
BEGIN
    EXECUTE format('SELECT nextval(''%s'')', seq_name) INTO seq_val;
    RETURN prefix || LPAD(seq_val::TEXT, 3, '0');
END;
$$ LANGUAGE plpgsql;

CREATE TABLE herramienta (
    id_herramienta VARCHAR(6) PRIMARY KEY,
    nombre_herramienta VARCHAR(100),
    modelo VARCHAR(100),
    nombre_proveedor VARCHAR(100),
	disponible BOOLEAN DEFAULT TRUE
);

CREATE TABLE gestor_produccion
(
  id_gestor CHAR(6) NOT NULL,
  dni CHAR(8) NOT NULL,
  prim_nom_ges VARCHAR(50) NOT NULL,
  seg_nom_ges VARCHAR(50) NOT NULL,
  prim_ape_ges VARCHAR(50) NOT NULL,
  seg_ape_ges VARCHAR(50) NOT NULL,
  PRIMARY KEY (id_gestor)
);

CREATE TABLE actividad
(
  id_actividad CHAR(6) NOT NULL,
  nombre_actividad VARCHAR(50) NOT NULL,
  PRIMARY KEY (id_actividad)
);

CREATE TABLE lote
(
  id_lote CHAR(6) NOT NULL,
  fecha_produccion DATE NOT NULL,
  cant_prod INT NOT NULL,
  PRIMARY KEY (id_lote)
);

CREATE TABLE categoria_taller
(
  id_cate_taller CHAR(6) NOT NULL,
  nom_cate_taller VARCHAR(50) NOT NULL,
  PRIMARY KEY (id_cate_taller)
);

CREATE TABLE estado_asignacion
(
  id_est_asignacion CHAR(6) NOT NULL,
  nom_est_asignacion VARCHAR(50) NOT NULL,
  PRIMARY KEY (id_est_asignacion)
);

CREATE TABLE taller
(
  id_taller CHAR(6) NOT NULL,
  capacidad_taller INT NOT NULL,
  id_cate_taller CHAR(6) NOT NULL,
  PRIMARY KEY (id_taller),
  FOREIGN KEY (id_cate_taller) REFERENCES categoria_taller(id_cate_taller)
);

CREATE TABLE operario
(
  id_operario CHAR(6) NOT NULL,
  prim_nom_op VARCHAR(50) NOT NULL,
  seg_nom_op VARCHAR(50) NOT NULL,
  prim_ape_op VARCHAR(50) NOT NULL,
  seg_ape_op VARCHAR(50) NOT NULL,
  dni CHAR(8) NOT NULL,
  id_taller CHAR(6) NOT NULL,
  PRIMARY KEY (id_operario),
  FOREIGN KEY (id_taller) REFERENCES taller(id_taller)
);

CREATE TABLE asignacion_actividad
(
  fecha_asig DATE NOT NULL,
  hora_inicio TIME NOT NULL,
  hora_fin TIME NOT NULL,
  id_asignacion CHAR(6) NOT NULL,
  id_gestor CHAR(6) NOT NULL,
  id_lote CHAR(6) NOT NULL,
  id_actividad CHAR(6) NOT NULL,
  id_operario CHAR(6) NOT NULL,
  id_est_asignacion CHAR(6) NOT NULL,
  PRIMARY KEY (id_asignacion),
  FOREIGN KEY (id_gestor) REFERENCES gestor_produccion(id_gestor),
  FOREIGN KEY (id_lote) REFERENCES lote(id_lote),
  FOREIGN KEY (id_actividad) REFERENCES actividad(id_actividad),
  FOREIGN KEY (id_operario) REFERENCES operario(id_operario),
  FOREIGN KEY (id_est_asignacion) REFERENCES estado_asignacion(id_est_asignacion)
);

CREATE TABLE estado_soli_herra(
	id_est_soli_herra VARCHAR(6) PRIMARY KEY,
	nom_est_soli_herra VARCHAR(50) DEFAULT 'Pendiente'
);
CREATE TABLE solicitud_herramienta (
    id_solicitud VARCHAR(10) PRIMARY KEY DEFAULT 'DEFAULT',
    fecha_solicitud TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    id_est_soli_herra VARCHAR(6) NOT NULL,
    id_operario VARCHAR(6) NOT NULL,
    id_gestor VARCHAR(6),
    id_herramienta VARCHAR(6) NOT NULL,
    FOREIGN KEY (id_operario) REFERENCES operario(id_operario),
    FOREIGN KEY (id_herramienta) REFERENCES herramienta(id_herramienta),
    FOREIGN KEY (id_gestor) REFERENCES gestor_produccion(id_gestor),
    FOREIGN KEY (id_est_soli_herra) REFERENCES estado_soli_herra(id_est_soli_herra)
);


CREATE TABLE Estado_Reclamo
(
 Id_estado_reclamo CHAR(6) NOT NULL,
 Nom_estado_reclamo VARCHAR(50) NOT NULL,
 PRIMARY KEY (Id_estado_reclamo)
);

CREATE TABLE Descripcion_reclamo
(
 Id_descrip_reclamo CHAR(6) NOT NULL,
 Nom_descrip_reclamo VARCHAR(50) NOT NULL,
 PRIMARY KEY (Id_descrip_reclamo)
);

CREATE TABLE Reclamo
(
 Id_reclamo CHAR(6) NOT NULL,
 Fecha_reclamo DATE NOT NULL,
 Id_operario CHAR(6) NOT NULL,
 Id_descrip_reclamo CHAR(6) NOT NULL,
 Id_estado_reclamo CHAR(6) NOT NULL,
 PRIMARY KEY (Id_reclamo),
 FOREIGN KEY (Id_operario) REFERENCES Operario(Id_operario),
 FOREIGN KEY (Id_descrip_reclamo) REFERENCES Descripcion_reclamo(Id_descrip_reclamo),
 FOREIGN KEY (Id_estado_reclamo) REFERENCES Estado_Reclamo(Id_estado_reclamo)
);

CREATE TABLE Estado_Observacion
(
 Id_estado_observacion CHAR(6) NOT NULL,
 Nom_estado_observacion VARCHAR(50) NOT NULL,
 PRIMARY KEY (Id_estado_observacion)
);

CREATE TABLE Descripcion_observacion
(
 Id_descrip_observacion CHAR(6) NOT NULL,
 Nom_descrip_observacion VARCHAR(50) NOT NULL,
 PRIMARY KEY (Id_descrip_observacion)
);

CREATE TABLE Observacion
(
 Id_observacion CHAR(6) NOT NULL,
 Fecha_observacion DATE NOT NULL,
 id_asignacion CHAR(6) NOT NULL,
 Id_descrip_observacion CHAR(6) NOT NULL,
 Id_estado_observacion CHAR(6) NOT NULL,
 PRIMARY KEY (Id_observacion),
 FOREIGN KEY (id_asignacion) REFERENCES asignacion_actividad(id_asignacion),
 FOREIGN KEY (Id_descrip_observacion) REFERENCES Descripcion_observacion(Id_descrip_observacion),
 FOREIGN KEY (Id_estado_observacion) REFERENCES Estado_Observacion(Id_estado_observacion)
);

CREATE TABLE Reporte_reclamo
(
    Id_reporte CHAR(9) NOT NULL,
    Fecha_reporte DATE NOT NULL,
    Hora_reporte TIME NOT NULL,
    Id_gestor CHAR(6) NOT NULL,
    PRIMARY KEY (id_reporte),
    FOREIGN KEY (id_gestor) REFERENCES gestor_produccion(id_gestor)
);

CREATE VIEW Reporte_Reclamos_Por_Fecha AS
SELECT Fecha_reclamo, COUNT(*) AS Numero_de_Reclamos
FROM Reclamo
GROUP BY Fecha_reclamo;

CREATE VIEW Reporte_Reclamos_Por_Descripcion AS
SELECT D.Nom_descrip_reclamo, COUNT(*) AS Numero_de_Reclamos
FROM Reclamo R
JOIN Descripcion_reclamo D ON R.Id_descrip_reclamo = D.Id_descrip_reclamo
GROUP BY D.Nom_descrip_reclamo;

CREATE VIEW Reporte_Reclamos_Por_Estado AS
SELECT E.Nom_estado_reclamo, COUNT(*) AS Numero_de_Reclamos
FROM Reclamo R
JOIN Estado_Reclamo E ON R.Id_estado_reclamo = E.Id_estado_reclamo
GROUP BY E.Nom_estado_reclamo;

CREATE VIEW Reporte_Reclamos_Por_Operario AS
SELECT O.Id_operario, COUNT(*) AS Numero_de_Reclamos
FROM Reclamo R
JOIN Operario O ON R.Id_operario = O.Id_operario
GROUP BY O.Id_operario;


CREATE TABLE Reporte_herramienta (
    id_reporte SERIAL PRIMARY KEY,
    categoria VARCHAR(50),
    valor VARCHAR(50),
    cantidad INT
);

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

SELECT * FROM Reporte_herramienta
WHERE categoria = 'Nombre de herramienta';
SELECT * FROM Reporte_herramienta
WHERE categoria = 'Proveedor de herramienta';
SELECT * FROM Reporte_herramienta
WHERE categoria = 'Modelo de herramienta';

CREATE TABLE Tipo_deduccion
(
 Id_tipo_deduccion CHAR(6) NOT NULL,
 Nom_tipo_deduccion VARCHAR(50) NOT NULL,
 PRIMARY KEY (Id_tipo_deduccion)
);

CREATE TABLE Deduccion
(
 Id_deduccion CHAR(6) NOT NULL,
 Monto_deducido FLOAT NOT NULL,
 Id_tipo_deduccion CHAR(6) NOT NULL,
 Id_nomina CHAR(6) NOT NULL,
 PRIMARY KEY (Id_deduccion),
 FOREIGN KEY (Id_tipo_deduccion) REFERENCES Tipo_deduccion(Id_tipo_deduccion)
);

CREATE TABLE Tipo_Sueldo_Base
(
    Id_sueldo_base CHAR(6) NOT NULL,
    Monto_sueldo_base FLOAT NOT NULL,
    PRIMARY KEY (Id_sueldo_base)
);

CREATE TABLE Tipo_Bonificacion
(
 Id_tipo_boni CHAR(6) NOT NULL,
 Nom_tipo_boni VARCHAR(50) NOT NULL,
 PRIMARY KEY (Id_tipo_boni)
);

CREATE TABLE Bonificacion
(
 Id_bonificacion CHAR(6) NOT NULL,
 Monto_bonificacion FLOAT NOT NULL,
 Id_tipo_boni CHAR(6) NOT NULL,
 PRIMARY KEY (Id_bonificacion),
 FOREIGN KEY (Id_tipo_boni) REFERENCES Tipo_Bonificacion(Id_tipo_boni)
);
CREATE TABLE Periodo_pago
(
 Id_periodo_pago CHAR(6) NOT NULL,
 Nom_periodo_pago VARCHAR(50) NOT NULL,
 PRIMARY KEY (Id_periodo_pago)
);
	
CREATE TABLE Nomina
(
    Id_nomina CHAR(6) NOT NULL,
    Total_pago FLOAT,
    Fecha_emision DATE NOT NULL,
    Id_periodo_pago CHAR(6) NOT NULL,
    Id_gestor CHAR(6) NOT NULL,
    Id_bonificacion CHAR(6) NOT NULL,
    Id_deduccion CHAR(6) NOT NULL,
    Id_sueldo_base CHAR(6) NOT NULL,
    PRIMARY KEY (Id_nomina),
    FOREIGN KEY (Id_periodo_pago) REFERENCES Periodo_Pago(Id_periodo_pago),
    FOREIGN KEY (Id_gestor) REFERENCES Gestor_Produccion(Id_gestor),
    FOREIGN KEY (Id_bonificacion) REFERENCES Bonificacion(Id_bonificacion),
    FOREIGN KEY (Id_deduccion) REFERENCES Deduccion(Id_deduccion),
    FOREIGN KEY (Id_sueldo_base) REFERENCES Tipo_Sueldo_Base(Id_sueldo_base)
);

CREATE TABLE fallo (
    id_fallo CHAR(6) PRIMARY KEY,
    tipo_fallo VARCHAR(20),
    id_herramienta CHAR(6),
    descripcion_fallo VARCHAR(100),
    fecha_fallo DATE,
    FOREIGN KEY (id_herramienta) REFERENCES herramienta(id_herramienta)
);

CREATE TABLE estandar_de_calidad ( 
	id_calidad CHAR(6) PRIMARY KEY, 
	tipo_estandar VARCHAR(200), 
	descripcion_estandar VARCHAR(200) );

CREATE TABLE mantenimiento_herramienta( 
	id_mantenimiento CHAR(6) PRIMARY KEY, 
	tipo_mantenimiento CHAR(2), 
	estado_mantenimiento VARCHAR(15), 
	fecha_mantenimiento DATE NOT NULL, 
	id_responsable CHAR(6),
	id_calidad CHAR(6), 
	id_fallo CHAR(6), 
	descripcion_mantenimiento VARCHAR(200), 
	FOREIGN KEY (id_responsable) REFERENCES operario(id_operario), 
	FOREIGN KEY (id_calidad) REFERENCES estandar_de_calidad(id_calidad), 
	FOREIGN KEY (id_fallo) REFERENCES fallo(id_fallo));
	
CREATE TABLE Tipo_vehiculo (
    id_tipo_vehiculo CHAR(6) NOT NULL,
    nombre_tipo_vehiculo VARCHAR(50) NOT NULL,
    PRIMARY KEY (id_tipo_vehiculo)
);
	
CREATE TABLE Transportista (
    id_Transportista CHAR(6) PRIMARY KEY,
    nombre_transportista VARCHAR(50),
    disponibilidad VARCHAR(20) DEFAULT 'DISPONIBLE',
    ruta VARCHAR(50) DEFAULT NULL
);

CREATE TABLE Solicitud_insumo (
    id_solicitud_insumo VARCHAR(10) NOT NULL,
    fecha_solicitud VARCHAR(10) NOT NULL,
    id_gestor CHAR(6) NOT NULL,
	tipo_insumo VARCHAR(50) NOT NULL,
	cantidad_insumo INT NOT NULL,
	Nombre_provedor VARCHAR(50), 
    PRIMARY KEY (id_solicitud_insumo),
    FOREIGN KEY (id_gestor) REFERENCES gestor_produccion(id_gestor)
);
	
CREATE TABLE Transporte (
    id_transporte CHAR(6) NOT NULL,
    id_operario CHAR(6) NOT NULL,
    fecha_transporte CHAR(10) NOT NULL,
    id_tipo_vehiculo CHAR(6) NOT NULL,
	id_solicitud_insumo VARCHAR(10) NOT NULL,
	id_Transportista CHAR(6) ,
    PRIMARY KEY (id_transporte),
    FOREIGN KEY (id_solicitud_insumo) REFERENCES Solicitud_insumo(id_solicitud_insumo),
    FOREIGN KEY (id_Transportista) REFERENCES Transportista(id_Transportista),
    FOREIGN KEY (id_tipo_vehiculo) REFERENCES Tipo_vehiculo(id_tipo_vehiculo)
);

CREATE SEQUENCE asignacion_seq;
CREATE OR REPLACE FUNCTION asignacion_id_trigger() RETURNS TRIGGER AS $$
BEGIN
    NEW.id_asignacion := gen_id('ASI', 'asignacion_seq');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;


CREATE TRIGGER before_insert_asignacion
BEFORE INSERT ON asignacion_actividad
FOR EACH ROW
EXECUTE FUNCTION asignacion_id_trigger();


CREATE OR REPLACE FUNCTION generate_solicitud_id()
RETURNS TRIGGER AS $$
DECLARE
    new_id VARCHAR(10);
BEGIN
    SELECT 'SOL' || LPAD(nextval('solicitud_id_seq')::TEXT, 3, '0')
    INTO new_id;
    NEW.id_solicitud := new_id;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER set_solicitud_id
BEFORE INSERT ON solicitud_herramienta
FOR EACH ROW
EXECUTE FUNCTION generate_solicitud_id();


