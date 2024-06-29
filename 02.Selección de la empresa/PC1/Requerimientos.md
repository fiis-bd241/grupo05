## REQUERIMIENTOS

## USUARIOS DEL SISTEMA

- **Gerente de producción**: Este tipo de usuario es un usuario paramétrico, va a poder registrar la información necesaria según los que requieran ciertos módulos, analiza los reportes para asignar la gestión adecuada según los criterios validados que este mismo posea y solicitará el mantenimiento de maquinaria o herramientas.

- **Operario**: Este tipo de usuario también es paramétrico, se caracteriza porque el propio sistema es enfocado a su continuo uso, los requerimientos planteados son en su mayoría con base a lo requerido por este tipo de usuario durante el desempeño de sus labores, sobre todo le va a ayudar a automatizar los procesos de categorización de calidad, notificar el uso de herramientas o maquinarias para llevar un histórico o presentar reclamos u observaciones.

### 1. Requerimientos funcionales

* MÓDULO DE CALIDAD DE HERRAMIENTAS Y MAQUINARIA

#### **Caso de uso N°1: Mantenimiento Preventivo de herramientas y maquinaria**

| **Objetivo:** |Programar y hacer seguimiento de los mantenimientos periódicos para las herramientas y maquinarias. |
|------|--------|
| **Descripción:** | El responsable de mantenimiento accederá al sistema y seleccionará la opción de "Mantenimiento Preventivo". Se mostrará una lista de herramientas y maquinarias que requieren mantenimiento. El responsable seleccionará una herramienta o maquinaria y programará la fecha del próximo mantenimiento. | 
| **Actor Primario:** | Responsable de mantenimiento |
| **Actor Secundario:** | Gerente de producción | 
| **Precondiciones:** | Existencia de herramientas y maquinarias registradas en el sistema que requieran mantenimiento| 
| Paso | Acción |
| 1    |El responsable de mantenimiento ingresa al sistema.|
| 2    |Accede al apartado "Mantenimiento Preventivo".|
| 3    | Se monitorean y controlan los procesos de fabricación para asegurar que se cumplan los estándares de calidad establecidos. Esto puede incluir la implementación de controles en línea durante la producción para detectar y corregir posibles problemas de calidad de manera oportuna.|
| 4    | Selecciona una herramienta o maquinaria |
| 5    | Programa la fecha del próximo mantenimiento.|
| 6    | Confirma y guarda la programación del mantenimiento.|
| 7    | Caso terminado.|


#### **Caso de uso N°2: Reporte de Calidad de herramientas y maquinaria**

| **Objetivo:** |Identificar áreas de mejora en los procesos de producción a través del análisis de datos recopilados.|
|------|--------|
| **Descripción:** |	El sistema deberá analizar los datos de calidad recopilados durante las inspecciones y el control de calidad en procesos para identificar posibles áreas de mejora.| 
| **Actor:** | Gerente de producción | 
| **Precondiciones:** || 
| 1   |Definición de Estándares de Calidad: Opción para establecer y modificar estándares de calidad.|
|    |Campos para especificar criterios como dimensiones, materiales y procesos.
|2|Inspecciones de Producto|
|    |Registro de inspecciones periódicas a productos.|
|3|Campos para resultados, observaciones y fechas de inspección.|
| 4   |Control de Calidad en Procesos|
| |Registro de calidad de materias primas, eficiencia de procesos y satisfacción del cliente.|
| 5   |Opciones para evaluar y calificar los procesos de producción.|
| |Análisis y Mejora Continua|
| 6   |Análisis de datos para identificar áreas de mejora.|
| |Implementación de acciones correctivas y preventivas.|



#### **Caso de uso N°3: Reporte de Calidad de herramientas y maquinaria**

| **Objetivo:** |Identificar áreas de mejora en los procesos de producción a través del análisis de datos recopilados.|
|------|--------|
| **Descripción:** |	El sistema deberá analizar los datos de calidad recopilados durante las inspecciones y el control de calidad en procesos para identificar posibles áreas de mejora.| 
| **Actor:** | Gerente de producción | 
| **Precondiciones:** || 
| 1   |Definición de Estándares de Calidad: Opción para establecer y modificar estándares de calidad.|
|    |Campos para especificar criterios como dimensiones, materiales y procesos.
|2|Inspecciones de Producto|
|    |Registro de inspecciones periódicas a productos.
|3|Campos para resultados, observaciones y fechas de inspección.|
| 4   |Control de Calidad en Procesos|
| |Registro de calidad de materias primas, eficiencia de procesos y satisfacción del cliente.|
| 5   |Opciones para evaluar y calificar los procesos de producción.|
| |Análisis y Mejora Continua|
| 6   |Análisis de datos para identificar áreas de mejora.|
| |Implementación de acciones correctivas y preventivas.|

* MÓDULO DE CALIDAD DE PROCESOS

#### **Caso de uso N°4: reportes de calidad**

| **Objetivo:** | Generar informes detallados sobre la calidad de los procesos y productos textiles. |
|------|--------|
| **Descripción:** | El sistema permitirá a los usuarios generar informes de calidad que incluyan estadísticas, tendencias y análisis comparativos para evaluar la calidad de los productos y procesos textiles.| 
| **Actor:** | Gerente de producción | 
| **Precondiciones:** | Existencia de datos de calidad recopilados en el sistema. | 
| Paso | Acción |
| 1    | El usuario autorizado ingresa al sistema. |
| 2    | El usuario accede al apartado "Reportes de Calidad". |
| 3    | El sistema presenta opciones para seleccionar el tipo de informe deseado: calidad de insumos, calidad de operarios o calidad de confecciones.|
| 4    |El usuario selecciona el tipo de informe que desea generar.|
| 5    |El sistema genera el informe de calidad según las especificaciones del usuario.|
| 6    | Finaliza el caso.  |

*MÓDULO DE GESTION DE HERRAMIENTAS Y MAQUINARIAS

#### **Caso de uso N°5: Selección de herramientas y maquinarias**

| **Objetivo:** | Permitir al operario solicitar herramientas y maquinarias necesarias para llevar a cabo una actividad específica. |
|------|--------|
| **Descripción:** |  El operario ingresará al sistema y accederá al apartado de "Solicitar de herramienta". Luego de ello, podrá buscar la herramienta deseada por su nombre o código y especificar la actividad que va a realizar. Posteriormente, se dara su busqueda.
| **Actor Primario:** | Operario | 
| **Actor Secundario :** | Gestor de producción. | 
| **Precondiciones:** | Las herramientas y maquinarias deben estar registradas en la base de datos del sistema. | 
| Paso | Acción |
| 1    | El operario ingresa al sistema.. |
| 2    | El operario accede al apartado "Solicitar herramienta". |
| 3    | El operario busca la herramienta deseada por su nombre o código. |
| 4    | El operario especifica la actividad que va a realizar. |
| 5    | El operario inicia la búsqueda haciendo clic en el icono de la lupa. |
| 6    | El sistema muestra una tabla con las herramientas disponibles, incluyendo el nombre, código, modelo y estado (disponible, ocupado o mantenimiento). |
| 7    | El operario selecciona la herramienta deseada. |
| 8    | El operario hace clic en "Enviar solicitud". |
| 9    | El sistema envía la solicitud al gestor de producción para su validación. |
| 10    | Caso terminado. |


#### **Caso de uso N°6: Visualización de Histórico de Mantenimientos **

| **Objetivo:** | Visualizar el histórico de todos los mantenimientos realizados a las herramientas y maquinarias. |
|------|--------|
| **Descripción:** |  El responsable de mantenimiento o cualquier usuario autorizado accede al sistema y selecciona la opción de "Histórico de Mantenimientos". Se muestra un listado de todas las herramientas y maquinarias registradas, junto con los mantenimientos previamente realizados a esas maquinas
| **Actor Primario:** |  Responsable de mantenimiento | 
| **Actor Secundario :** | Personal autorizado | 
| **Precondiciones:** |Existencia de registros de mantenimientos previos en el sistema.
Estándares de calidad definidos y asociados a cada herramienta y maquinaria.. | 
| Paso | Acción |
| 1    | El responsable de mantenimiento o usuario autorizado ingresa al sistema. |
| 2    | Accede al apartado "Histórico de Mantenimientos". |
| 3    | Se muestra un listado de todas las herramientas y maquinarias registradas. |
| 4    | Selecciona una herramienta o maquinaria para ver su histórico de mantenimientos y|
|      | estándares de calidad.|
| 5    |Visualiza los detalles de los mantenimientos realizados, incluyendo fechas, tipo de |
|      |mantenimiento, cumplimiento de estándares y comentarios adicionales. |
| 6    |Puede realizar búsquedas o filtrados adicionales según sea necesario.|
| 7    | Caso terminado. |

* MÓDULO DE RECLAMOS Y OBSERVACIONES

#### **Caso de uso N°7: Reclamo del operario**
| **Objetivo:** |Permitir a los operarios registrar reclamos sobre condiciones laborales, problemas de seguridad, sugerencias de mejora u otras preocupaciones relacionadas con su experiencia laboral.|
|------|--------|
| **Descripción:** |Los operarios puedan presentar reclamos a través del sistema digital, facilitando la comunicación y la gestión eficiente de problemas en el lugar de trabajo.|
| **Actor Primario:** |operario| 
| **Actor Secundario :** |gerente de producción| 
| **Precondiciones:** |El operario debe estar registrado en el sistema y una preocupación o problema laboral que desee registrar como reclamo|
| Paso | Acción |
| 1    |Dirigirse a la sección de quejas y reclamos del sistema|
| 2    |Seleccionar la opción para registrar un nuevo reclamo y completar los campos requeridos|
| 3    |Envío del reclamo al sistema para su registro|
| 4    |Durante el proceso de resolución, el sistema permite la comunicación entre el operario y el responsable de la gestión del reclamo, facilitando cualquier intercambio de información o feedback|
| 5    |Una vez que se resuelve el reclamo, el sistema notifica al operario sobre las acciones tomadas y cierra el reclamo|

* MÓDULO DE RECLAMOS Y OBSERVACIONES

#### **Caso de uso N°8: Reclamo del operario**
| **Objetivo:** |Permitir a los operarios registrar reclamos sobre condiciones laborales, problemas de seguridad, sugerencias de mejora u otras preocupaciones relacionadas con su experiencia laboral.|
|------|--------|
| **Descripción:** |Los operarios puedan presentar reclamos a través del sistema digital, facilitando la comunicación y la gestión eficiente de problemas en el lugar de trabajo.|
| **Actor Primario:** |operario| 
| **Actor Secundario :** |gerente de producción| 
| **Precondiciones:** |El operario debe estar registrado en el sistema y una preocupación o problema laboral que desee registrar como reclamo|
| Paso | Acción |
| 1    |Dirigirse a la sección de quejas y reclamos del sistema|
| 2    |Seleccionar la opción para registrar un nuevo reclamo y completar los campos requeridos|
| 3    |Envío del reclamo al sistema para su registro|
| 4    |Durante el proceso de resolución, el sistema permite la comunicación entre el operario y el responsable de la gestión del reclamo, facilitando cualquier intercambio de información o feedback|
| 5    |Una vez que se resuelve el reclamo, el sistema notifica al operario sobre las acciones tomadas y cierra el reclamo|

* MÓDULO DE REPORTES

### **Caso de uso N°9: Reportes por operarios**
| **Objetivo:** |Permitir al jefe de producción analizar las actividades concluidas por un operario|
|------|--------|
| **Descripción:** | el jefe de producción se encarga de rellenar la información de las actividades de cada empleado
| **Actor Primario:** |jefe de producción| 
| **Actor Secundario :** |no hay actor secundario| 
| **Precondiciones:** |no hay precondiciones vigentes|
| Paso | Acción |
| 1    |Seleccionar el reporte de los operarios|
| 2    |Ingresar el código del empleado e la cuadrícula|
| 3    |Visualizar el reporte| 

#### **Caso de uso N°10: Reportes por supervisor**
| **Objetivo:** |Permitir al jefe de producción analizar las actividades concluidas por los operarios de un cierto supervisor|
|------|--------|
| **Descripción:** |A partir de la información obtenida en el registro de tareas se concluye aquí la revisión de todos los operarios por supervisor|
| **Actor Primario:** |jefe de producción| 
| **Actor Secundario :** |no hay actor secundario| 
| **Precondiciones:** |no hay precondiciones vigentes|
| Paso | Acción |
| 1    |Seleccionar el reporte por supervisor|
| 2    |Ingresar el código del supervisor en la cuadrícula|
| 3    |Visualizar el reporte| 

#### **Caso de uso N°11: Reportes por Herramienta**
| **Objetivo:** |Permitir al jefe de producción analizar los estados de las herramientas durante el trabajo|
|------|--------|
| **Descripción:** |A partir de la información obtenida en el registro de herramientas y maquinarias se concluye aquí la revisión de todas las herramientas|
| **Actor Primario:** |jefe de producción| 
| **Actor Secundario :** |no hay actor secundario| 
| **Precondiciones:** |Datos ya creados desde el registro de herramientas y maquinarias|
| Paso | Acción |
| 1    |Seleccionar el reporte de herramientas|
| 2    |Ingresar el código de la heramienta en la cuadrícula|
| 3    |Visualizar el reporte| 


#### **Caso de uso N°12: Reportes por Maquinarias**
| **Objetivo:** |Permitir al jefe de producción analizar los estados de las maquinarias durante el trabajo|
|------|--------|
| **Descripción:** |A partir de la información obtenida en el registro de herramientas y maquinarias se concluye aquí la revisión de todas las maquinarias|
| **Actor Primario:** |jefe de producción| 
| **Actor Secundario :** |no hay actor secundario| 
| **Precondiciones:** |Datos ya creados desde el registro de herramientas y maquinarias|
| Paso | Acción |
| 1    |Seleccionar el reporte de maquinarias|
| 2    |Ingresar el código de la maquinaria en la cuadrícula|
| 3    |Visualizar el reporte| 


#### **Caso de uso N°13: Reportes por operario**
| **Objetivo:** |Permitir al operario analizar sus propias actividades para conocer su paga semanal|
|------|--------|
| **Descripción:** |A partir de la información obtenida en el registro de tareas se concluye aquí la revisión de todas las actividades realizadas por el operario|
| **Actor Primario:** |operario| 
| **Actor Secundario :** |no hay actor secundario| 
| **Precondiciones:** |Datos ya creados desde el registro de tareas|
| Paso | Acción |
| 1    |Seleccionar el reporte por operario|
| 2    |Visualizar el reporte|

* MÓDULO DE SOLICITUD DE PEDIDOS DE INSUMOS

#### **Caso de uso N°14: Abastecimiento de insumos**

| **Objetivo:** | Coordinar y gestionar el flujo de materiales desde el almacén hasta las líneas de producción, asegurando que se satisfagan las necesidades de producción de manera oportuna y eficiente. |
|------|--------|
| **Descripción:** | Este caso de uso describe el proceso de abastecimiento de materia prima desde la planificación de la producción y gestión del inventario hasta la distribución de la materia prima al área de producción. | 
| **Actor:** | Encargado de Adquisiciones | 
| **Precondiciones:** | El sistema de gestión de inventario se encuentra actualizado, asimismo se posee suficiente espacio para almacenar la materia prima. | 
| Paso | Acción |
| 1    | Se determinan los niveles de inventario tanto en el almacén como en el área de producción para determinar los materiales necesarios, así como el tiempo necesario para que dicha producción no se detenga. |
| 2    | Se gestionan las compras para adquirir los materiales necesarios para la producción. |
| 3    | Se lleva a cabo una selección y evaluación de proveedores para garantizar la calidad del producto y el tiempo de entrega, entre otros criterios. |
| 4    | Se recibe la materia prima de los proveedores y se verifica su calidad. |
| 5    | Una vez adquiridos los materiales, se gestiona la correcta recepción y almacenamiento de estos, la cual será guiado por un registro detallado. |
| 6    | Se distribuyen los materiales necesarios para el área de producción, que en este caso consiste en la confección de ropa. |
| 7    | Finaliza el caso. |

* MÓDULO DE REGISTRO DE ACTIVIDADES

#### **Caso de uso N°15: Asignación de Actividades**

| **Objetivo:** | Permitir a un gestor de producción asignar actividades a los operarios dentro del sistema web. |
|------|--------|
| **Descripción:** | Este caso de uso describe el proceso mediante el cual un gestor de producción puede asignar una actividad específica a un operario en el sistema web. Las actividades pueden incluir tareas de producción de la empresa. | 
| **Actores:** | Gestor de Producción | 
| **Precondiciones:** | El gestor de producción debe tener los permisos adecuados para asignar actividades, además debe existir al menos un operario al que se pueda asignar la actividad. | 
| Paso | Acción |
| 1    | El gestor de producción inicia sesión en el sistema web. |
| 2    | El gestor de producción accede a la sección de gestión de actividades. |
| 3    | El gestor de producción selecciona la opción de "Asignar nueva actividad". |
| 4    | El sistema muestra un formulario para la asignación de la actividad. |
| 5    | El gestor de producción completa el formulario, incluyendo detalles como la  actividad a realizar, la fecha límite y el operario asignado. |
| 6    | El sistema registra la actividad asignada y notifica al operario. |
| 7    | Finaliza el caso. |

#### **Caso de uso N°16: Envío de Verificación de Actividad**

| **Objetivo:** | Permitir a un operario enviar una verificación de una actividad al gestor de producción para su revisión. |
|------|--------|
| **Descripción:** |  Este caso de uso describe el proceso mediante el cual un operario puede enviar una verificación de una actividad completada al gestor de producción para su revisión. La verificación proporciona al gestor de producción la confirmación de que la actividad ha sido realizada de acuerdo con los requisitos establecidos. | 
| **Actores:** | Operario | 
| **Precondiciones:** | La actividad debe haber sido completada por el operario, el operario debe tener los permisos necesarios para enviar verificaciones | 
| Paso | Acción |
| 1    | El operario inicia sesión en el sistema web. |
| 2    | El operario accede a la lista de actividades que está haciendo. |
| 3    | El operario selecciona la actividad que desea verificar y envía una solicitud de verificación al gestor de producción. |
| 4    | El sistema notifica al gestor de producción sobre la solicitud de verificación. |
| 5    | El gestor de producción recibe la notificación y accede a la lista de verificaciones pendientes. |
| 6  | Finaliza el caso. |


#### **Caso de uso N°17: Auditar Actividades**

| **Objetivo:** | Permitir a un gestor de producción dar un visto bueno a una actividad para indicar que ha sido realizada correctamente por un operario. |
|------|--------|
| **Descripción:** |  Este caso de uso describe cómo un gestor de producción puede auditar una actividad realizada por un operario para verificar que ha sido completada satisfactoriamente. El gestor de producción tiene la capacidad de dar un visto bueno a la actividad, lo que indica que ha sido realizada según los estándares establecidos. | 
| **Actores:** | Gestor de Producción | 
| **Precondiciones:** | La actividad debe estar marcada como completada por el operario, además el gestor de producción debe tener los permisos adecuados para auditar actividades. | 
| Paso | Acción |
| 1    | El gestor de producción inicia sesión en el sistema web. |
| 2    | El gestor de producción accede a la lista de actividades pendientes de auditoría. |
| 3    | El sistema muestra las actividades que están listas para ser auditadas. |
| 4    | El gestor de producción selecciona una actividad para auditar. |
| 5    | El gestor de producción revisa los detalles de la actividad y verifica que ha sido completada correctamente por el operario. |
| 6    | Si la actividad cumple con los criterios establecidos, el gestor de producción da un visto bueno. |
| 7    | El sistema registra el visto bueno y actualiza el estado de la actividad como auditada. |
| 8    | Si la actividad no cumple con los criterios, el gestor de producción puede solicitar rehacer la actividad al operario. |
| 9    | El sistema notifica al operario sobre el resultado de la auditoría. |
| 10   | Finaliza el caso. |

#### **Caso de uso N°18: Historial de Actividades**

| **Objetivo:** | Permitir a los usuarios revisar el historial de actividades realizadas en el sistema. |
|------|--------|
| **Descripción:** | Este caso de uso describe cómo los usuarios pueden acceder al historial completo de actividades realizadas por los operarios en el sistema web. El historial proporciona una visión retrospectiva de todas las actividades completadas, asignadas o modificadas dentro del sistema. | 
| **Actores:** | Operario y Gestor de Producción | 
| **Precondiciones:** | Deben existir actividades registradas en el sistema y en caso de que el usuario sea un operario, solo puede ver las actividades hechas por el mismo. | 
| Paso | Acción |
| 1    | El usuario inicia sesión en el sistema web. |
| 2    | El usuario accede a la sección de historial de actividades. |
| 3    | El sistema muestra una lista ordenada cronológicamente de todas las actividades realizadas. |
| 4    | El usuario puede aplicar filtros de búsqueda para encontrar actividades específicas. |
| 5    | El usuario revisa el historial de actividades, que incluye detalles como la descripción de la actividad, fecha de creación, fecha de asignación, fecha de finalización, y el estado de la actividad. |
| 6    | Finaliza el caso. |

### 2. Requerimientos de atributos de calidad
* Seguridad: El sistema debe garantizar la confidencialidad e integridad de los datos almacenados y transmitidos. Para ello, el sistema solo permitirá acceso a los usuarios que están registrados y que cumplan un rol en la empresa, y solicitará que los usuarios proporcionen dos formas de autenticación: una contraseña y un código enviado a su dispositivo móvil.
* Escalabilidad: El sistema debe ser capaz de manejar grandes volúmenes de datos y usuarios en tiempo real.
* Fiabilidad: El sistema debe ser resistente a fallos menores y ser capaz de recuperarse automáticamente sin afectar significativamente la operación. En caso de fallos graves, el tiempo de recuperación no debe superar las 3 horas. Además, se realizará copias de seguridad diarias de los datos del sistema y mantener copias de seguridad históricas durante al menos 90 días.
* Usabilidad: El sistema debe ser fácil de usar y comprender, con una interfaz amigable para los usuarios.
* Compatibilidad: El sistema debe funcionar en múltiples dispositivos, así como en diferentes sistemas operativos y navegadores web.

### 3. Restricciones
* El Backend del sistema se implementará en PostgreSQL
       
[Selección de la empresa](../SeleccionEmpresa.md)

[Regresar al índice](../README.md)
