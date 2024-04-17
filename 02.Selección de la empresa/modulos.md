# MODULOS 

## MÓDULO DE LOGIN Y REGISTRO DE USUARIO 

Este módulo se encarga de poder registrar su perfil de usuario, recopliando informació relevante como nombres y cargos de ocupación. Tambien se encarga de poder actualizar la contraseña mediante una verificación mediante una "palabra clave", y si contesta correctamente según la base de datos se procede a actualizar la contraseña. 
1. ingreso de usuario y contraseña : los usarios tendrán asignadas usuarios con sus respectivas contraseñas
2. cambio de contraseña : si el usuario no recuerda la contraseña se le puede dar la función de poder actualizarla mediante un control de seguridad llamado "palabra clave" y si responde correctamente se procede a la actualización de la contraseña
3. actualización de datos de usuario :  se permite la actualización de datos de usuario, como el telefono celular, el correo, la foto de usuario que se quiere presentar en tal perfil
4. depuración de cuenta : en caso de quiere eliminar la cuenta se podrá, solo si se se conoce la contraseña para eliminar el usuario  

## MÓDULO DE REGISTRO DE HERRAMIENTAS Y MAQUINARIAS
Este módulo se encarga de gestionar y mantener un registro detallado de las herramientas y maquinarias utilizadas por los operarios en las actividades diarias de producción. Su objetivo es garantizar un uso eficiente de los recursos y un seguimiento preciso de su disponibilidad y estado. El módulo consiste en lo siguiente:

1. Registro de herramientas y maquinarias: Incluye un catálogo completo de todas las herramientas y maquinarias disponibles en la empresa, especificando detalles como nombre, descripción, número de serie, ubicación y estado de cada elemento.

2. Solicitud de herramientas: Permite a los operarios solicitar las herramientas y maquinarias que necesitan para realizar sus tareas, indicando también la actividad específica que van a llevar a cabo. Esta solicitud puede realizarse a través de un formulario en línea .

3. Asignación y registro de uso: Una vez aprobada la solicitud, se asigna la herramienta o maquinaria al operario correspondiente, y se registra la hora de inicio y finalización de su uso. Esto permite llevar un seguimiento preciso del tiempo de utilización de cada herramienta y planificar su mantenimiento de manera oportuna.

4. Control de inventario: Actualiza automáticamente el inventario de herramientas y maquinarias en función de las solicitudes realizadas y de los registros de uso. De esta manera, se mantiene un inventario actualizado y se evitan situaciones de escasez o exceso de stock.

5. Informe de uso y disponibilidad: Genera informes periódicos sobre el uso de herramientas y maquinarias, incluyendo estadísticas de utilización, tiempos de inactividad, mantenimientos realizados y disponibilidad de equipos. Estos informes son útiles para la toma de decisiones y la optimización de los recursos.

## MÓDULO DE REGISTRO DE ACTIVIDADES
Este módulo se encarga de registar las actividades o trabajos asignados a cada operario, sus responsabilidades son:
1. Mostrar las actividades realizadas al operario: Esto le permitirá ver como es su avances a lo largo de un tiempo determinado y que actividades realizó con satisfacción.
2. Actividades generales de los operarios: Para el gestor de producción le permitirá mostrar las actividades realizadas de los operarios, así como controlar el tiempo de ellos.
3. Estadistica de los operarios: Mostrará un pequeño rendimiento de un operario designado como cuanto tiempo trabaja por día en promedio, si su trabajo es continuo o interrupido por otras actividades, etc.

## MÓDULO DE SOLICITUD DE PEDIDOS DE INSUMOS 

## MÓDULO DE REGISTRO DE CALIDAD
El módulo de Registro de Calidad se encarga de supervisar y garantizar que los productos textiles cumplan con los estándares de calidad establecidos por la empresa. Este módulo registra y analiza los datos relacionados con la calidad de los productos, tanto en términos de materiales como de procesos de producción.

Interacción con otros módulos:

1. Módulo de Herramientas y Maquinarias: 
   - Utiliza información sobre el estado de las herramientas y maquinarias para garantizar que estén en condiciones óptimas y no afecten la calidad del producto.
   - Notifica cuando una herramienta o maquinaria presenta un número alto de usos, lo que puede afectar la calidad del producto

2. Módulo de Registro de Tareas:
   - Recibe información sobre las tareas realizadas por los empleados para verificar si se están siguiendo los procedimientos de calidad establecidos.
   - Analiza el avance en medidas de producción para evaluar la eficiencia y calidad del trabajo realizado.

3. Módulo de Reportes:
   - Genera reportes individuales de calidad para cada empleado, destacando su desempeño en términos de calidad.
   - Produce reportes específicos sobre la calidad de las herramientas y maquinarias utilizadas.
   - Contribuye con información para la generación de reportes macro que permiten analizar el desempeño de los trabajadores bajo la supervisión de ciertos supervisores o de la empresa en general.




## MÓDULO DE REPORTES 

Este módulo se encarga de dar información sobre las actividades concluidas por cada empleado, el estado de las herramientas o el estado de las maquinarias, en forma de reportes; también se encarga de brindar a los empleados su avance en medidas de producción; un último uso que puede brindar es un reporte macro para analizar cómo van los trabajadores de cierto supervisor o de Topitop en general
1. Tomar información del módulo de herramientas y maquinarias, también de registro de tareas para concretar los reportes
2. Generación de reportes individuales de cada empleado
3. Generación de reportes de cada herramienta y maquinaria
4. Notificar cuando una herramienta o maquinaria presenta un número alto de usos

## MÓDULO DE RECLAMOS Y OBSERVACIONES 

Este módulo se encarga de darle un espacio al trabajador de llenar específicamente ciertos inconvenientes que puede tener durante su jornada laboral o con algún trato, también comentar las imperfecciones de algún producto, o problemas con herramientas y maquinarias, esta información se la envía al supervisor y finalmente este lo eleva más o realiza operaciones convenientes para el caso

# INTERACCIONES ENTRE MÓDULOS 

## MÓDULO DE REGISTRO DE ACTIVIDADES CON MÓDULO DE REGISTRO DE CALIDAD
Estos módulos están en constante comunicación para proporcionar información sobre el personal asignado a ciertas tareas de inspección o control(que gestor de producción fue asignado a tal control).
## MÓDULO DE REPORTES CON MÓDULO DE REGISTRO DE ACTIVIDADES
Estos módulos estan relación pues el módulo de registro de actividades le brinda la información de las actividades de los usuarios para que este pueda sintetisarlo y exportarlo mediante un archivo pdf de reporte manual.
