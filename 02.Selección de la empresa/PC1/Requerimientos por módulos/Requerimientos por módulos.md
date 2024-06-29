### 1. Requerimientos por modulos
- [MÓDULO DE CALIDAD DE HERRAMIENTAS Y MAQUINARIA]()
- [MÓDULO DE CALIDAD DE PROCESOS]()
- [MÓDULO DE GESTION DE HERRAMIENTAS Y MAQUINARIAS]()
- [MÓDULO DE RECLAMOS Y OBSERVACIONES]()
- [MÓDULO DE REGISTRO DE ACTIVIDADES]()
- [MÓDULO DE REPORTES]()
- [MÓDULO DE SOLICITUD DE PEDIDOS DE INSUMOS]()


### 2. Requerimientos de atributos de calidad
* Seguridad: El sistema debe garantizar la confidencialidad e integridad de los datos almacenados y transmitidos. Para ello, el sistema solo permitirá acceso a los usuarios que están registrados y que cumplan un rol en la empresa, y solicitará que los usuarios proporcionen dos formas de autenticación: una contraseña y un código enviado a su dispositivo móvil.
* Escalabilidad: El sistema debe ser capaz de manejar grandes volúmenes de datos y usuarios en tiempo real.
* Fiabilidad: El sistema debe ser resistente a fallos menores y ser capaz de recuperarse automáticamente sin afectar significativamente la operación. En caso de fallos graves, el tiempo de recuperación no debe superar las 3 horas. Además, se realizará copias de seguridad diarias de los datos del sistema y mantener copias de seguridad históricas durante al menos 90 días.
* Usabilidad: El sistema debe ser fácil de usar y comprender, con una interfaz amigable para los usuarios.
* Compatibilidad: El sistema debe funcionar en múltiples dispositivos, así como en diferentes sistemas operativos y navegadores web.

### 3. Restricciones
* El Backend del sistema se implementará en PostgreSQL
       
[Selección de la empresa](SeleccionEmpresa.md)

[Regresar al índice](../../README.md)
