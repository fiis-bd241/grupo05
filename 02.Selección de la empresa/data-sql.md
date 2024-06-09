# CREACIÓN DE TABLA

## CÓDIGO DE CREACIÓN

### TABLA: OPERARIO
``CREATE TABLE operario (
    id_operario CHAR(6) PRIMARY KEY,
    dni_operario CHAR(8),
    telefono_operario CHAR(9),
    prim_nom_op VARCHAR(50),
    prim_ape_op VARCHAR(50),
    seg_ape_op VARCHAR(50)
);``

### TABLA: INSUMO
``CREATE TABLE insumo (
    id_insumo CHAR(6) PRIMARY KEY,
    id_proveedor_ins VARCHAR(10),
    cantidad_insumo INT
);``

### TABLA: ESTANDAR DE CALIDAD
``CREATE TABLE estandar_de_calidad (
    id_calidad CHAR(6) PRIMARY KEY,
    tipo_estandar VARCHAR(20),
    descripcion_estandar VARCHAR(50)
);``

### TABLA: FALLO
``CREATE TABLE fallo (
    id_fallo CHAR(6) PRIMARY KEY,
    tipo_fallo VARCHAR(10),
    fecha_fallo DATE
);``



### TABLA: RECLAMO
``CREATE TABLE reclamo (
    id_reclamo CHAR(6) PRIMARY KEY,
    fecha_reclamo DATE,
    estado_reclamo VARCHAR(15),
    descripcion_reclamo VARCHAR(50),
    id_operario CHAR(6),
    FOREIGN KEY (id_operario) REFERENCES operario(id_operario)
);``

### TABLA: ACTIVIDAD
``CREATE TABLE actividad (
    id_actividad CHAR(6) PRIMARY KEY,
    tipo_actividad VARCHAR(50),
    fecha_actividad DATE,
    hora_ini_actividad TIME,
    hora_fin_actividad TIME,
    id_operario CHAR(6),
    FOREIGN KEY (id_operario) REFERENCES operario(id_operario)
);``

### TABLA: HERRAMIENTA MAQUINARIA
``CREATE TABLE herramienta_maquinaria (
    id_herramienta CHAR(6) PRIMARY KEY,
    id_proveedor_maq VARCHAR(10),
    id_almacen VARCHAR(15),
    tiempo_uso VARCHAR(50),
    id_operario CHAR(6),
    FOREIGN KEY (id_operario) REFERENCES operario(id_operario)
);``

### TABLA: OBSERVACIONES
``CREATE TABLE observaciones (
    id_obs CHAR(6) PRIMARY KEY,
    fecha_obs DATE,
    estado_obs VARCHAR(15),
    descripcion_obs VARCHAR(50),
    id_actividad CHAR(6),
    FOREIGN KEY (id_actividad) REFERENCES actividad(id_actividad)
);``

### TABLA: GESTOR DE PRODUCCIÓN
``CREATE TABLE gestor_de_produccion (
    id_gestor CHAR(6) PRIMARY KEY,
    dni_gestor CHAR(8),
    telefono_gestor CHAR(9),
    prim_nom_gestor VARCHAR(50),
    prim_ape_gestor VARCHAR(50),
    seg_ape_gestor VARCHAR(50)
);``

### TABLA: REPORTE
``CREATE TABLE reporte (
    id_reporte CHAR(6) PRIMARY KEY,
    tipo_reporte VARCHAR(50),
    fecha_reporte DATE,
    hora_reporte TIME,
    id_gestor CHAR(6),
    FOREIGN KEY (id_gestor) REFERENCES gestor_de_produccion(id_gestor)
);``

### TABLA: CATALOGO DE INSUMOS
``CREATE TABLE catalogo_insumos (
    id_catalogo_insumos CHAR(6) PRIMARY KEY,
    tipo_insumo VARCHAR(50),
    id_insumo CHAR(6),
    FOREIGN KEY (id_insumo) REFERENCES insumo(id_insumo)
);``

### TABLA: TALLER
``CREATE TABLE taller (
    id_taller CHAR(6) PRIMARY KEY,
    categoria_taller VARCHAR(50),
    id_catalogo_insumos CHAR(6),
    id_calidad CHAR(6),
    id_operario CHAR(6), 
	FOREIGN KEY (id_catalogo_insumos) REFERENCES catalogo_insumos(id_catalogo_insumos),
    FOREIGN KEY (id_calidad) REFERENCES estandar_de_calidad(id_calidad),
    FOREIGN KEY (id_operario) REFERENCES operario(id_operario)
);``

### TABLA: LOTE
``CREATE TABLE lote (
    id_lote CHAR(6) PRIMARY KEY,
    fecha_produccion DATE,
    id_taller CHAR(6),
    FOREIGN KEY (id_taller) REFERENCES taller(id_taller)
);``

### TABLA: SOLICITUD DE HERRAMIENTA
``CREATE TABLE solicitud_herramienta (
    id_solicitud CHAR(6) PRIMARY KEY,
    estado_solicitud VARCHAR(50),
    id_operario CHAR(6),
    id_gestor CHAR(6),
    FOREIGN KEY (id_operario) REFERENCES operario(id_operario),
    FOREIGN KEY (id_gestor) REFERENCES gestor_de_produccion(id_gestor)
);``

### TABLA: FALLO
``CREATE TABLE fallo (
    id_fallo CHAR(6) PRIMARY KEY,
    tipo_fallo VARCHAR(10),
    id_herramienta CHAR(6) REFERENCES herramienta_maquinaria(id_herramienta) ON DELETE CASCADE,
    descripcion_fallo CHAR(60) NOT NULL,
    fecha_fallo DATE
);
``
### TABLA: MANTENIMIENTO DE MAQUINARIA
``CREATE TABLE mantenimiento_maquinaria (
    id_mantenimiento CHAR(6) PRIMARY KEY,
    tipo_mantenimiento CHAR(2),
    estado_mantenimiento VARCHAR(15),
    fecha_mantenimiento DATE NOT NULL,
    id_responsable CHAR(6),
    id_calidad CHAR(6),
    id_fallo CHAR(6),
    descripcion_mantenimiento VARCHAR(70),
    FOREIGN KEY (id_responsable) REFERENCES operario(id_operario),
    FOREIGN KEY (id_calidad) REFERENCES estandar_de_calidad(id_calidad),
    FOREIGN KEY (id_fallo) REFERENCES fallo(id_fallo)
);``
## CÓDIGO DE LLENADO DE DATOS

### DATOS TABLA: OPERARIO
``INSERT INTO operario (id_operario, dni_operario, telefono_operario, prim_nom_op, prim_ape_op, seg_ape_op)
VALUES 
('OP001', '12345678', '912345678', 'Juan', 'Perez', 'Gomez'),
('OP002', '23456789', '923456789', 'Maria', 'Gonzalez', 'Lopez'),
('OP003', '34567890', '934567890', 'Pedro', 'Martinez', 'Sanchez');``

### DATOS TABLA: INSUMO
``INSERT INTO insumo (id_insumo, id_proveedor_ins, cantidad_insumo)
VALUES 
('INS001', 'PRV001', 100),
('INS002', 'PRV002', 150),
('INS003', 'PRV003', 200);``

### DATOS TABLA: ESTANDAR DE CALIDAD
``INSERT INTO estandar_de_calidad (id_calidad, tipo_estandar, descripcion_estandar)
VALUES 
('CAL001', 'ISO 11148-3', 'Requisitos de seguridad para herramientas portátiles accionadas neumáticamente'),
('CAL002', 'ISO 13849-1', 'Seguridad de las máquinas - Partes de sistemas de control relacionadas con la seguridad'),
('CAL003', 'ISO 17066', 'Requisitos para herramientas manuales no motorizadas');``


### DATOS TABLA: FALLO
``INSERT INTO fallo (id_fallo, tipo_fallo, fecha_fallo)
VALUES 
('FL001', 'Eléctrico', '2024-04-01'),
('FL002', 'Mecánico', '2024-04-15'),
('FL003', 'Hidráulico', '2024-04-20');``



### DATOS TABLA: RECLAMO
``INSERT INTO reclamo (id_reclamo, fecha_reclamo, estado_reclamo, descripcion_reclamo, id_operario)
VALUES 
('RC001', '2024-04-10', 'En proceso', 'Problema con la máquina', 'OP001'),
('RC002', '2024-04-20', 'Pendiente', 'Falla en la producción', 'OP002'),
('RC003', '2024-04-25', 'Completado', 'Reclamo solucionado', 'OP003');``

### DATOS TABLA: ACTIVIDAD
``INSERT INTO actividad (id_actividad, tipo_actividad, fecha_actividad, hora_ini_actividad, hora_fin_actividad, id_operario)
VALUES 
('ACT001', 'Producción', '2024-04-05', '08:00:00', '16:00:00', 'OP001'),
('ACT002', 'Mantenimiento', '2024-04-15', '09:00:00', '12:00:00', 'OP002'),
('ACT003', 'Inspección', '2024-04-20', '10:00:00', '14:00:00', 'OP003');``

### DATOS TABLA: HERRAMIENTA MAQUINARIA
``INSERT INTO herramienta_maquinaria (id_herramienta, id_proveedor_maq, id_almacen, tiempo_uso, id_operario)
VALUES 
('HRM001', 'PRV001', 'ALM001', '2 meses', 'OP001'),
('HRM002', 'PRV002', 'ALM002', '1 mes', 'OP002'),
('HRM003', 'PRV003', 'ALM003', '3 meses', 'OP003');``

### DATOS TABLA: OBSERVACIONES
``INSERT INTO observaciones (id_obs, fecha_obs, estado_obs, descripcion_obs, id_actividad)
VALUES 
('OBS001', '2024-04-05', 'En proceso', 'Necesita más supervisión', 'ACT001'),
('OBS002', '2024-04-15', 'Pendiente', 'Requiere más piezas', 'ACT002'),
('OBS003', '2024-04-20', 'Completado', 'Tareas realizadas correctamente', 'ACT003');``

### DATOS TABLA: GESTOR DE PRODUCCIÓN
``INSERT INTO gestor_de_produccion (id_gestor, dni_gestor, telefono_gestor, prim_nom_gestor, prim_ape_gestor, seg_ape_gestor)
VALUES 
('GES001', '98765432', '978654321', 'Luis', 'Lopez', 'Perez'),
('GES002', '87654321', '967543210', 'Ana', 'Ramirez', 'Garcia'),
('GES003', '76543210', '956432109', 'Carlos', 'Sanchez', 'Gomez');``

### DATOS TABLA: REPORTE
``INSERT INTO reporte (id_reporte, tipo_reporte, fecha_reporte, hora_reporte, id_gestor)
VALUES 
('REP001', 'Producción', '2024-04-05', '08:30:00', 'GES001'),
('REP002', 'Mantenimiento', '2024-04-15', '10:00:00', 'GES002'),
('REP003', 'Inspección', '2024-04-20', '11:30:00', 'GES003');``

### DATOS TABLA: CATALOGO INSUMOS
``INSERT INTO catalogo_insumos (id_catalogo_insumos, tipo_insumo, id_insumo)
VALUES 
('CAT001', 'Herramienta', 'INS001'),
('CAT002', 'Repuesto', 'INS002'),
('CAT003', 'Material', 'INS003');``

### DATOS TABLA: TALLER
``INSERT INTO taller (id_taller, categoria_taller, id_catalogo_insumos, id_calidad, id_operario)
VALUES 
('TAL001', 'Producción', 'CAT001', 'CAL001', 'OP001'),
('TAL002', 'Mantenimiento', 'CAT002', 'CAL002', 'OP002'),
('TAL003', 'Inspección', 'CAT003', 'CAL003', 'OP003');``

### DATOS TABLA: LOTE
``INSERT INTO lote (id_lote, fecha_produccion, id_taller)
VALUES 
('LOT001', '2024-04-05', 'TAL001'),
('LOT002', '2024-04-15', 'TAL002'),
('LOT003', '2024-04-20', 'TAL003');``

### DATOS TABLA: SOLICITUD DE HERRAMIENTA
``INSERT INTO solicitud_herramienta (id_solicitud, estado_solicitud, id_operario, id_gestor)
VALUES 
('SOL001', 'En proceso', 'OP001', 'GES001'),
('SOL002', 'Pendiente', 'OP002', 'GES002'),
('SOL003', 'Completado', 'OP003', 'GES003');``

### DATOS TABLA: FALLO
``INSERT INTO fallo (id_fallo, tipo_fallo, id_herramienta, descripcion_fallo, fecha_fallo) 
VALUES  
('FL001', 'Eléctrico', 'HRM001', 'Fallo eléctrico en la máquina de coser recta', '2024-04-01'),
('FL002', 'Mecánico', 'HRM002', 'Fallo mecánico en la máquina overlock', '2024-04-15'),
('FL003', 'Hidráulico', 'HRM003', 'Fallo hidráulico en la máquina de bordar', '2024-04-20');
;``
### DATOS TABLA: MANTENIMIENTO DE MAQUINARIA
``INSERT INTO mantenimiento_de_maquinaria (id_mantenimiento, tipo_mantenimiento, estado_mantenimiento, fecha_mantenimiento, id_responsable, id_calidad, id_fallo, descripcion_mantenimiento)
VALUES  
('MNT001', 'M1', 'En proceso', '2024-04-05', 'OP001', 'CAL001', 'FL001', 'Mantenimiento preventivo para resolver el fallo eléctrico en la máquina de coser recta'),
('MNT002', 'M2', 'Pendiente', '2024-04-17', 'OP002', 'CAL002', 'FL002', 'Mantenimiento correctivo para reparar el fallo mecánico en la máquina overlock');
``


