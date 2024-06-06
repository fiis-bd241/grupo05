
# Prototipo 1: Interfaz de Registro de Solicitudes de Herramientas por Operario
### Código Requerimiento: R-001
### Código Interfaz: I-001
### Imagen Interfaz: (imagen ilustrativa) 
<img src="Group 3.png" alt="02.Selección de la empresa" style="width: 120%; height: auto;" />
 
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
<img src="Group 4.png" alt="02.Selección de la empresa" style="width: 120%; height: auto;" />
### Descripción: Esta interfaz permite a un operario visualizar todas sus solicitudes y las herramientas disponibles.
## Sentencias SQL:
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
<img src="interfaz 10.1.png" alt="02.Selección de la empresa" style="width: 120%; height: auto;" />
 
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

# Prototipo : Interfaz de Muestra de bonificación de pago
### Código Requerimiento: R-R01
### Código Interfaz: I-R01
### Imagen Interfaz: (imagen ilustrativa) 

### Descripción: Esta interfaz permite a un operario visualizar las bonificaciones que ha percibido dentro de su ciclo de remuneración.
### Eventos:
### 1- Carga de Página: Se llenará la lista de bonificaciones por código de bonificación o monto de bonificación para seleccionar.
### Por código de bonificación:
SELECT id_bonificacion FROM bonificacion;
### Por monto de bonificación:
SELECT monto_bonificacion FROM bonificacion;
### 2- Botón buscar: Cuando el usuario oprima la opción de buscar se llenará la grilla de resultados
### 3- Cálculo final: Estos datos son usados posteriormente en la tabla de bonificación para determinar la remuneración total


# Prototipo : Interfaz de Muestra de deducción de pago
### Código Requerimiento: R-D01
### Código Interfaz: I-D01
### Imagen Interfaz: (imagen ilustrativa) 

### Descripción: Esta interfaz permite a un operario visualizar las deducciones que ha percibido dentro de su ciclo de remuneración.
### Eventos:
### 1- Carga de Página: Se llenará la lista de deducciones por código de deducción o monto de deducción para seleccionar.
### Por código de deducción:
SELECT id_deduccion FROM deduccion;
### Por monto de deducción:
SELECT monto_deduccion FROM deduccion;
### 2- Botón buscar: Cuando el usuario oprima la opción de buscar se llenará la grilla de resultados
### 3- Cálculo final: Estos datos son usados posteriormente en la tabla de deducción para determinar la remuneración total

# Prototipo : Interfaz de Muestra de remuneración total de pago
### Código Requerimiento: R-R01
### Código Interfaz: I-R01
### Imagen Interfaz: (imagen ilustrativa)
### Descripción: Esta interfaz permite a un operario visualizar el total de su remuneración dentro de su ciclo de pago, además revisar datos adicionales de su nómina.
### Eventos:
### 1- Carga de página: Se llenará la lista de remuneraciones por todos los pagos que se le haya hecho al operario, se puede buscar por el id de la nómina, por el total de pago o por la fecha de emisión
### Por id de la nómina:
### SELECT id_nomina FROM nomina;
### Por el total de pago:
### SELECT total_pago FROM nomina;
### Por la fecha de pago:
### SELECT fecha_emision FROM nomina;


# MODULO REGISTRO DE ACTIVIDADES

# Prototipo: Interfaz de Asignación de actividades
### Código Requerimiento: Caso de uso N°15
### Código Interfaz: IMG1
### Imagen Interfaz: (imagen ilustrativa)
<img src="asig.png" alt="02.Selección de la empresa" style="width: 120%; height: auto;" />

### Descripción: Esta interfaz permite a un operario visualizar el proceso para asignar una actividad a un operario.

## Sentencia SQL:
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

# Prototipo: Interfaz de Envío de Verificación de Actividad
### Código Requerimiento: Caso de uso N°16
### Código Interfaz: IMG2
### Imagen Interfaz: (imagen ilustrativa)
<img src="veri.png" alt="02.Selección de la empresa" style="width: 120%; height: auto;" />

### Descripción: Esta interfaz permitir a un operario enviar una verificación de una actividad al gestor de producción para su revisión.

## Sentencia SQL:
### Eventos:
### 1- Cargar página: Se mostrará la tabla de asignacion de actividades ya mandadas a revisión.
||
  |-------------------------------------|
  |  codigo:  
      SELECT *
      FROM asignacion_actividad
      WHERE id_est_actividad = 'EST4';
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

# Prototipo: Interfaz de Auditoria de actividades
### Código Requerimiento: Caso de uso N°17
### Código Interfaz: IMG3
### Imagen Interfaz: (imagen ilustrativa)
<img src="audi.png" alt="02.Selección de la empresa" style="width: 120%; height: auto;" />
<img src="rehacer.png" alt="02.Selección de la empresa" style="width: 120%; height: auto;" />

### Descripción: Esta interfaz permitir a un gestor de producción dar un visto bueno a una actividad para indicar que ha sido realizada correctamente por un operario.

## Sentencia SQL:
### Eventos:
### 1- Carga de página: Se mostrará la tabla de asignacion de actividades ya mandadas a revisión.
||
  |-------------------------------------|
  |  codigo:  
      SELECT *
      FROM asignacion_actividad
      WHERE id_est_actividad = 'EST3';

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

# Prototipo: Interfaz de Registro de Reclamos
### Código Requerimiento: R-005
### Código Interfaz: I-005
### Imagen Interfaz: (imagen ilustrativa) 
<img src="interfaz reclamos op1 mejorado.png" alt="02.Selección de la empresa" style="width: 120%; height: auto;" />

### Descripción: Esta interfaz permite a un operario registrar un reclamo.

## Sentencias SQL:
### 1-Registrar un reclamo: Agregar un nuevo reclamo.

  ||
  |-------------------------------------|
  |codigo:
    INSERT INTO reclamo (id_reclamo, fecha_reclamo, estado_reclamo, descripcion_reclamo, id_operario) VALUES  ('RC001', '2024-04-10', 'En proceso', 'Problema con la máquina', <1>);
    
|Donde:|
|-------------------------------------|
| <1> es el ID del operario autenticado. |

#MODULO REPORTE
# Prototipo: Reportes
### Código Requerimiento: R-001
### Código Interfaz: I-001
### Imagen Interfaz: (imagen ilustrativa) 
 
### Descripción: Esta interfaz permite a un gestor de la producción revisar los reportes para los reclamos y las herramientas

### HERRAMIENTAS: Se puede consultar de 3 diferentes formas: por nombre, proveedor y modelo
### RECLAMOS: Se puede consultar por las formas de id_operario, fecha_reclamo, estado del reclamo y el tipo de descripción de reclamo
