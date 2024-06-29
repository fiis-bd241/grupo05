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



