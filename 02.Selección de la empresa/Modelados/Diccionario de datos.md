# Diccionario de datos
### Entidad: Operario
#### Se refiere a un individuo que trabaja en la división de producción de la empresa TOPITOP, desempeñando roles y tareas relacionadas con la fabricación de productos textiles de acuerdo con los estándares de calidad y diseño establecidos.

|     Atributo     |                  Descripción                  |   Formato   | Naturaleza |  Valores |
|:----------------:|:---------------------------------------------:|:-----------:|:----------:|:--------:|
|    ID_operario  |              Código del operario             |   999999 |   Varchar  | 6 dígitos|
|  Nombre_operario |          Nombre del empleado                  |     X(60)    |   char   | NOT NULL |
| Apellido_operario|          Apellido del empleado                |     X(60)     |   char  | NOT NULL |
|  DNI_operario   |          documento de indentidad del empleado  |  99999999   |  char |  8 dígitos|
|     Teléfono     |        Número de teléfono del empleado        | 999 999 999 |    Char    | 9 dígitos |

### Entidad: Gestor de Produccion
#### Se refiere a un individuo que trabaja en la gestion de producción de la empresa TOPITOP, desempeñando roles y tareas relacionadas con  organizar, dirigir y controlar todas las actividades relacionadas con la producción, con el objetivo de garantizar la eficiencia y rentabilidad de la empresa

|     Atributo     |                  Descripción                  |   Formato   | Naturaleza |  Valores |
|:----------------:|:---------------------------------------------:|:-----------:|:----------:|:--------:|
|    ID_gestor  |              Código del operario             |   999999 |   Varchar  | 6 dígitos|
|  Nombre_gestor |          Nombre del empleado                  |     X(60)    |   char   | NOT NULL |
| Apellido_gestor|          Apellido del empleado                |     X(60)     |   char  | NOT NULL |
|  DNI_gestor    |          documento de indentidad del empleado  |  99999999   |  char |  8 dígitos|
|     Teléfono     |        Número de teléfono del empleado        | 999 999 999 |    Char    | 9 dígitos |


### Entidad: Solicitud de herramienta
#### Se refiere al pedido realizado por un empleado para el uso de una maquinaria específica en el area producción de la empresa TOPITOP.

|     Atributo     |                  Descripción                  |   Formato   | Naturaleza |  Valores |
|:----------------:|:---------------------------------------------:|:-----------:|:----------:|:--------:|
|    ID_Solicitud |              Código del solicitud              |   9999-AAA   |   Varchar  | 4 dígitos + 3 letras paridad|
|  Fecha_Solicitud |          Fecha en que se realiza la solicitud |    YYYY-MM-DD  |  Date  | NOT NULL |
| Estado           |          Estado actual de la solicitud         |   AAA   |   char  | TAB 1 |

#### TAB 1

|     Cargo    |    Semantica |
|:---------------:|:-----------------:|
|     E1    |    Disponible|
| E2 |  Mantenimiento |
| E3 |  Ocupado |

### Entidad: Herramienta
#### Se refiere al pedido realizado por un empleado para el uso de una maquinaria o herramienta específica en el area producción de la empresa TOPITOP.

|     Atributo     |                  Descripción                  |   Formato   | Naturaleza |  Valores |
|:----------------:|:---------------------------------------------:|:-----------:|:----------:|:--------:|
|  ID_herramienta |              Código de de la maquinaria             |   99999-AA   |   Varchar  | 5 dígitos + 2 letras paridad|
|  Nombre_Herramienta |          Nombre de la maquinaria   |  YYYY-MM-DD  |  Date  | NOT NULL |
| Modelo_Herramienta        |          Modelo de la maquinaria       |   AAA   |   char  | No null |
| tiempo de uso       |          tiempo de uso la maquinaria       |   99:99 H   |   time | No null |

### Entidad: Insumo
#### Se refiere a los insumos utilizados en el proceso de producción de la empresa. Los operarios pueden realizar solicitudes de pedido de insumos a través del sistema.
|     Atributo      |              Descripción                  |   Formato   | Naturaleza |  Valores |
|:-----------------:|:-----------------------------------------:|:-----------:|:----------:|:--------:|
|   id_insumo       |        Código del insumo                  |   999999    |   Varchar  | 6 dígitos|
|   tipo_insumo     |        Tipo de insumo                      |     X(60)   |   Char     | NOT NULL |
|   cantidad_insumo |        Cantidad del insumo                 |     999     |   Int      | NOT NULL |
|   id_proveedor    |        Código del proveedor del insumo     |   999999    |   Varchar  | 6 dígitos|

### Entidad: FALLO
#### P.

|     Atributo      |              Descripción                  |   Formato   | Naturaleza |  Valores |
|:-----------------:|:-----------------------------------------:|:-----------:|:----------:|:--------:|
|   ID_FALLO        |                                           |             |   Varchar  | 6 dígitos|
| DESCRIPCION_FALLO |                                           |             |   Char     | NOT NULL |

  
### Entidad: INSPECCION
#### P.

|     Atributo      |              Descripción                  |   Formato   | Naturaleza |  Valores |
|:-----------------:|:-----------------------------------------:|:-----------:|:----------:|:--------:|
|   ID_FALLO        |                                           |             |   Varchar  | 6 dígitos|
| DESCRIPCION_FALLO |                                           |             |   Char     | NOT NULL |



  ### Entidad: MANTENIMIENTO_HERRA_MAQUIN
#### P.

|     Atributo      |              Descripción                  |   Formato   | Naturaleza |  Valores |
|:-----------------:|:-----------------------------------------:|:-----------:|:----------:|:--------:|
|   ID_FALLO        |                                           |             |   Varchar  | 6 dígitos|
| DESCRIPCION_FALLO |                                           |             |   Char     | NOT NULL |



  ### Entidad: ESTANDAR_CALIDAD
#### P.

|     Atributo      |              Descripción                  |   Formato   | Naturaleza |  Valores |
|:-----------------:|:-----------------------------------------:|:-----------:|:----------:|:--------:|
|   ID_FALLO        |                                           |             |   Varchar  | 6 dígitos|
| DESCRIPCION_FALLO |      



### Entidad: Reportes
#### Se refiere al pedido realizado por un empleado para el uso de una maquinaria específica en el area producción de la empresa TOPITOP.

|     Atributo     |                  Descripción                  |   Formato   | Naturaleza |  Valores |
|:----------------:|:---------------------------------------------:|:-----------:|:----------:|:--------:|
|    ID_REPORTE |              Código del reporte            |   999AAA9   |   Varchar  | <999 caracteres alfanumericos|
|  FECHA_REPORTE |          Fecha del reporte   |  YYYY-MM-DD  |  Date  | NOT NULL |
| HORA_REPORTE      |          Hora del reporte       |   HH-MM   |   Date  | NOT NULL |
| TIPO_REPORTE      |          Tipo de reporte       |   AAA   |   char  | TAB 2 |

#### TAB 2

|     Tipo de reporte    |    Semantica |
|:---------------:|:-----------------:|
|     R1    |    Reporte por herramienta|
| R2 |  Reporte por maquinaria |
| R3 |  Reporte por operario |
| R4 |  Reporte por operaro (visualización del operario) |
  
