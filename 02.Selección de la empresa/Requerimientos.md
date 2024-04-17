## REQUERIMIENTOS

## USUARIOS DEL SISTEMA

- **Gerente de producción**: Este tipo de usuario es un usuario paramétrico, va a poder registrar la información necesaria según los que requieran ciertos módulos, analiza los reportes para asignar la gestión adecuada según los criterios validados que este mismo posea y solicitará el mantenimiento de maquinaria o herramientas.

- **Operario**: Este tipo de usuario también es paramétrico, se caracteriza porque el propio sistema es enfocado a su continuo uso, los requerimientos planteados son en su mayoría con base a lo requerido por este tipo de usuario durante el desempeño de sus labores, sobre todo le va a ayudar a automatizar los procesos de categorización de calidad, notificar el uso de herramientas o maquinarias para llevar un histórico o presentar reclamos u observaciones.

### 1. Requerimientos funcionales

#### **Caso de uso N°1: Abastecimiento de insumos**

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

#### **Caso de uso N°2: Selección de herramientas y maquinarias**

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

#### **Caso de uso N°3: Validación de la solicitud de herramientas y maquinarias**

| **Objetivo:** | Permitir al gestor de producción validar las solicitudes de herramientas y maquinarias realizadas por los operarios. |
|------|--------|
| **Descripción:** |  El gestor de producción ingresará al sistema y accederá al apartado de "Solicitud de herramienta". Se mostrará una tabla con todas las solicitudes pendientes, donde se visualizará el código del usuario que solicita, el código de la herramienta, el modelo y nombre de la herramienta. El gestor tendrá la opción de aceptar o rechazar la solicitud.
| **Actor Primario:** |  Gestor de producción | 
| **Actor Secundario :** | Operario | 
| **Precondiciones:** | Existencia de solicitudes de herramientas y maquinarias pendientes en el sistema. | 
| Paso | Acción |
| 1    | El gestor de producción ingresa al sistema. |
| 2    | El gestor de producción accede al apartado "Solicitud de herramienta". |
| 3    | El sistema muestra una tabla con todas las solicitudes pendientes. |
| 4    | En la tabla se visualiza el código del usuario que solicita, el código de la herramienta, el modelo y nombre de la herramienta. |
| 5    | El gestor de producción revisa cada solicitud pendiente. |
| 6    | El gestor de producción tiene la opción de aceptar o rechazar cada solicitud. |
| 7    | Si se decide aceptar la solicitud: |
||a. El gestor de producción marca la solicitud como aceptada. |
||b. El sistema actualiza el estado de la herramienta a "ocupado". |
||c. Se notifica al operario que su solicitud ha sido aprobada. |
| 8    | Si se decide rechazar la solicitud: |
|  |a. El gestor de producción marca la solicitud como rechazada. |
|     |b. Se notifica al operario que su solicitud ha sido rechazada. |
| 9  | El gestor de producción puede repetir el proceso para todas las solicitudes pendientes.|
| 10  | Caso terminado.|



#### **Caso de uso N°4: Registro de las actividades**

| **Objetivo:** | Gestionar de manera eficaz la mano de obra y optimizar los procesos de fabricación. |
|------|--------|
| **Descripción:** | Este caso de uso describe el proceso de registro de la información relacionada con el trabajo de los empleados en las líneas de producción de prendas. | 
| **Actores:** | Operario y Gestor de Producción | 
| **Precondiciones:** | Se disponen de instrumentos de medición que permiten registrar intervalos de tiempo así como los datos de los operarios y de las actividades a registrar. | 
| Paso | Acción |
| 1    | Se registra la hora de inicio y acabado de las actividades de los empleados en sus jornadas laborales. Esto proporciona un seguimiento preciso del tiempo de trabajo por cada empleado. |
| 2    | Los gestores de producción de este módulo pueden verificar el estado de las acividades en curso y realizar ajustes según sea necesario para garantizar que se cumplan los plazos y objetivos de producción. |
| 3    | Se asignan tareas especificas a los empleados en función de sus habilidades y la disponibiidad que tienen, con esto se asegura una distribución equitativa del trabajo y una correcta asignación eficiente de recursos humanos en cada turno de producción. |
| 4    | Se registra el tiempo extra trabajado por los empleados , así como las ausencias de éstos en el trabajo, vacaciones o días libres. También se registran las ausencias no planificadas como enfermedades, con esto se puede garantizar una correcta cobertura adecuada en la línea de producción. |
| 5    | Se generan informes detallados sobre la asistencia y el rendimiento laboral de los empleados, como también las horas trabajadas en cada día. Esto permite generar información valiosa para evaluar la eficiencia operativa, identificar áreas de mejora y tomar mejores decisiones. |
| 6    | Finaliza el caso. |

#### **Caso de uso N°5: Control de calidad**

| **Objetivo:** | Garantizar la excelencia de los productos fabricados. |
|------|--------|
| **Descripción:** | Este caso de uso describe el proceso de control de calidad mediante el cumplimiento de estándares de calidad. | 
| **Actor:** | Gerente de producción | 
| **Precondiciones:** | Se conocen previamente los estándares de calidad. | 
| Paso | Acción |
| 1    | Se realizan inspecciones de calidad en los productos terminados, así como en los materiales y componentes utilizados en el proceso de fabricación y se registran los resultados obtenidos. Esto incluye la evaluación de aspectos como la apariencia, la resistencia, la durabilidad y otros criterios de calidad definidos por la empresa. |
| 2    | Se monitorean y controlan los procesos de fabricación para asegurar que se cumplan los estándares de calidad establecidos. Esto puede incluir la implementación de controles en línea durante la producción para detectar y corregir posibles problemas de calidad de manera oportuna.|
| 3    | Se registran y gestionan las no conformidades identificadas durante las inspecciones de calidad. Esto incluye el registro de las causas de las no conformidades, así como las acciones correctivas y preventivas implementadas para abordarlas y evitar su recurrencia. |
| 4    | Se analizan los datos recopilados durante las inspecciones de calidad para identificar tendencias, patrones y áreas de mejora en los procesos de fabricación. Esto permite tomar decisiones informadas para optimizar la calidad y la eficiencia operativa. |
| 5    | Finaliza el caso. |

#### **Caso de uso N°8: registro de usuario**:
| **Objetivo:** |Permitir al gestor de la producción u operario ingresar con su usario y contraseña al sistema |
|------|--------|
| **Descripción:** |  El usario ingresará al sistema y se topará con "el inicio de sesión" junto con dos espacios para completar , el usuario deberá ingresar sus datos y podrá acceder al sistema. 
| **Actor Primario:** |Usuario (operario o gestor de producción)| 
| **Actor Secundario :** |no hay actor secundario | 
| **Precondiciones:** | los datos a ingresar deben ser unos que esten registrados enla base de datos, de lo contrario  no se podrá acceder al sistema 
| Paso | Acción |
| 1    | El operario o gestor de la producción ingresa al inicio de sesión sistema.. |
| 2    | El operario o gestor de la producción digita su usuario|
| 3    | El operario o gestor de la producción digita su contraseña|
| 4    | Se revisa si existe dicho usuario y contraseña en la base de datos|
| 5    |si los datos concuerdan con la algún valor de la base de datos se da acceso al sistema de lo contrario se envía un mensaje de "usuario o contraseña invalidos"|
| 6    |  Caso terminado.|
#### **Caso de uso N°9: Edición del perfil**:
| **Objetivo:** |Permitir al operario o gestor de producción cambiar algunos datos que se tengan registrado en el sistema|
|------|--------|
| **Descripción:** | el usuario tendrá la opción de editar algunos datos como , el telefono celulqar , el correo, la foto de perfil y incluso la contraseña. 
| **Actor Primario:** |Usuario (operario o gestor de producción)| 
| **Actor Secundario :** |no hay actor secundario | 
| **Precondiciones:** |el numero de celular debe ser de 9 digitos (+51) , se debería verificar el correo sea existente , la foto de perfil se tendría que agregar en formato png. 
| Paso | Acción |
| 1    |ingresar al apartado de edición de la cuenta|
| 2    |seleccionar que parametro se va editar|
| 3    |subir cambios ya sea en letra o un archivo png|       
| 4    |dar confirmación del cambio|
| 5    |caso terminado|
#### **Caso de uso N°10: depuración de cuenta**:
| **Objetivo:** |permite la eliminación total de la cuenta de la base de datos , esto incluye datos personales , usuario y contraseña|
|------|--------|
| **Descripción:** | el responsable se encarga de eliminar la cuenta ya sea por renuncia o despido
| **Actor Primario:** |gestor de producción| 
| **Actor Secundario :** |no hay actor secundario | 
| **Precondiciones:** |el gestor de la producción tendrá una contraseña especial para acceder a la eliminación de la cuenta
| Paso | Acción |
| 1    |ingresar al apartado de eliminación de la cuenta|
| 2    |digitar la contraseña de acceso para el apartado de eliminación|
| 3    |seleccionar a el usuario que se va eliminar|       
| 4    |dar confirmación de la depuración|
| 5    |actualización de cambios|
| 5    |caso terminado|

#### **Caso de uso N°11: Reportes por operarios**
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

#### **Caso de uso N°12: Reportes por supervisor**
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

### 2. Requerimientos de atributos de calidad
* Seguridad: El sistema debe garantizar la confidencialidad e integridad de los datos almacenados y transmitidos. Para ello, el sistema solo permitirá acceso a los usuarios que están registrados y que cumplan un rol en la empresa, y solicitará que los usuarios proporcionen dos formas de autenticación: una contraseña y un código enviado a su dispositivo móvil.
* Escalabilidad: El sistema debe ser capaz de manejar grandes volúmenes de datos y usuarios en tiempo real.
* Fiabilidad: El sistema debe ser resistente a fallos menores y ser capaz de recuperarse automáticamente sin afectar significativamente la operación. En caso de fallos graves, el tiempo de recuperación no debe superar las 3 horas. Además, se realizará copias de seguridad diarias de los datos del sistema y mantener copias de seguridad históricas durante al menos 90 días.
* Usabilidad: El sistema debe ser fácil de usar y comprender, con una interfaz amigable para los usuarios.
* Compatibilidad: El sistema debe funcionar en múltiples dispositivos, así como en diferentes sistemas operativos y navegadores web.

### 3. Restricciones
* El Backend del sistema se implementará en PostgreSQL
       
[Selección de la empresa](SeleccionEmpresa.md)

[Regresar al índice](../README.md)
