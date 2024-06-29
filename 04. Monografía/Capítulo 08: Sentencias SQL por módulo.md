# Sentencias SQL

# Prototipo 1: Interfaz de Registro de Solicitudes de Herramientas por Operario
### Código Requerimiento: R-001
### Código Interfaz: I-001
### Imagen Interfaz: (imagen ilustrativa) 

![image](https://github.com/fiis-bd241/grupo05/assets/164263389/07b588b8-4c82-4303-b251-ade0f1059cd8)

 
### Descripción: Esta interfaz permite a un operario registrar una nueva solicitud de herramienta.
## Sentencias SQL
### Eventos
### 1- Carga de Página: Se llenará la lista de herramientas por código de herramienta o nombre de herramienta para seleccionar.
### Por código de herramienta :
SELECT id_herramienta FROM herramienta; 
### Por nombre de herramienta:
SELECT nombre_herramienta FROM herramienta; 
### 2-Boton buscar:  Cuando el usuario oprima el botón buscar se llenará la grilla de resultados utilizando la siguiente sentencia
### Por código de herramienta :
||
  |-------------------------------------|
  |  codigo:  
      SELECT id_herramienta, nombre_herramienta, modelo, nombre_proveedor
      FROM herramienta
      WHERE id_herramienta = <3> AND disponible = TRUE;
      
### Por nombre de herramienta:
||
  |-------------------------------------|
  |  codigo:  
      SELECT id_herramienta, nombre_herramienta, modelo, nombre_proveedor
      FROM herramienta
      WHERE nombre_herramienta ILIKE '%' || <3> || '%' AND disponible = TRUE;
      
### 3-Botón Registrar Solicitud: Agregar una nueva solicitud de herramienta.
||
  |-------------------------------------|
  |  codigo:  
     INSERT INTO solicitud_herramienta (id_est_soli_herra, fecha_solicitud, id_operario,id_herramienta)
     VALUES ('EHE1', CURRENT_TIMESTAMP, <1> ,<2>);

|Donde:|
|--------------------------------------------|
|<1> es el ID del operario que realiza la solicitud. |
|<2> es el ID de la herramienta seleccionada. |
|<3> es el nombre de la herramienta seleccionada. |

 
## Prototipo 2: Interfaz de Visualización de Herramientas y Solicitudes por Operario
### Código Requerimiento: R-002
### Código Interfaz: I-002
### Imagen Interfaz:  (imagen ilustrativa)

![image](https://github.com/fiis-bd241/grupo05/assets/164263389/031f2bf6-b653-4ccb-935d-a61d29d486ce)


### Descripción: Esta interfaz permite a un operario visualizar todas sus solicitudes y las herramientas disponibles.
## Sentencias SQL
### Eventos
### 1-Carga de Página: Mostrar solicitudes del operario.

  ||
  |-------------------------------------|
  |codigo:
    SELECT 
     s.id_solicitud, 
     s.fecha_solicitud, 
     s.id_est_soli_herra, 
     h.nombre_herramienta, 
     h.modelo
     FROM 
      solicitud_herramienta s
     JOIN 
      herramienta h ON s.id_herramienta = h.id_herramienta
     WHERE 
       s.id_operario = <1>
     ORDER BY 
       s.fecha_solicitud DESC;
    
|Donde:|
|-------------------------------------|
| <1> es el ID del operario autenticado. |


 ## Prototipo 3: Interfaz de Aprobación de Solicitudes por Gestor
### Código Requerimiento: R-003
### Código Interfaz: I-003
### Imagen Interfaz:  (imagen ilustrativa)
![image](https://github.com/fiis-bd241/grupo05/assets/164263389/447514c4-6af7-40c3-8c78-8ca7b706fd6a)

 
### Descripción: Esta interfaz permite a un gestor ver las solicitudes pendientes y aprobar o rechazar las solicitudes.

## Sentencias SQL:
### Eventos
### 1-Carga de Página: Mostrar solicitudes pendientes.
||
  |-------------------------------------|
  |  codigo:  
      SELECT 
       s.id_solicitud, 
       o.prim_nom_op || ' ' || o.seg_nom_op || ' ' || o.prim_ape_op || ' ' || o.seg_ape_op AS nombre_completo_operario,
       h.modelo,
       h.nombre_herramienta
    
      FROM 
       solicitud_herramienta s
      JOIN 
       operario o ON s.id_operario = o.id_operario
      JOIN 
       herramienta h ON s.id_herramienta = h.id_herramienta
      WHERE 
       s.id_est_soli_herra = 'EHE1';
    
### 2-Botón Buscar: Buscar solicitudes por nombre y apellido del operario.
||
  |-------------------------------------|
  |  codigo:  
      SELECT 
        s.id_solicitud, 
        o.prim_nom_op || ' ' || o.seg_nom_op || ' ' || o.prim_ape_op || ' ' || o.seg_ape_op AS nombre_completo_operario,
        h.modelo,
        h.nombre_herramienta,
        s.id_est_soli_herra
      FROM 
        solicitud_herramienta s
      JOIN 
       operario o ON s.id_operario = o.id_operario
      JOIN 
       herramienta h ON s.id_herramienta = h.id_herramienta
      WHERE 
       s.id_est_soli_herra = 'EHE1' AND
      (o.prim_nom_op || ' ' || o.seg_nom_op || ' ' || o.prim_ape_op || ' ' || o.seg_ape_op) ILIKE '%' || <3> || '%';


|Donde:|
|--------------------------------------------|
|<1> es la cadena de búsqueda ingresada por el gestor (nombre y apellido del operario).|

### 3-Botón Aprobar Solicitud: Aprobar una solicitud pendiente.
||
  |-------------------------------------|
  |  codigo:  
      UPDATE solicitud_herramienta
      SET id_est_soli_herra = 'EHE2', fecha_solicitud = CURRENT_TIMESTAMP, id_gestor = <1>
      WHERE id_solicitud = <2>;

### 4-Botón Rechazar Solicitud: Rechazar una solicitud pendiente.
||
  |-------------------------------------|
  |  codigo:  
      UPDATE solicitud_herramienta
      SET id_est_soli_herra = 'EHE3', fecha_solicitud = CURRENT_TIMESTAMP, id_gestor = <1>
      WHERE id_solicitud = <2>;
|Donde:|
|--------------------------------------------|
|<1> es el ID del gestor que toma la acción.|
|<2> es el ID de la solicitud seleccionada.|

 ## Prototipo 4: Interfaz de Muestra de bonificación de pago
### Código Requerimiento: R-004
### Código Interfaz: I-004
### Imagen Interfaz: (imagen ilustrativa) 

### Descripción: Esta interfaz permite a un operario visualizar las bonificaciones que ha percibido dentro de su ciclo de remuneración.
## Sentencias SQL
### Eventos
### 1- Carga de Página: Se llenará la lista de bonificaciones por código de bonificación o monto de bonificación para seleccionar.
### Por código de bonificación:
SELECT id_bonificacion FROM bonificacion;
### Por monto de bonificación:
SELECT monto_bonificacion FROM bonificacion;
### 2- Botón buscar: Cuando el usuario oprima la opción de buscar se llenará la grilla de resultados
### 3- Cálculo final: Estos datos son usados posteriormente en la tabla de bonificación para determinar la remuneración total


 ## Prototipo 5: Interfaz de Muestra de deducción de pago
### Código Requerimiento: R-005
### Código Interfaz: I-005
### Imagen Interfaz: (imagen ilustrativa) 

### Descripción: Esta interfaz permite a un operario visualizar las deducciones que ha percibido dentro de su ciclo de remuneración.
## Sentencias SQL
### Eventos
### 1- Carga de Página: Se llenará la lista de deducciones por código de deducción o monto de deducción para seleccionar.
### Por código de deducción:
SELECT id_deduccion FROM deduccion;
### Por monto de deducción:
SELECT monto_deduccion FROM deduccion;
### 2- Botón buscar: Cuando el usuario oprima la opción de buscar se llenará la grilla de resultados
### 3- Cálculo final: Estos datos son usados posteriormente en la tabla de deducción para determinar la remuneración total

 ## Prototipo 6: Interfaz de Muestra de remuneración total de pago
### Código Requerimiento: R-006
### Código Interfaz: I-006
### Imagen Interfaz: (imagen ilustrativa)

### Descripción: Esta interfaz permite a un operario visualizar el total de su remuneración dentro de su ciclo de pago, además revisar datos adicionales de su nómina.
## Sentencias SQL
### Eventos
### 1- Carga de página: Se llenará la lista de remuneraciones por todos los pagos que se le haya hecho al operario, se puede buscar por el id de la nómina, por el total de pago o por la fecha de emisión
### Por id de la nómina:
### SELECT id_nomina FROM nomina;
### Por el total de pago:
### SELECT total_pago FROM nomina;
### Por la fecha de pago:
### SELECT fecha_emision FROM nomina;


# MODULO REGISTRO DE ACTIVIDADES

 ## Prototipo 7: Interfaz de Asignación de actividades
### Código Requerimiento: R-007
### Código Interfaz: I-007
### Imagen Interfaz: (imagen ilustrativa)
![image](https://github.com/fiis-bd241/grupo05/assets/164263389/3b859c2d-f386-41e1-bf99-9327a54eb1db)


### Descripción: Esta interfaz permite a un operario visualizar el proceso para asignar una actividad a un operario.

## Sentencias SQL:
### Eventos:
### 1- Boton  Asignar Actividad: Se agregará un nuevo registro a la tabla de asignación de actividad.
||
  |-------------------------------------|
  |  codigo:  
      INSERT INTO asignacion_actividad (fecha_asig, hora_inicio, hora_fin, id_asignacion, id_gestor, id_lote, id_actividad, id_operario, id_est_actividad)
      VALUES (<1>, <2>, 'ASI1' , <3>, <4>, <5>, <6>, <7>, 'EST4');
|Donde:|
|--------------------------------------------|
|<1> es el fecha de elaborar la actividad.|
|<2> es el hora de inicio.|
|<3> es el hora de fin.|
|<4> es el ID del gestor que está asignando.|
|<5> es el ID del lote a elaborar.|
|<6> es el ID del la actividad que se realizará.|
|<7> es el ID del operario que realizará la actividad.|

 ## Prototipo 8: Interfaz de Envío de Verificación de Actividad
### Código Requerimiento: R-008
### Código Interfaz: I-008
### Imagen Interfaz: (imagen ilustrativa)
![image](https://github.com/fiis-bd241/grupo05/assets/164263389/6f393373-dd7b-4963-ab03-e0e1eb72d751)

### Descripción: Esta interfaz permitir a un operario enviar una verificación de una actividad al gestor de producción para su revisión.

## Sentencias SQL:
### Eventos:
### 1- Cargar página: Se mostrará la tabla de asignacion de actividades ya mandadas a revisión.
||
  |-------------------------------------|
  |  codigo:  
      SELECT 
    aa.fecha_asig,
    aa.hora_inicio,
    aa.hora_fin,
    aa.id_gestor,
    aa.id_lote,
    aa.id_actividad,
    aa.id_operario,
    aa.id_est_actividad,
    o.id_taller
    FROM 
    asignacion_actividad aa
     JOIN 
    operario o ON aa.id_operario = o.id_operario
     WHERE 
    aa.id_est_actividad = 'EST4';

      
### 2- Botón seleccionar: Se escogera una id de asignación de actividad.
||
  |-------------------------------------|
  |  codigo:  
      SELECT id_asignacion;
      
### 3- Boton  Enviar a revisión: Se modificara un nueva registro a la tabla de asignación de actividad.
||
  |-------------------------------------|
  |  codigo:  
      UPDATE asignacion_actividad
      SET id_est_actividad = 'EST3'
      WHERE id_asignacion = <1>;

|Donde:|
|--------------------------------------------|
|<1> es el ID de asignación de actividad.|

 ## Prototipo 9: Interfaz de Auditoria de actividades
### Código Requerimiento: R-009
### Código Interfaz: I-009
### Imagen Interfaz: (imagen ilustrativa)
![image](https://github.com/fiis-bd241/grupo05/assets/164263389/f3b954c4-7135-4e8a-a669-bed110b1e73d)


### Descripción: Esta interfaz permitir a un gestor de producción dar un visto bueno a una actividad para indicar que ha sido realizada correctamente por un operario.

## Sentencias SQL:
### Eventos:
### 1- Carga de página: Se mostrará la tabla de asignacion de actividades ya mandadas a revisión.
||
  |-------------------------------------|
  |  codigo:  
      SELECT aa.*, o.id_taller
      FROM asignacion_actividad aa
      JOIN operario o ON aa.id_operario = o.id_operario
      WHERE aa.id_est_actividad = 'EST3';

### 2- Boton de selección: Se escogera una asignación.
||
  |-------------------------------------|
  |  codigo:  
      SELECT id_asignacion;
    
### 3- Boton  Aprobar: Se modificara un nueva registro a la tabla de asignación de actividad.
||
  |-------------------------------------|
  |  codigo:  
      UPDATE asignacion_actividad
      SET id_est_actividad = 'EST2'
      WHERE id_asignacion = <1>;
 
### 4- Boton  Rehacer actividad: Se modificara un nueva registro a la tabla de asignación de actividad.
||
  |-------------------------------------|
  |  codigo:  
      UPDATE asignacion_actividad
      SET id_est_actividad = 'EST4'
      SET hora_inicio = <2>;
      SET hora_inicio = <3>;
      WHERE id_asignacion = <1>;
|Donde:|
|--------------------------------------------|
|<1> es el ID de asignación de actividad.|
|<2> es la hora de inicio de actividad.|
|<3> es la hora de fin de actividad.|

 ## Prototipo 10: Interfaz de Registro de Reclamos
### Código Requerimiento: R-010
### Código Interfaz: I-010
### Imagen Interfaz: (imagen ilustrativa) 
<img src="../02.Selección de la empresa/PC3/InterfazReclamosOp1.png" alt="PC3" style="width: 120%; height: auto;" />
<img src="../02.Selección de la empresa/PC3/InterfazReclamosOp2.png" alt="PC3" style="width: 120%; height: auto;" />

### Descripción: Esta interfaz permite a un operario registrar un reclamo.

## Sentencias SQL
### Eventos
### 1- Registrar un reclamo: Agregar un nuevo reclamo.

  ||
  |-------------------------------------|
  |codigo:
    INSERT INTO reclamo (id_reclamo, fecha_reclamo, id_estado_reclamo, id_descrip_reclamo, id_operario)
    VALUES ('RC001', '2024-04-10', 'En proceso', 'Problema con la máquina', <1>);
    
|Donde:|
|-------------------------------------|
| <1> es el ID del operario autenticado. |

 ## Prototipo 11: Interfaz de Visualización de Reclamos
### Código Requerimiento: R-011
### Código Interfaz: I-011
### Imagen Interfaz: (imagen ilustrativa) 
<img src="../02.Selección de la empresa/PC3/InterfazReclamosGp.png" alt="PC3" style="width: 120%; height: auto;" />

### Descripción: Esta interfaz permite al gestor de producción visualizar los reclamos realizados por los operarios.

## Sentencias SQL
### Eventos
### 1- Carga de Página: Se llenará la lista de reclamos por código de reclamo, código de operario, fecha de reclamo o estado del reclamo para seleccionar.
### Por código de reclamo :
SELECT id_reclamo FROM reclamo;
### Por código de operario :
SELECT id_operario FROM reclamo; 
### Por fecha de reclamo:
SELECT fecha_reclamo FROM reclamo;
### Por estado de reclamo:
SELECT id_estado_reclamo FROM reclamo;
### 2-Boton buscar:  Cuando el gestor oprima el botón buscar, se llenará la grilla de resultados utilizando la siguiente sentencia
### Por código de reclamo :
||
  |-------------------------------------|
  |  codigo:  
      SELECT fecha_reclamo, id_reclamo, id_operario, id_descrip_reclamo, id_estado_reclamo
      FROM reclamo
      WHERE id_reclamo = <1>;

### Por código de operario :
||
  |-------------------------------------|
  |  codigo:  
      SELECT fecha_reclamo, id_reclamo, id_operario, id_descrip_reclamo, id_estado_reclamo
      FROM reclamo
      WHERE id_operario = <2>;

### Por fecha de reclamo :
||
  |-------------------------------------|
  |  codigo:  
      SELECT fecha_reclamo, id_reclamo, id_operario, id_descrip_reclamo, id_estado_reclamo
      FROM reclamo
      WHERE fecha_reclamo = <3>;

### Por estado de reclamo :
||
  |-------------------------------------|
  |  codigo:  
      SELECT fecha_reclamo, id_reclamo, id_operario, id_descrip_reclamo, id_estado_reclamo
      FROM reclamo
      WHERE id_estado_reclamo = <4>;

|Donde:|
|--------------------------------------------|
|<1> es el ID del reclamo seleccionado.|
|<2> es el ID del operario que realizó el reclamo.|
|<3> es la fecha del reclamo seleccionado.|
|<4> es el estado del reclamo seleccionado.|

 ## Prototipo 12: Interfaz de Visualización de Observaciones
### Código Requerimiento: R-012
### Código Interfaz: I-012
### Imagen Interfaz: (imagen ilustrativa) 
<img src="InterfazObservaciones.png" alt="PC3" style="width: 120%; height: auto;" />

### Descripción: Esta interfaz permite al gestor de producción visualizar el total de observaciones realizadas.

## Sentencias SQL
### Eventos
### 1- Carga de Página: Se llenará la lista de observaciones por código de observación, código de actividad, fecha de la observación o estado de la observación para seleccionar.
### Por código de observación :
SELECT id_observacion FROM observacion;
### Por código de operario :
SELECT id_asignacion FROM observacion; 
### Por fecha de reclamo:
SELECT fecha_observacion FROM observacion;
### Por estado de reclamo:
SELECT id_estado_observacion FROM observacion;
### 2-Boton buscar:  Cuando el gestor oprima el botón buscar, se llenará la grilla de resultados utilizando la siguiente sentencia
### Por código de observación :
||
  |-------------------------------------|
  |  codigo:  
      SELECT fecha_observacion, id_observacion, id_asignacion, id_descrip_observacion, id_estado_observacion
      FROM observacion
      WHERE id_observacion = <1>;

### Por código de actividad :
||
  |-------------------------------------|
  |  codigo:  
      SELECT fecha_observacion, id_observacion, id_asignacion, id_descrip_observacion, id_estado_observacion
      FROM observacion
      WHERE id_asignacion = <2>;

### Por fecha de observación :
||
  |-------------------------------------|
  |  codigo:  
      SELECT fecha_observacion, id_observacion, id_asignacion, id_descrip_observacion, id_estado_observacion
      FROM observacion
      WHERE fecha_observacion = <3>;

### Por estado de observación :
||
  |-------------------------------------|
  |  codigo:  
      SELECT fecha_observacion, id_observacion, id_asignacion, id_descrip_observacion, id_estado_observacion
      FROM observacion
      WHERE id_estado_observacion = <4>;

|Donde:|
|--------------------------------------------|
|<1> es el ID de la observación seleccionada.|
|<2> es el ID de la actividad relacionada a la observación.|
|<3> es la fecha de la observación seleccionada.|
|<4> es el estado de la observación seleccionada.|

#### MODULO REPORTE
 ## Prototipo : Reportes
### Código Requerimiento: R-000
### Código Interfaz: I-000
### Imagen Interfaz: (imagen ilustrativa) 
 
### Descripción: Esta interfaz permite a un gestor de la producción revisar los reportes para los reclamos y las herramientas

### HERRAMIENTAS: Se puede consultar de 3 diferentes formas: por nombre, proveedor y modelo
### RECLAMOS: Se puede consultar por las formas de id_operario, fecha_reclamo, estado del reclamo y el tipo de descripción de reclamo




 ## Prototipo 13: Mantenimiento Preventivo e Inspecciones de Calidad
### Código Requerimiento: R-013
### Código Interfaz: I-013
### Imagen Interfaz: (imagen ilustrativa) 
### Descripción:Esta interfaz sirve para gestionar y asegurar la calidad y mantenimiento de las herramientas y maquinarias utilizadas en la producción textil.
### 1- Carga de Página:Para la programación de mantenimiento de herramientas y maquinaria, al cargar la página, se debe llenar la lista de opciones disponibles para la selección.
### Seleccionar Tipos de Mantenimiento:
||
  |-------------------------------------|
  |  codigo:  
      SELECT 'M1' AS tipo_mantenimiento, 'Preventivo' AS descripcion
      UNION
      SELECT 'M2' AS tipo_mantenimiento, 'Correctivo' AS descripcion;

### Seleccionar Herramientas/Maquinarias:
||
  |-------------------------------------|
  |  codigo:  
      SELECT id_herramienta, nombre_herramienta FROM herramienta;

### 2-Boton buscar:  Cuando el gestor oprima el botón buscar, se llenará la grilla de resultados utilizando la siguiente sentencia:
### Por ID de Mantenimiento:
||
  |-------------------------------------|
  |  codigo:  
      SELECT id_mantenimiento, tipo_mantenimiento, estado_mantenimiento, fecha_mantenimiento, id_responsable, id_calidad, id_fallo, descripcion_mantenimiento
      FROM mantenimiento_de_maquinaria
      WHERE id_mantenimiento = '<ID_MANTENIMIENTO>';
### Por ID de Herramienta/Maquinaria:
||
  |-------------------------------------|
  |  codigo:
      SELECT id_mantenimiento, tipo_mantenimiento, estado_mantenimiento, fecha_mantenimiento, id_responsable, id_calidad, id_fallo, descripcion_mantenimiento
      FROM mantenimiento_de_maquinaria
      WHERE id_herramienta = '<ID_HERRAMIENTA>';
     
### Por Fecha de Mantenimiento:
||
  |-------------------------------------|
  |  codigo:
      SELECT id_mantenimiento, tipo_mantenimiento, estado_mantenimiento, fecha_mantenimiento, id_responsable, id_calidad, id_fallo, descripcion_mantenimiento
      FROM mantenimiento_de_maquinaria
      WHERE fecha_mantenimiento = '<FECHA_MANTENIMIENTO>';

### Por Estado de Mantenimiento:
||
  |-------------------------------------|
  |  codigo:
      SELECT id_mantenimiento, tipo_mantenimiento, estado_mantenimiento, fecha_mantenimiento, id_responsable, id_calidad, id_fallo, descripcion_mantenimiento
      FROM mantenimiento_de_maquinaria
      WHERE estado_mantenimiento = '<ESTADO_MANTENIMIENTO>';

### Por ID de Inspección:
||
  |-------------------------------------|
  |  codigo:
      SELECT id_inspeccion, id_herramienta, fecha_inspeccion, resultado, observaciones
      FROM inspecciones_de_calidad
      WHERE id_inspeccion = '<ID_INSPECCION>';


### Por ID de Herramienta/Maquinaria (Inspección):
||
  |-------------------------------------|
  |  codigo:
      SELECT id_inspeccion, id_herramienta, fecha_inspeccion, resultado, observaciones
      FROM inspecciones_de_calidad
      WHERE id_herramienta = '<ID_HERRAMIENTA>';


### 3 Boton Historial: Cuando el gestor oprima el botón historial, se mostrara todo los Mantenimientos e Inspecciones de dicha herrmaienta.

### Por Tipo (Mantenimiento/Inspección):
||
  |-------------------------------------|
  |  codigo:

    SELECT 'Mantenimiento' AS tipo, id_mantenimiento AS id, id_herramienta, fecha_mantenimiento AS fecha, estado_mantenimiento AS estado 
    FROM mantenimiento_de_maquinaria
    UNION
    SELECT 'Inspección' AS tipo, id_inspeccion AS id, id_herramienta, fecha_inspeccion AS fecha, resultado AS estado 
    FROM inspecciones_de_calidad;

### Por Herramienta/Maquinaria:
||
  |-------------------------------------|
  |  codigo:
      SELECT nombre_herramienta FROM herramienta WHERE id_herramienta = '<ID_HERRAMIENTA>';
 
### 3-Boton Acciones (Editar, Eliminar):
### Editar Mantenimiento:
||
  |-------------------------------------|
  |  codigo:
      UPDATE mantenimiento_de_maquinaria 
      SET tipo_mantenimiento = '<TIPO_MANTENIMIENTO>', estado_mantenimiento = '<ESTADO>', fecha_mantenimiento = '<FECHA>', id_responsable = '<ID_RESPONSABLE>', id_calidad = '<ID_CALIDAD>', id_fallo = '<ID_FALLO>', descripcion_mantenimiento = '<DESCRIPCION>'
      WHERE id_mantenimiento = '<ID_MANTENIMIENTO>';
### Editar Mantenimiento:
||
  |-------------------------------------|
  |  codigo:
      UPDATE mantenimiento_de_maquinaria 
      SET tipo_mantenimiento = '<TIPO_MANTENIMIENTO>', estado_mantenimiento = '<ESTADO>', fecha_mantenimiento = '<FECHA>', id_responsable = '<ID_RESPONSABLE>', id_calidad = '<ID_CALIDAD>', id_fallo = '<ID_FALLO>', descripcion_mantenimiento = '<DESCRIPCION>'
      WHERE id_mantenimiento = '<ID_MANTENIMIENTO>';

### Eliminar Mantenimiento:
||
  |-------------------------------------|
  |  codigo:
      DELETE FROM mantenimiento_de_maquinaria WHERE id_mantenimiento = '<ID_MANTENIMIENTO>';

### Editar Inspección:
||
  |-------------------------------------|
  |  codigo:
      UPDATE inspecciones_de_calidad 
      SET id_herramienta = '<ID_HERRAMIENTA>', fecha_inspeccion = '<FECHA>', resultado = '<RESULTADO>', observaciones = '<OBSERVACIONES>'
      WHERE id_inspeccion = '<ID_INSPECCION>';
### Eliminar Inspección:
||
  |-------------------------------------|
  |  codigo:
      DELETE FROM inspecciones_de_calidad WHERE id_inspeccion = '<ID_INSPECCION>';



