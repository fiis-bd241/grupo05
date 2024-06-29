# Aplicación de una base de datos NoSQL

## ScyllaDB
ScyllaDB es una base de datos NoSQL de alto rendimiento y escalabilidad diseñada para aplicaciones de Big Data. Se basa en Apache Cassandra y ofrece una serie de mejoras[1], incluyendo:

Mayor rendimiento: ScyllaDB logra un rendimiento significativamente mayor que Cassandra gracias a su arquitectura asíncrona y sin bloqueos, sus asignadores de memoria personalizados y la optimización meticulosa de las solicitudes de E/S.

Escalabilidad horizontal flexible: ScyllaDB se escala sin problemas mediante la adición de nodos a un clúster, lo que permite manejar conjuntos de datos cada vez más grandes sin sacrificar el rendimiento.

Compatibilidad con Apache Cassandra: ScyllaDB mantiene una compatibilidad a nivel de API con Apache Cassandra, lo que facilita la migración de datos y aplicaciones existentes.

Arquitectura optimizada para el rendimiento: ScyllaDB elimina los cuellos de botella de rendimiento comunes en Cassandra, como la caché de páginas, y prioriza la caché de filas para un acceso rápido y eficiente a los datos.

Costos reducidos: ScyllaDB ofrece una solución rentable al reducir el tiempo de administración y optimizar el uso de recursos, lo que se traduce en menores costos operativos.

### Beneficios de ScyllaDB
Alto rendimiento y baja latencia: ScyllaDB está diseñada para ofrecer un alto rendimiento y baja latencia, lo que la hace ideal para aplicaciones que requieren respuestas rápidas.

Escalabilidad horizontal: ScyllaDB se puede escalar horizontalmente para manejar grandes conjuntos de datos sin sacrificar el rendimiento.

Compatibilidad con Apache Cassandra: ScyllaDB es compatible con Apache Cassandra, lo que facilita la migración de datos y aplicaciones existentes.

Arquitectura optimizada para el rendimiento: ScyllaDB está diseñada para eliminar los cuellos de botella de rendimiento y proporcionar un acceso rápido y eficiente a los datos.

Costos reducidos: ScyllaDB es una solución rentable que puede ayudar a reducir los costos operativos.
## DESCRIPCION DEL USO DEL MOTOR SCYLLA EN NUESTRO TRABAJO
Para ello usaremos el modulo de Registro de Actividades, pues este módulo se adapta muy bien a  ScyllaDB pues presenta un montón de filtros de busqueda por columnas.
* TAREA 1: BUSQUEDA DE HISTORIAL DE UNA ASIGNACIÓN DE ACTIVIDAD
Esta tarea consiste en desarrollar funcionalidad para buscar el historial completo de una asignación de actividad en el sistema de Topitop. Esto puede incluir detalles como fechas de asignación, cambios de estado, gestores asignados, y operarios involucrados.

* TAREA 2: BUSQUEDA DE ASIGNACION DE ACTIVIDADES PARA UN GESTOR, OPERARIO, FECHA O ESTADO DE ASIGNACION
Funcionalidad para buscar asignaciones de actividades basadas en criterios específicos como gestor responsable, operario asignado, fecha de asignación o estado actual de la asignación en el sistema de Topitop.

### SECUENCIA DE PASOS 

### INICIO DE SESION
Ingresamos a la pagina de oficial de scylladb cuyo link es la siguiente : https://www.scylladb.com/onboard/ donde nos dejara utilizar la aplicacion por un periodo de tiempo , donde para ello se debio crear un usuario 

<img src="Captura de pantalla 2024-06-29 170231.png"  style="width: 100%; height: auto;" />

<img src="Captura de pantalla 2024-06-29 170323.png"  style="width: 100%; height: auto;" />


### CONFIGURACION 
Para configurar este motor de base de datos NOSQL y poder hacerlo correr dentro de esta pagina se debe hacer una seguidilla de pasos los cuales viene de manera intuitiva en la parte derecha de la pantalla donde nos facilita la opcion de hacer "run" los codigos  
### 1) 
<img src="Captura de pantalla 2024-06-29 174120.png"  style="width: 80%; height: auto;" />

### 2) 
<img src="imágenes/Captura de pantalla 2024-06-29 174442.png" style="width: 80%; height: auto;" />

### 3) 
<img src="imágenes/Captura de pantalla 2024-06-29 174457.png" style="width: 80%; height: auto;" />

### 4) 
<img src="imágenes/Captura de pantalla 2024-06-29 174506.png" style="width: 80%; height: auto;" />

### 5) 
<img src="imágenes/Captura de pantalla 2024-06-29 174515.png" style="width: 80%; height: auto;" />

### 6) 
<img src="imágenes/Captura de pantalla 2024-06-29 174523.png" style="width: 80%; height: auto;" />

### IMPLEMENTACIÓN
Con esto ya se pueden crear las tablas, hacer los inserts y hacer consultas, la hacemos:

* Dropeo y creacion de tabla:
``` SQL
DROP TABLE asignacion_actividad;

CREATE TABLE asignacion_actividad (
  id_asignacion TEXT ,
  fecha_asig DATE,
  hora_inicio TEXT,
  hora_fin TEXT,
  id_gestor TEXT,
  id_lote TEXT,
  actividad TEXT,
  id_operario TEXT,
  est_asignacion TEXT,
  PRIMARY KEY (id_asignacion,est_asignacion,fecha_asig,id_gestor,id_operario)
);
``` 

![image](https://github.com/fiis-bd241/grupo05/assets/164263409/f4f69436-6703-4abe-bed3-bfe8dd180a9d)

* Inserción de datos:
Para ello usamos esta insercción:
``` SQL
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI001', '2023-09-25', '9:30', '16:07', 'GES2', 'LOT61', 'Control de calidad de prendas', 'OPE11', 'En proceso');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI002', '2023-09-25', '10:46', '14:57', 'GES8', 'LOT3', 'Almacenamiento de productos terminados', 'OPE10', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI003', '2023-09-25', '11:58', '16:22', 'GES18', 'LOT45', 'Planchado y acabado de prendas', 'OPE19', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI004', '2023-10-26', '10:38', '16:26', 'GES8', 'LOT5', 'Diseño de prendas de vestir', 'OPE10', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI005', '2023-09-25', '11:09', '17:08', 'GES1', 'LOT76', 'Empaquetado y etiquetado de prendas', 'OPE1', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI006', '2024-02-06', '9:55', '13:53', 'GES1', 'LOT99', 'Control de calidad de prendas', 'OPE7', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI007', '2023-09-25', '9:53', '15:33', 'GES13', 'LOT68', 'Patronaje y corte de telas', 'OPE3', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI008', '2024-03-16', '10:32', '15:00', 'GES10', 'LOT14', 'Control de calidad de prendas', 'OPE5', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI009', '2024-03-16', '11:25', '14:21', 'GES1', 'LOT16', 'Confección de prendas', 'OPE7', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI010', '2023-06-20', '10:23', '13:18', 'GES19', 'LOT26', 'Control de calidad de prendas', 'OPE6', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI011', '2024-02-02', '11:30', '19:39', 'GES20', 'LOT6', 'Patronaje y corte de telas', 'OPE1', 'En proceso');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI012', '2024-03-21', '11:25', '16:52', 'GES19', 'LOT13', 'Costura y ensamblaje de componentes', 'OPE5', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI013', '2023-11-15', '11:13', '18:32', 'GES20', 'LOT93', 'Patronaje y corte de telas', 'OPE15', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI014', '2023-09-25', '11:50', '18:35', 'GES6', 'LOT14', 'Control de calidad de prendas', 'OPE18', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI015', '2024-05-04', '9:14', '19:04', 'GES9', 'LOT27', 'Confección de prendas', 'OPE17', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI016', '2023-08-13', '9:03', '14:59', 'GES2', 'LOT64', 'Diseño de prendas de vestir', 'OPE12', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI017', '2023-09-25', '9:00', '19:32', 'GES1', 'LOT46', 'Costura y ensamblaje de componentes', 'OPE16', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI018', '2023-07-16', '9:04', '15:44', 'GES9', 'LOT79', 'Planchado y acabado de prendas', 'OPE13', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI019', '2024-03-10', '10:23', '15:21', 'GES4', 'LOT48', 'Costura y ensamblaje de componentes', 'OPE12', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI020', '2024-05-24', '11:02', '17:26', 'GES16', 'LOT59', 'Empaquetado y etiquetado de prendas', 'OPE14', 'En proceso');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI021', '2023-10-18', '9:58', '17:26', 'GES13', 'LOT57', 'Costura y ensamblaje de componentes', 'OPE13', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI022', '2024-03-04', '9:31', '17:17', 'GES18', 'LOT97', 'Empaquetado y etiquetado de prendas', 'OPE15', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI023', '2024-04-26', '9:08', '16:29', 'GES15', 'LOT52', 'Control de calidad de prendas', 'OPE8', 'En proceso');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI024', '2024-01-01', '10:03', '14:48', 'GES18', 'LOT97', 'Planchado y acabado de prendas', 'OPE16', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI025', '2023-12-07', '10:29', '16:57', 'GES12', 'LOT88', 'Empaquetado y etiquetado de prendas', 'OPE4', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI026', '2023-11-10', '10:50', '17:41', 'GES5', 'LOT23', 'Empaquetado y etiquetado de prendas', 'OPE12', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI027', '2023-08-10', '11:37', '14:14', 'GES5', 'LOT40', 'Planchado y acabado de prendas', 'OPE11', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI028', '2023-11-19', '11:19', '15:12', 'GES8', 'LOT91', 'Planchado y acabado de prendas', 'OPE4', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI029', '2023-07-05', '9:47', '18:48', 'GES8', 'LOT54', 'Almacenamiento de productos terminados', 'OPE14', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI030', '2023-07-31', '11:37', '17:29', 'GES7', 'LOT73', 'Costura y ensamblaje de componentes', 'OPE20', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI031', '2023-08-05', '10:12', '18:02', 'GES17', 'LOT81', 'Planchado y acabado de prendas', 'OPE8', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI032', '2023-08-13', '11:43', '13:18', 'GES6', 'LOT1', 'Confección de prendas', 'OPE8', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI033', '2024-05-11', '10:55', '18:21', 'GES19', 'LOT73', 'Diseño de prendas de vestir', 'OPE3', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI034', '2023-09-06', '10:19', '18:16', 'GES6', 'LOT80', 'Empaquetado y etiquetado de prendas', 'OPE15', 'En proceso');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI035', '2023-12-12', '11:16', '13:05', 'GES19', 'LOT89', 'Patronaje y corte de telas', 'OPE5', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI036', '2024-02-12', '11:03', '17:29', 'GES3', 'LOT84', 'Costura y ensamblaje de componentes', 'OPE18', 'En proceso');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI037', '2023-07-11', '10:40', '16:24', 'GES15', 'LOT59', 'Planchado y acabado de prendas', 'OPE6', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI038', '2024-05-24', '9:27', '14:12', 'GES8', 'LOT49', 'Planchado y acabado de prendas', 'OPE4', 'En proceso');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI039', '2023-06-07', '11:51', '14:58', 'GES10', 'LOT40', 'Costura y ensamblaje de componentes', 'OPE3', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI040', '2024-04-13', '11:06', '19:13', 'GES17', 'LOT1', 'Control de calidad de prendas', 'OPE10', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI041', '2023-09-13', '11:58', '16:12', 'GES14', 'LOT96', 'Almacenamiento de productos terminados', 'OPE9', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI042', '2023-09-16', '9:13', '13:34', 'GES20', 'LOT6', 'Diseño de prendas de vestir', 'OPE13', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI043', '2024-02-15', '10:10', '16:23', 'GES13', 'LOT15', 'Costura y ensamblaje de componentes', 'OPE9', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI044', '2024-04-12', '10:24', '14:36', 'GES1', 'LOT72', 'Diseño de prendas de vestir', 'OPE3', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI045', '2024-05-15', '11:54', '17:34', 'GES8', 'LOT77', 'Diseño de prendas de vestir', 'OPE18', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI046', '2024-01-07', '9:37', '13:51', 'GES19', 'LOT9', 'Almacenamiento de productos terminados', 'OPE2', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI047', '2023-07-12', '9:43', '19:04', 'GES18', 'LOT8', 'Confección de prendas', 'OPE9', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI048', '2024-02-16', '11:13', '16:20', 'GES4', 'LOT94', 'Patronaje y corte de telas', 'OPE17', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI049', '2023-07-22', '11:39', '17:26', 'GES17', 'LOT85', 'Almacenamiento de productos terminados', 'OPE16', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI050', '2024-02-12', '10:15', '18:34', 'GES6', 'LOT4', 'Confección de prendas', 'OPE15', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI051', '2023-09-10', '11:02', '18:34', 'GES17', 'LOT89', 'Diseño de prendas de vestir', 'OPE9', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI052', '2023-09-02', '9:40', '13:03', 'GES5', 'LOT60', 'Diseño de prendas de vestir', 'OPE18', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI053', '2024-04-03', '11:06', '15:46', 'GES10', 'LOT65', 'Control de calidad de prendas', 'OPE3', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI054', '2023-08-09', '10:38', '16:03', 'GES8', 'LOT67', 'Patronaje y corte de telas', 'OPE15', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI055', '2023-09-01', '10:43', '17:25', 'GES7', 'LOT92', 'Confección de prendas', 'OPE16', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI056', '2023-12-09', '11:23', '16:40', 'GES19', 'LOT44', 'Confección de prendas', 'OPE20', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI057', '2024-01-07', '9:54', '18:17', 'GES5', 'LOT26', 'Control de calidad de prendas', 'OPE1', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI058', '2024-05-25', '9:54', '17:44', 'GES2', 'LOT72', 'Control de calidad de prendas', 'OPE6', 'En proceso');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI059', '2024-05-15', '11:09', '16:40', 'GES11', 'LOT28', 'Control de calidad de prendas', 'OPE1', 'En proceso');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI060', '2024-02-08', '11:35', '16:22', 'GES7', 'LOT34', 'Almacenamiento de productos terminados', 'OPE15', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI061', '2023-06-17', '10:18', '17:57', 'GES16', 'LOT40', 'Control de calidad de prendas', 'OPE16', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI062', '2023-11-24', '10:42', '15:27', 'GES2', 'LOT53', 'Planchado y acabado de prendas', 'OPE8', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI063', '2023-07-25', '11:27', '14:20', 'GES8', 'LOT21', 'Confección de prendas', 'OPE15', 'En proceso');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI064', '2023-11-12', '9:41', '16:28', 'GES7', 'LOT1', 'Planchado y acabado de prendas', 'OPE3', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI065', '2023-12-06', '11:07', '13:32', 'GES10', 'LOT4', 'Patronaje y corte de telas', 'OPE1', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI066', '2023-08-11', '11:40', '15:45', 'GES1', 'LOT50', 'Costura y ensamblaje de componentes', 'OPE11', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI067', '2023-10-09', '10:25', '13:45', 'GES3', 'LOT22', 'Planchado y acabado de prendas', 'OPE14', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI068', '2024-05-23', '11:06', '19:06', 'GES4', 'LOT67', 'Confección de prendas', 'OPE3', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI069', '2023-08-18', '9:37', '19:05', 'GES2', 'LOT72', 'Confección de prendas', 'OPE6', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI070', '2023-12-08', '10:25', '16:00', 'GES6', 'LOT76', 'Empaquetado y etiquetado de prendas', 'OPE12', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI071', '2023-06-20', '10:35', '13:21', 'GES10', 'LOT62', 'Confección de prendas', 'OPE13', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI072', '2024-02-12', '9:44', '16:30', 'GES16', 'LOT41', 'Planchado y acabado de prendas', 'OPE3', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI073', '2023-12-06', '10:08', '19:10', 'GES5', 'LOT13', 'Planchado y acabado de prendas', 'OPE9', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI074', '2023-08-07', '9:36', '16:46', 'GES5', 'LOT72', 'Planchado y acabado de prendas', 'OPE5', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI075', '2024-04-23', '9:13', '13:10', 'GES9', 'LOT99', 'Empaquetado y etiquetado de prendas', 'OPE3', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI076', '2023-11-08', '10:24', '14:55', 'GES8', 'LOT2', 'Planchado y acabado de prendas', 'OPE20', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI077', '2023-11-02', '9:06', '17:13', 'GES15', 'LOT97', 'Patronaje y corte de telas', 'OPE4', 'En proceso');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI078', '2023-10-29', '10:57', '14:00', 'GES19', 'LOT65', 'Diseño de prendas de vestir', 'OPE16', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI079', '2023-11-23', '9:09', '13:33', 'GES8', 'LOT31', 'Control de calidad de prendas', 'OPE13', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI080', '2024-04-23', '10:10', '18:35', 'GES17', 'LOT56', 'Control de calidad de prendas', 'OPE5', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI081', '2023-07-27', '11:07', '16:57', 'GES3', 'LOT54', 'Diseño de prendas de vestir', 'OPE11', 'En proceso');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI082', '2024-01-31', '10:33', '13:27', 'GES18', 'LOT70', 'Empaquetado y etiquetado de prendas', 'OPE15', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI083', '2024-03-12', '11:12', '19:42', 'GES4', 'LOT76', 'Control de calidad de prendas', 'OPE7', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI084', '2024-05-06', '9:10', '13:32', 'GES8', 'LOT15', 'Confección de prendas', 'OPE10', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI085', '2024-01-18', '9:12', '16:34', 'GES9', 'LOT13', 'Patronaje y corte de telas', 'OPE11', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI086', '2023-09-22', '10:27', '19:50', 'GES16', 'LOT36', 'Empaquetado y etiquetado de prendas', 'OPE20', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI087', '2023-11-09', '9:55', '15:55', 'GES3', 'LOT30', 'Diseño de prendas de vestir', 'OPE3', 'En proceso');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI088', '2023-10-08', '9:46', '15:22', 'GES19', 'LOT28', 'Almacenamiento de productos terminados', 'OPE4', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI089', '2023-11-10', '9:18', '16:25', 'GES6', 'LOT43', 'Almacenamiento de productos terminados', 'OPE6', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI090', '2024-03-18', '10:26', '18:02', 'GES16', 'LOT93', 'Confección de prendas', 'OPE18', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI091', '2023-10-21', '9:18', '15:25', 'GES10', 'LOT28', 'Empaquetado y etiquetado de prendas', 'OPE5', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI092', '2023-10-02', '11:39', '13:13', 'GES9', 'LOT50', 'Confección de prendas', 'OPE8', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI093', '2024-05-12', '9:16', '14:13', 'GES20', 'LOT48', 'Confección de prendas', 'OPE6', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI094', '2024-05-12', '10:51', '18:20', 'GES8', 'LOT21', 'Costura y ensamblaje de componentes', 'OPE8', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI095', '2023-09-22', '9:42', '18:47', 'GES10', 'LOT47', 'Confección de prendas', 'OPE5', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI096', '2024-03-13', '11:40', '17:17', 'GES2', 'LOT78', 'Patronaje y corte de telas', 'OPE19', 'En revisión');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI097', '2023-08-08', '9:03', '16:06', 'GES2', 'LOT65', 'Control de calidad de prendas', 'OPE17', 'Culminado');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI098', '2023-09-11', '10:52', '15:03', 'GES6', 'LOT70', 'Diseño de prendas de vestir', 'OPE10', 'Con defectos');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI099', '2024-05-21', '10:56', '14:50', 'GES15', 'LOT18', 'Empaquetado y etiquetado de prendas', 'OPE8', 'En proceso');
insert into asignacion_actividad (id_asignacion, fecha_asig, hora_inicio, hora_fin, id_gestor, id_lote, actividad, id_operario, est_asignacion) values ('ASI100', '2023-09-29', '11:10', '18:59', 'GES9', 'LOT57', 'Patronaje y corte de telas', 'OPE18', 'En proceso');
```

* Consultas a la base de datos:
Para ello hacemos:
 1) Para una asignación en concreto (ASI001):
    ![image](https://github.com/fiis-bd241/grupo05/assets/164263409/6793178b-157c-484a-808e-4c271e505795)
 2) Para asignaciones ya acabadas:
    ![image](https://github.com/fiis-bd241/grupo05/assets/164263409/46bdd2b3-7a6e-4e15-966d-7655a5ac6d0a)

 3) Para asginaciones ya acabadas y hechas en el 2023-09-25:
    ![image](https://github.com/fiis-bd241/grupo05/assets/164263409/af6dbea3-e9c5-4642-884e-841e2862aa20)

 4) Para asginaciones ya acabadas ,hechas en el 2023-09-25 y con gestor GES1:
    ![image](https://github.com/fiis-bd241/grupo05/assets/164263409/8fc18d17-44ac-4e83-b276-692728e3e930)

 5) Para asginaciones ya acabadas ,hechas en el 2023-09-25, con gestor GES1 y operario OPE16:
    ![image](https://github.com/fiis-bd241/grupo05/assets/164263409/6a270e50-6ed6-4a78-bcc1-0bf47e2c408c)

### VIDEO EXPLICATIVO:

[![Video](https://img.youtube.com/vi/TfTlVybQPhI/0.jpg)](https://www.youtube.com/watch?v=TfTlVybQPhI)






















