## Requerimientos

### 1. Requerimientos funcionales

#### **Caso de uso N°1: Abastecimiento de la materia prima**

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

| **Objetivo:** | Garantizar un proceso de producción eficiente y seguro en la empresa mediante el conocimiento del uso de las herramientas y maquinarias, así como de los procesos asociados a éstos. |
|------|--------|
| **Descripción:** | Este caso de uso describe el proceso de selección de herramientas y maquinarias por parte del operario. | 
| **Actor:** | Operario | 
| **Precondiciones:** | Se disponen de suficientes herramientas y maquinarias para mantener el flujo de producción de la empresa. | 
| Paso | Acción |
| 1    | El operario comprende a fondo el proceso de producción. Esto le permitirá elegir las herramientas y maquinarias adecuadas para cada tarea específica. |
| 2    | El operario conoce las características técnicas de las herramientas y maquinarias disponibles. Esto incluye detalles como la capacidad, velocidad, precisión, facilidad de uso y mantenimiento. |
| 3    | El operario se asegura de que la herramienta seleccionada se adapte al tipo de trabajo que realizará. |
| 4    | El operario debe evaluar si la herramienta es cómoda de usar durante largos períodos y si cumple con las normas de seguridad. |
| 5    | El operario selecciona la herramienta que le permite una mayor eficiencia y productividad. Además evalúa si la herramienta reduce el tiempo de trabajo y mejora la calidad del producto final. |
| 6    | Luego de seleccionar la herramienta, el operario procede a seleccionar el tiempo de inicio así como el tiempo de finalización del uso de la herramienta. |
| 7    | Finaliza el caso. |

#### **Caso de uso N°3: Registro de los empleados**

| **Objetivo:** | Gestionar de manera eficaz la mano de obra y optimizar los procesos de fabricación. |
|------|--------|
| **Descripción:** | Este caso de uso describe el proceso de registro de la información relacionada con el trabajo de los empleados en las líneas de producción de calzado. | 
| **Actores:** | Operario y Supervisor | 
| **Precondiciones:** | Se disponen de instrumentos de medición que permiten registrar intervalos de tiempo. | 
| Paso | Acción |
| 1    | Se registra la hora de entrada y salida de los empleados en sus jornadas laborales. Esto proporciona un seguimiento preciso del tiempo de trabajo por cada empleado. |
| 2    | Se monitorea el progreso de las tareas asignadas en tiempo real. Los encargados de este módulo pueden verificar el estado de las acividades en curso y realizar ajustes según sea necesario para garantizar que se cumplan los plazos y objetivos de producción. |
| 3    | Se asignan tareas especificas a los empleados en función de sus habilidades y la disponibiidad que tienen, con esto se asegura una distribución equitativa del trabajo y una correcta asignación eficiente de recursos humanos en cada turno de producción. |
| 4    | Se registra el tiempo extra trabajado por los empleados , así como las ausencias de éstos en el trabajo, vacaciones o días libres. También se registran las ausencias no planificadas como enfermedades, con esto se puede garantizar una correcta cobertura adecuada en la línea de producción. |
| 5    | Se generan informes detallados sobre la asistencia y el rendimiento laboral de los empleados. Esto permite generar información valiosa para evaluar la eficiencia operativa, identificar áreas de mejora y tomar mejores decisiones. |
| 6    | Finaliza el caso. |

#### **Caso de uso N°4: Control de calidad**

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
