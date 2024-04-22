# Diccionario de datos
### Entidad: Empleado
#### Se refiere a un individuo que trabaja en la división de producción de la empresa TOPITOP, desempeñando roles y tareas relacionadas con la fabricación de productos textiles de acuerdo con los estándares de calidad y diseño establecidos.

|     Atributo     |                  Descripción                  |   Formato   | Naturaleza |  Valores |
|:----------------:|:---------------------------------------------:|:-----------:|:----------:|:--------:|
|    ID_Empleado   |              Código del empleado              |   999999 |   Varchar  | 6 dígitos|
|  Nombre_Empleado |          Nombre del empleado                  |     X(60)    |   char   | NOT NULL |
| Apellido_Empleado|          Apellido del empleado                |     X(60)     |   char  | NOT NULL |
|  DNI_Empleado    |          documento de indentidad del empleado  |  99999999   |  char |  8 dígitos|
|       Cargo      |                Cargo del empleado              |     AAA     |   Varchar  | TAB1 |
|     Teléfono     |        Número de teléfono del empleado        | 999 999 999 |    Char    | 9 dígitos |
|      Correo      | Dirección del correo electrónico del empleado |   999-AAA   |   Varchar  | NOT NULL |
| Fecha_Nacimineto |        Fecha de nacimiento del empleado       |     999     |     Int    | NOT NULL |
|   Sexo              |           Sexo del empleado           |     X(60)    |   String   |TAB2 |


#### TAB 1                                                

|     Cargo    |    Semantica |         
|:---------------:|:-----------------:|
|     C2    |    operario |
| C2 |  gestor de produccion |

#### TAB 2

|     Sexo   |    Semantica |
|:---------------:|:-----------------:|
|     A1    |    Masculino |
| A2 |  Femenino|

### Entidad: Solicitud de Maquinaria
#### Se refiere al pedido realizado por un empleado para el uso de una maquinaria específica en el area producción de la empresa TOPITOP.

|     Atributo     |                  Descripción                  |   Formato   | Naturaleza |  Valores |
|:----------------:|:---------------------------------------------:|:-----------:|:----------:|:--------:|
|    ID_Solicitud |              Código del solicitud              |   999-AAA   |   Varchar  | 6 dígitos|
|  Fecha_Solicitud |          Fecha en que se realiza la solicitud |    YYYY-MM-DD  |  Date  | NOT NULL |
| Estado           |          Estado actual de la solicitud         |   AAA   |   char  | TAB 3 |

#### TAB 3

|     Cargo    |    Semantica |
|:---------------:|:-----------------:|
|     E1    |    Disponible|
| E2 |  Mantenimiento |
| E3 |  Ocupado |

### Entidad: Maquinaria
#### Se refiere al pedido realizado por un empleado para el uso de una maquinaria específica en el area producción de la empresa TOPITOP.

|     Atributo     |                  Descripción                  |   Formato   | Naturaleza |  Valores |
|:----------------:|:---------------------------------------------:|:-----------:|:----------:|:--------:|
|    CODIGO_MAQUINA |              Código de de la maquinaria             |   99999-AA   |   Varchar  | 5 dígitos + 2 letras paridad|
|  Nombre_Maquina |          Nombre de la maquinaria   |  YYYY-MM-DD  |  Date  | NOT NULL |
| Modelo_Maquina        |          Modelo de la maquinaria       |   AAA   |   char  | No null |

