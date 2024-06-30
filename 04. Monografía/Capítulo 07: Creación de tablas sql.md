# Capítulo 07: Creacion de tablas


-Tabla: HERRAMIENTA
``` SQL
CREATE TABLE herramienta (
    id_herramienta VARCHAR(6) PRIMARY KEY,
    nombre_herramienta VARCHAR(100),
    modelo VARCHAR(100),
    nombre_proveedor VARCHAR(100),
	disponible BOOLEAN DEFAULT TRUE
);
``` 
-Tabla: GESTOR DE LA PRODUCCIÓN
``` SQL
CREATE TABLE gestor_produccion
(
  id_gestor CHAR(6) NOT NULL,
  gestor_contra VARCHAR(10) NOT NULL,
  dni CHAR(8) NOT NULL,
  prim_nom_ges VARCHAR(50) NOT NULL,
  seg_nom_ges VARCHAR(50) NOT NULL,
  prim_ape_ges VARCHAR(50) NOT NULL,
  seg_ape_ges VARCHAR(50) NOT NULL,
  PRIMARY KEY (id_gestor)
);
```
-Tabla: ACTIVIDAD
``` SQL
CREATE TABLE actividad
(
  id_actividad CHAR(6) NOT NULL,
  nombre_actividad VARCHAR(50) NOT NULL,
  PRIMARY KEY (id_actividad)
);
```
-Tabla: LOTE
``` SQL
CREATE TABLE lote
(
  id_lote CHAR(6) NOT NULL,
  fecha_produccion DATE DEFAULT CURRENT_DATE,
  cant_prod INT NOT NULL,
  PRIMARY KEY (id_lote)
);
```
-Tabla: CATEGORÍA DEL TALLER
``` SQL
CREATE TABLE categoria_taller
(
  id_cate_taller CHAR(6) NOT NULL,
  nom_cate_taller VARCHAR(50) NOT NULL,
  PRIMARY KEY (id_cate_taller)
);
```
-Tabla: ESTADO DE LA ASIGNACIÓN
``` SQL
CREATE TABLE estado_asignacion
(
  id_est_asignacion CHAR(6) NOT NULL,
  nom_est_asignacion VARCHAR(50) NOT NULL,
  PRIMARY KEY (id_est_asignacion)
);
```
-Tabla: TALLER
``` SQL
CREATE TABLE taller
(
  id_taller CHAR(6) NOT NULL,
  capacidad_taller INT NOT NULL,
  id_cate_taller CHAR(6) NOT NULL,
  PRIMARY KEY (id_taller),
  FOREIGN KEY (id_cate_taller) REFERENCES categoria_taller(id_cate_taller)
);
```
-Tabla: OPERARIO
``` SQL
CREATE TABLE operario
(
  id_operario CHAR(6) NOT NULL,
  operario_contra VARCHAR(10) NOT NULL,
  prim_nom_op VARCHAR(50) NOT NULL,
  seg_nom_op VARCHAR(50) NOT NULL,
  prim_ape_op VARCHAR(50) NOT NULL,
  seg_ape_op VARCHAR(50) NOT NULL,
  dni CHAR(8) NOT NULL,
  id_taller CHAR(6) NOT NULL,
  PRIMARY KEY (id_operario),
  FOREIGN KEY (id_taller) REFERENCES taller(id_taller)
);
```
-Tabla: ASIGNACIÓN DE ACTIVIDAD
``` SQL
CREATE TABLE asignacion_actividad
(
  id_asignacion CHAR(6) NOT NULL,
  fecha_asig DATE DEFAULT CURRENT_DATE,
  hora_inicio TIME NOT NULL,
  hora_fin TIME NOT NULL,
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
```
-Tabla: ESTADO DE LA SOLICITUD DE LA HERRAMIENTA
``` SQL
CREATE TABLE estado_soli_herra(
	id_est_soli_herra VARCHAR(6) PRIMARY KEY,
	nom_est_soli_herra VARCHAR(50) DEFAULT 'Pendiente'
);
```
-Tabla: SOLICITUD DE LA HERRAMIENTA
``` SQL
CREATE TABLE solicitud_herramienta (
    id_solicitud VARCHAR(10) PRIMARY KEY DEFAULT gen_id('SOL', 'seq_solicitud'),
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
```
-Tabla: ESTADO DEL RECLAMO
``` SQL
CREATE TABLE Estado_Reclamo
(
 Id_estado_reclamo CHAR(6) NOT NULL,
 Nom_estado_reclamo VARCHAR(50) NOT NULL,
 PRIMARY KEY (Id_estado_reclamo)
);
```
-Tabla: RECLAMO
``` SQL
CREATE TABLE Reclamo
(
 Id_reclamo CHAR(6) NOT NULL,
 Fecha_reclamo DATE DEFAULT CURRENT_DATE,
 Id_operario CHAR(6) NOT NULL,
 descrip_reclamo VARCHAR(100),
 Id_estado_reclamo CHAR(6) NOT NULL,
 PRIMARY KEY (Id_reclamo),
 FOREIGN KEY (Id_operario) REFERENCES Operario(Id_operario),
 FOREIGN KEY (Id_estado_reclamo) REFERENCES Estado_Reclamo(Id_estado_reclamo)
);
```
-Tabla: REPORTE DEL RECLAMO
``` SQL
CREATE TABLE Reporte_reclamo
(
    Id_reporte CHAR(9) NOT NULL,
    Fecha_reporte DATE DEFAULT CURRENT_DATE,
    Hora_reporte TIME NOT NULL,
    Id_gestor CHAR(6) NOT NULL,
    PRIMARY KEY (id_reporte),
    FOREIGN KEY (id_gestor) REFERENCES gestor_produccion(id_gestor)
);
```
-Tabla: REPORTE DE LA HERRAMIENTA
``` SQL
CREATE TABLE Reporte_herramienta (
    id_reporte SERIAL PRIMARY KEY,
    categoria VARCHAR(50),
    valor VARCHAR(50),
    cantidad INT
);
```
-Tabla: EMPRESA
``` SQL
CREATE TABLE Empresa(
	id_empresa SERIAL PRIMARY KEY NOT NULL,
	ruc NUMERIC(12) NOT NULL,
	regimen VARCHAR(25) NOT NULL,
	estado VARCHAR(20) NOT NULL,
	razon_social VARCHAR(50) NOT NULL,
	direccion VARCHAR(200) NOT NULL,
	giro VARCHAR(50) NOT NULL,
	ciudad VARCHAR(25) NOT NULL,
	logo VARCHAR(200) NOT NULL
);
```
-Tabla: TIPO DE DEDUCCIÓN
``` SQL
CREATE TABLE Tipo_deduccion
(
 Id_tipo_deduccion CHAR(6) NOT NULL,
 Nom_tipo_deduccion VARCHAR(50) NOT NULL,
 PRIMARY KEY (Id_tipo_deduccion)
);
```
-Tabla: DEDUCCIÓN
``` SQL
CREATE TABLE Deduccion
(
 Id_deduccion CHAR(6) NOT NULL,
 Monto_deducido FLOAT NOT NULL,
 Id_tipo_deduccion CHAR(6) NOT NULL,
 PRIMARY KEY (Id_deduccion),
 FOREIGN KEY (Id_tipo_deduccion) REFERENCES Tipo_deduccion(Id_tipo_deduccion)
);
```
-Tabla: TIPO DE SUELDO BASE
``` SQL
CREATE TABLE Tipo_Sueldo_Base
(
    Id_sueldo_base CHAR(6) NOT NULL,
    Monto_sueldo_base FLOAT NOT NULL,
    PRIMARY KEY (Id_sueldo_base)
);

```
-Tabla: TIPO DE BONIFICACIÓN
``` SQL
CREATE TABLE Tipo_Bonificacion
(
 Id_tipo_boni CHAR(6) NOT NULL,
 Nom_tipo_boni VARCHAR(50) NOT NULL,
 PRIMARY KEY (Id_tipo_boni)
);
```
-Tabla: BONIFICACIÓN
``` SQL
CREATE TABLE Bonificacion
(
 Id_bonificacion CHAR(6) NOT NULL,
 Monto_bonificacion FLOAT NOT NULL,
 Id_tipo_boni CHAR(6) NOT NULL,
 PRIMARY KEY (Id_bonificacion),
 FOREIGN KEY (Id_tipo_boni) REFERENCES Tipo_Bonificacion(Id_tipo_boni)
);

```
-Tabla: PERIODO DE PAGO 
``` SQL
CREATE TABLE Periodo_pago
(
 Id_periodo_pago CHAR(6) NOT NULL,
 Nom_periodo_pago VARCHAR(50) NOT NULL,
 PRIMARY KEY (Id_periodo_pago)
);
```
-Tabla: NÓMINA
``` SQL
CREATE TABLE Nomina
(
    Id_nomina CHAR(6) NOT NULL,
    Total_pago FLOAT,
    Fecha_emision DATE DEFAULT CURRENT_DATE,
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
```
-Tabla: TIPO DE FALLO
``` SQL
CREATE TABLE tipo_fallo (
    id_tipo_fallo CHAR(6) PRIMARY KEY,
    nom_tipo_fallo VARCHAR(50) NOT NULL
);
```
-Tabla: FALLO 
``` SQL
CREATE TABLE fallo (
    id_fallo CHAR(6) PRIMARY KEY,
    id_tipo_fallo CHAR(6) NOT NULL,
    id_herramienta CHAR(6) NOT NULL,
    descripcion_fallo VARCHAR(50),
    fecha_fallo DATE DEFAULT CURRENT_DATE,
	arreglado_fallo BOOLEAN DEFAULT FALSE,
    FOREIGN KEY (id_tipo_fallo) REFERENCES tipo_fallo(id_tipo_fallo),
    FOREIGN KEY (id_herramienta) REFERENCES herramienta(id_herramienta)
);
```
-Tabla: TIPO DE ESTÁNDAR
``` SQL
CREATE TABLE tipo_estandar (
    id_tipo_estandar CHAR(6) PRIMARY KEY,
    nom_tipo_estandar VARCHAR(200) NOT NULL
);
```
-Tabla: ESTADO DEL MANTENIMIENTO
``` SQL
CREATE TABLE estado_mantenimiento (
    id_estado_mantenimiento CHAR(6) PRIMARY KEY,
    nom_estado_mantenimiento VARCHAR(15) NOT NULL
);
```
-Tabla: TIPO DE MANTENIMIENTO
``` SQL
CREATE TABLE tipo_mantenimiento (
    id_tipo_mantenimiento CHAR(6) PRIMARY KEY,
    nom_tipo_mantenimiento VARCHAR(200)
);
```
-Tabla: MANTENIMIENTO DE LA HERRAMIENTA
``` SQL
CREATE TABLE mantenimiento_herramienta (
    id_mantenimiento CHAR(6) PRIMARY KEY,
    id_tipo_mantenimiento CHAR(6) NOT NULL,
    id_estado_mantenimiento CHAR(6) NOT NULL,
    fecha_mantenimiento DATE DEFAULT CURRENT_DATE,
    id_responsable CHAR(6),
    id_calidad CHAR(6) NOT NULL,
    id_fallo CHAR(6),
    descripcion_mantenimiento VARCHAR(200),
    FOREIGN KEY (id_tipo_mantenimiento) REFERENCES tipo_mantenimiento(id_tipo_mantenimiento),
    FOREIGN KEY (id_estado_mantenimiento) REFERENCES estado_mantenimiento(id_estado_mantenimiento),
    FOREIGN KEY (id_responsable) REFERENCES operario(id_operario),
    FOREIGN KEY (id_calidad) REFERENCES estandar_de_calidad(id_calidad),
    FOREIGN KEY (id_fallo) REFERENCES fallo(id_fallo)
);
```
-Tabla: TIPO DE INSUMO
``` SQL
CREATE TABLE tipo_insumo (
    id_tipo_insumo CHAR(6) PRIMARY KEY,
    nom_tipo_insumo VARCHAR(50) NOT NULL
);

```
-Tabla: SOLICITUD DE INSUMO
``` SQL
CREATE TABLE Solicitud_insumo (
    id_solicitud_insumo VARCHAR(10) NOT NULL,
    fecha_solicitud DATE DEFAULT CURRENT_DATE,
    id_gestor CHAR(6) NOT NULL,
    id_tipo_insumo CHAR(6) NOT NULL,
    cantidad_insumo INT NOT NULL,
    Nombre_provedor VARCHAR(50), 
    PRIMARY KEY (id_solicitud_insumo),
    FOREIGN KEY (id_gestor) REFERENCES gestor_produccion(id_gestor),
    FOREIGN KEY (id_tipo_insumo) REFERENCES tipo_insumo(id_tipo_insumo)
);
```



