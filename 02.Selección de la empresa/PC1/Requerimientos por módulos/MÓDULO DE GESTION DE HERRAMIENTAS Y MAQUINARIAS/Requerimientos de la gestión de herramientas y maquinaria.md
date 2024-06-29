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
