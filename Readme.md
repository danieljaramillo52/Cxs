
# Tabla de Contenido

[introduccion](#Introduccion)
   1.1 [Glosario](#Glosario-de-terminos)
   1.2 [Consultas](#Lista-de-consultas-para-la-automatizacion-de-Comercial-Nutresa)
   1.3 [Objetivo](#objetivo-de-la-automatizacion)
   1.3 [categorias_calsificación](#categorias-de-clasificacion)
   1.4 [Etapas_de_desarrollo](#etapas-del-desarrollo-del-proceso-de-cxs)
   1.5 [Columnas_adicionales](#columnas-adicionales)
   1.6 [Aclaraciones](#aclaraciones)
   
[Archivos_necesarios_para_la_automatizacion](#archivos-necesarios-para-la-automatización)
   2.1 [Consultas](#Lista-de-consultas-para-la-automatización-de-Comercial-Nutresa)
    2.1.1 [Descripcion_consultas](#descripcion-consultas)
    2.1.2 [Estructura_consultas](#estructura-de-las-consultas)
    2.1.3 [Recomendaciones_consultas](#recomendaciones-consultas)
    2.1.4 [Ubicacion_de_las_consultas_de_ventas.](#ubicacion-de-las-consultas-de-ventas)
   2.2[Drivers](#drivers)
    2.2.1[Driver_DS](#driver-ds)
    2.2.2[Drvier_NO_DS](#driver-no_ds)
    2.2.3[Driver_Cadenas](#driver-cadenas)
    2.2.4[Ubicacion_drivers](#ubicacion-de-los-drivers)
    2.2.5[Recomendaciones y obligaciones para la manipulación de los Drivers.](#recomendaciones-y-obligaciones-drivers)
   2.3[Archivos_de_ventas](#archivos-de-ventas)
    2.3.1[Archivos_necesarios_de ventas](#archivos-necesarios-de-ventas)

3. [Archivo_config.yml](#archivo-configyml)
   3.1 [Estructura y Desglose. (Resumen)](#Estructura-y-Desglose-(Resumen))
   2.2 [Visualizaciones](#Visualizaciones-del-archivo-(config_yml))
   3.3 [Contenido_y_estructura](#contenido-y-estructura-resumen)
   3.4 [Glosario de constantes](#glosario-de-constantes-de-la-automatización)
   3.5 [ParametrizacionesCxS](#Parametrizaciones-requeridas-para-el-proceso-de-CxS)
   3.6 [NO_permitido_modificar](#NO-modificable)
   3.7 [SI_permitido_modificar](#SI-modificable)
   3.8 [Adicional_NO_modificables](#listas-de-información-adicionales-no-modificables)

4. [Responsables](#responsables)

5. [Manual_de_usuario](#enlace-al-manual-de-usuario)

# Proyecto de CxS

## Introducción
Este manual contiene toda la información necesaria para el buen uso del asistente del proceso "Automatización de CxS". Además, se incluye una descripción detallada de archivos, procedimientos e instrucciones sobre el contenido del ejecutable y la estructura de los archivos finales, entre otros.

## Glosario de terminos

| **Término** | **Definición** | 
|---|---|
| **Consultas de informacion** | Las consultas son las fuentes de información principales, contienen toda la información de relacionada la CxS. En esencia se refieren a archivos del tipo xlsx o csv, que serán cargados procesados y cargados en memoria con diferentes funciones. Se divide en tres categorías: Consulta DS, Consulta NO_DS, Consulta Cadenas. Cada consulta contiene un tipo especifico de clientes de CN, a su vez, a cada consulta se le hacen modificaciones y trasformaciones diferentes para prepararlas antes de consolidarlas en el insumo del CxS.|
| **Drivers** | (Definicón) En este contexto de trabajo, un driver tiene un significado similar a una consulta. Son las fuentes de información adicionales, contienen toda la información de relacionada el CxS. En esencia se refieren a archivos del tipo xlsx o csv, que serán cargados procesados y cargados en memoria con diferentes funciones. Estos son los archivos auxiliares, modificables, y parametrizables que sirven para modificar principalmente los datos, más no las estructuras de las consultas. 
|
| **Automatización CxS** | El proceso de CxS es un asistente que utiliza información de algunas bases de datos de clientes de la compañía Comercial Nutresa. De los dos tipos de atención conocidos (Directa e Indirecta), se emplea información de tres consultas de clientes NO_DS, DS, Cadenas |  
| **CxS** | Proceso que calcula todos los gastos destinados al proceso de logística y relacionados, que permitan de manera efectiva y eficiente llevar los productos de Comercial Nutresa a todos sus clientes. La definición concreta va directamente por parte del área encargada de financiera en CN.|

## Objetivo de la automatización.

Este proceso forma parte del proceso completo de CxS, dentro de Comercial Nutresa. El objetivo es consolidar una base de datos con información de ventas, descuentos, gastos, devoluciones entre otras categorías, para todos los clientes de CN, registrados en los “Secos” == “Centros de Costos” de clientes durante un periodo determinado (Mes – Mes) y (Año Móvil). La información es agrupada por las siguientes categorías de clasificación:

### Categorias de clasificacion 
| Categoría | Descripción |
|---|---|
| Sector | La industria a la que pertenece el cliente. |
| Canal | El tipo de cliente, por ejemplo, minorista, mayorista o institucional. |
| Subcanal | Una clasificación más específica del canal, por ejemplo, supermercados, tiendas de conveniencia o restaurantes. |
| Canal Transformado | Una transformación del canal para fines de análisis. |
| Subcanal Transformado | Una transformación del subcanal para fines de análisis. |
| Formato | Actua como nombre del cliente. |
| Formato N.I.F | El formato del establecimiento del cliente, por ejemplo, m2 o número de mesas. |
| Segmento Agrupado | Un grupo de clientes con características similares. |

Así mismo se desprenden ciertas etapas en el proceso de desarrollo: 

### Etapas del desarrollo del proceso de CxS
| Etapa | Descripción |
|---|---|
| Limpieza y transformación de datos | Se limpian y transforman los datos de las tres consultas de clientes. Según los requerimientos |
| Consolidación de datos | Se consolidan los datos de las tres consultas en una sola base de datos. |
| Cálculo de columnas adicionales | Se calculan columnas adicionales con la información disponible. |
| Adición de datos | Se agregan los datos de otros archivos para el cálculo de devoluciones. |

En el proceso de "Cálculo de columnas adicionales" se agregan: 

### Columnas adicionales
<table>
  <thead>
    <tr>
      <th style="text-align: center; width: 200px;" >Columnas adicionales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: center; width: 200px;">Depuración descuentos</td>
    </tr>
    <tr>
      <td style="text-align: center; width: 200px;">Descuentos grupo</td>
    </tr>
    <tr>
      <td style="text-align: center; width: 200px;">Ventas efectivas grupo</td>
    </tr>
    <tr>
      <td style="text-align: center; width: 200px;">Descuentos CN</td>
    </tr>
    <tr>
      <td style="text-align: center; width: 100px;">Ventas netas CN</td>
    </tr>
    <tr>
      <td style="text-align: center; width: 100px;">Venta neta grupo</td>
    </tr>
  </tbody>
</table>

### Aclaraciones.

El proceso de CxS se sirve de los insumos de consultas, de drivers, y de archivos adicionales que contienen las devoluciones en dos categorías principales: compañía y cadenas. Todos los archivos anteriores son parametrizables y se explicará su manejo más adelante en el manual de usuario correspondiente. 

El objetivo final de la automatización es brindar el insumo del cual se sirven las personas encargadas del área financiera y el área de TI de CN,  con el fin de generar una visualización del mismo.

## Archivos necesarios para la automatización

### Lista de consultas para la automatización de Comercial Nutresa

* **Clientes DS:**
    * Clientes que reciben atención modalidad directa de Comercial Nutresa.
* **Clientes No_DS:**
    * Clientes que reciben atención modalidad indirecta de Comercial Nutresa.
* **Consulta Cadenas:**
    * Consulta que obtiene toda la información de los clientes tipo Cadenas atendida por Comercial Nutresa.

**Nota:** Todas estas consultas requieren individualmente una limpieza y transformación de parte de sus datos en la primera parte de la automatización.

---
### Descripcion consultas 

**Consulta NO_DS**

![Consulta_No_DS](Img_Readme/Consulta_NO_DS.png)

* **Nombre:** Consulta CXS Cliente NO_DS
* **Tipo de archivo:** Archivo de Excel
* **Formato de archivo:** Archivos Dinámicos / No contiene macros
* **Macros necesarias para el proceso:** Ninguna
* **Drivers necesarios para el proceso:** Si (Driver_ds, Driver_no_ds)
* **Extensión del archivo:** xlsx
* **Hoja necesaria:** (A parametrizar)
* **Hoja 1**
    * **Nota:** Esta Hoja debe parametrizarse se explicará cómo más adelante.

**Consulta DS**

![Consulta_DS](Img_Readme/Consulta_DS.png)

* **Nombre:** Consultas CXS Cliente DS Mensual (Nombre original al momento de parámetrizar)
* **Tipo de archivo:** Archivo de Excel
* **Formato de archivo:** Archivos Dinámicos / No contiene macros
* **Macros necesarias para el proceso:** Ninguna
* **Drivers necesarios para el proceso:** Si (Driver_ds, Driver_no_ds)
* **Extensión del archivo:** xlsx
* **Hoja necesaria:** (A parametrizar)
* **Hoja 1**
    * **Nota:** Esta Hoja debe parametrizarse se explicará cómo más adelante.

**Consulta cadenas**

![Consulta_Cadenas](Img_Readme/Consulta_Cadenas.png)

* **Nombre:** Consultas CXS Cliente Cadenas (Nombre original al momento de parámetrizar)
* **Tipo de archivo:** Archivo de Excel
* **Formato de archivo:** Archivos Dinámicos / No contiene macros
* **Macros necesarias para el proceso:** Ninguna
* **Drivers necesarios para el proceso:** Si Si (Driver_ds, Driver_no_ds, Driver_Cadenas)
* **Extensión del archivo:** xlsx
* **Hoja necesaria:** (A parametrizar)
* **Hoja 1**
    * **Nota:** Esta Hoja debe parametrizarse se explicará cómo más adelante.


### Estructura de las consultas
Se recomienda no preocuparse por las columnas que se le  adicionaran en el proceso a las consultas, revisar el archivo Estructura_consultas.xlsx para poder conocer el formato, estructura y nombres de las columnas que debe tener de base cada consulta. Las modificaciones posteriores son trabajo y fin de la automatización 

Para verificar la estructura necesaria de esta consulta y las demás, siga estos pasos:

1. Dirijase a la ruta `CxS/Documentacion`

2. Abra el archivo `Estructura_consultas.xlsx`.

3. Consulte la hoja `Estructuras` para obtener información sobre la estructura de la consulta.

### Recomendaciones consultas 

<ul id="requisitos">
  <li>No mover de la carpeta insumos</li>
  <li>No eliminar ninguno de los 3 archivos anteriormente descritos (solo modificarlos en nombre del archivo y/o nombre de la hoja.)</li>
  <li>Verificar que la extensión siempre sea la misma .xlsx</li>
  <li>No cambiar el nombre a la carpeta anterior (Insumos) Ni cambiar su ubicación</li>
  <li>En caso de querer cambiar el nombre (Del archivo o la hoja) cambiar el parámetro (Luego se explicará cómo hacerlo.)</li>
  <li>No agregar a la carpeta archivos adicionales con los mismos nombres que puedan generar conflictos en la automatización.</li>
  <li>Si se desea cambiar el nombre de los archivos se debe hacer parametrizándolos. Proceso que se explicará más adelante.</li>
</ul>

### Ubicacion de las consultas de ventas.
![Ruta_Consultas](Img_Readme/Ruta_consultas.png)

![Consultas](Img_Readme/Consultas.png)


## Drivers.
Estos son los archivos auxiliares, modificables, y parametrizables que sirven para modificar principalmente los datos, más no las estructuras de las consultas de ventas. Se dividen en **drivers ds, no_ds y cadenas**. sin embargo, los drivers no son excluyentes entre sí, es decir, ciertas modificaciones en las consultas requieren de la interferencia e información añadida y parametrizada en 1, 2 o los **3 drivers**.

Por lo tanto, es necesario para la automatización que los 3 se encuentren en la carpeta correspondiente, debidamente diligenciados para obtener los resultados esperados. Dentro de cada driver, se encuentra también una explicación de la utilidad de cada uno de los segmentos de información. el usuario puede modificar los drivers cada vez que quiera en términos de datos, **pero en ningún caso en términos de estructura y organización ya que esto repercute en el desarrollo de la automatización**. Es igual de importante mantener la estructura de los drivers como de las correspondientes consultas de información.

## Driver DS

* **Tipo de archivos:** Archivo de Excel.
* **Formato del archivo:** Archivos Dinámicos / No contiene macros.
* **Macros necesarias para el proceso:** Ninguna
* **Consultas impactadas en el proceso:** Si (Consulta cadena, consulta DS, Consulta NO_DS)
* **Extensión del archivo:** xlsx
* **Hoja Necesaria:** (A parametrizar)

* **Visual del Driver:**

![Driver_DS](Img_Readme/Driver_DS.png)

La hoja del Driver debe parametrizarse como se indicará más adelante. Así mismo se puede parametrizar el nombre del archivo.

![Hoja1](Img_Readme/Hoja1.png)

Nombre genérico para las hojas de los drivers. (Recomendado mantener). 

## Driver NO_DS

* **Tipo de archivos:** Archivo de Excel.
* **Formato del archivo:** Archivos Dinámicos / No contiene macros.
* **Macros necesarias para el proceso:** Ninguna
* **Consultas impactadas en el proceso:** Si (Consulta cadena, consulta DS, Consulta NO_DS)
* **Extensión del archivo:** xlsx
* **Hoja Necesaria:** (A parametrizar)

* **Visual del Driver:**
![Driver_NO_DS](Img_Readme/Driver_no_ds.png)

#### Parte 1 driver NO_DS + Explicacion.
![Driver_NO_DS](Img_Readme/P1_Driver_NO_DS.png)

#### Parte 2 driver NO_DS
![Driver_NO_DS](Img_Readme/P2_Driver_NO_DS.png)

#### Explicacion P2 driver NO_DS.
![Driver_NO_DS](Img_Readme/Explicacion_P2_D_NO_DS.png)

## Driver Cadenas

* **Tipo de archivos:** Archivo de Excel.
* **Formato del archivo:** Archivos Dinámicos / No contiene macros.
* **Macros necesarias para el proceso:** Ninguna
* **Consultas impactadas en el proceso:** Si (Consulta cadena, consulta DS, Consulta NO_DS)
* **Extensión del archivo:** xlsx
* **Hoja Necesaria:** (A parametrizar)

* **Visual del Driver:**
![Driver_NO_DS](Img_Readme/Driver_no_ds.png)

#### Parte 1 driver cadenas 
![Driver_Cadenas](Img_Readme/P1_Driver_Cadenas.png)

#### Explicación P1 driver cadenas
![Explicación_P1_Driver_Cadenas.png](Img_Readme/Explicacion_P1_D_Cad.png)

#### Parte 2 driver cadenas + Explicacion
![Driver_Cadenas](Img_Readme/P2_Driver_Cadenas.png)

#### Parte 3 driver cadenas 
![Driver_Cadenas](Img_Readme/P3_Driver_Cadenas.png)

#### Explicación P3 driver cadenas
![Explicación_P1_Driver_Cadenas.png](Img_Readme/Explicacion_P3_D_Cad.png)

#### Parte 3 driver cadenas 
![Driver_Cadenas](Img_Readme/P4_Driver_Cadenas.png)

#### Explicación P3 driver cadenas
![Explicación_P1_Driver_Cadenas.png](Img_Readme/Explicacion_P4_D_Cad.png)

---

### Ubicacion de los drivers.
![Ruta_Drivers](Img_Readme/Ruta_drivers.png)

![Drivers](Img_Readme/Drivers.png)

#### Recomendaciones y obligaciones Drivers.
<ul>
    <li>No mover los archivos de la carpeta "insumos".</li>
    <li>No eliminar ninguno de los 3 archivos mencionados anteriormente (solo se pueden modificar en nombredelarchivo y/o nombre de la hoja)</li>
    <li>Verificar que la extensión del archivo siempre sea la misma (.xlsx).</li>
    <li>No cambiar el nombre de la carpeta anterior ("Insumos")ni cambiar su ubicación.</li>
    <li>En caso de querer cambiar elnombre del archivo o de la hoja,cambiar el parámetro según las instrucciones proporcionadas.</li>
    <li>No agregar archivos adicionales a la carpeta con los mismos nombres que puedan generar conflictos en la automatización.</li>
    <li>Si se desea cambiar el nombre de los archivos, sedebe hacer parametrizándolos siguiendo el proceso que se explicará más adelante.</li>
    <li>Respetar los nombres de las columnas de cada archivo y mantener la estructura para facilitar la parametrización y reconocimiento fácil.</li>
    <li>Para consultar la estructurade los drivers, se proporcionauna visualización de las columnas utilizadas. Para ver la estructura completa y correcta, consultar "Estructura_consultas.xlsx" dentro de la carpeta de documentación.</li>
    <li><b>Es importante tener encuenta que puede haber nombres repetidos de columnas en los drivers, y esto no debe cambiarse en ninguna columna, especialmente en el driver_cadenas.</b></li>
    </ul>

---

## Archivos de ventas
Los archivos de ventas contienen información adicional sobre ventas, pero se concentran y son de principal interés en el tema de las devoluciones.

**Se dividen en 2 tipos** 
1. `Devoluciones por compañía`
2. `Devoluciones por cadenas`

A su vez, las devoluciones de cada categoria se dividen nuevamente en 2 tipos

1. `Devoluciones malas`
2. `Devoluciones sin asignar` 

El proceso consiste en utilizar la información aquí contenida para hacer una distribución de todas las devoluciones.

### Archivos necesarios de ventas 

**Venta cadenas**

![Ruta_Drivers](Img_Readme/Venta_Cadenas.png)

* **Tipo de archivos:** Archivo de Excel.
* **Formato del archivo:** Archivos Dinámicos / No contiene macros.
* **Macros necesarias para el proceso:** Ninguna
* **Consultas impactadas en el proceso:** Si (Consulta cadena, consulta DS, Consulta NO_DS)
* **Extensión del archivo:** xlsx
* **Hojas Necesarias:** (A parametrizar)
![Hoja_Venta_cadenas](Img_Readme/Hojas_Venta_Cadenas.png)

**Venta general**

![Venta_general](Img_Readme/Venta_General.png)

* **Tipo de archivos:** Archivo de Excel.
* **Formato del archivo:** Archivos Dinámicos / No contiene macros.
* **Macros necesarias para el proceso:** Ninguna
* **Consultas impactadas en el proceso:** Si (Consulta cadena, consulta DS, Consulta NO_DS)
* **Extensión del archivo:** xlsx
* **Hojas necesarias:** (A parametrizar)
![Ruta_Drivers](Img_Readme/Hojas_Venta_Cadenas.png)


Nuevamente para consultar la estructura del archivo de ventas, se da una visualización de las columnas utilizadas. 
Si se quiere ver la estructura correcta completa, consultar Estructura_consultas.xlsx dentro de la carpeta de documentación para verificar estructura

---

## Archivo (config.yml)
![Archivo_cofing](Img_Readme/config_yml.png)

* **Tipo de archivo**  Archivo yml (De parámetros)
* **Formato del archivo** (yml) (Formato especial de archivo de texto para parametrizar)

### Estructura y Desglose (Resumen)

* **Consultas** 
1. Consulta CXS Cliente NO_DS.xlsx
2. Consultas CXS Cliente Cadenas.xlsx
3. Consultas CXS Cliente DS Mensual.xlsx

* **Drivers**
1. Driver_cadenas.xslx
2. Driver_ds.xlsx
3. Driver_no_ds.xlsx

* **Ventas**
1. Automatico Venta NETA (Cadenas).xlsx
2. Automatico Venta NETA (General).xlsx

Estos son los nombres registrados en el archivo config.yml actualmente en funcionamiento a la fecha de entrega del manual. Los nombres por manejar un estándar podrían mantenerse de esta manera y así ahorrar tiempo en temas de parametrización

--- 

### Visualizaciones del archivo (config_yml) 
`Diferentes visualizaciones del mismo archivo` 

![Ruta_Drivers](Img_Readme/visual_config_VSC.png)

![Ruta_Drivers](Img_Readme/visual_config_block_notas.png)

![Ruta_Drivers](Img_Readme/visual_config_Notepad++.png)

Las anteriores son visualizaciones para trabajar el **config.yml**, presente en la automatización. Dichas visualizaciones corresponden a los programas. 

#### Editor de código (USO NO RECOMENDADO) 

![Visual_VSC](Img_Readme/visual_VSC.png)

#### Block de notas (USO NO RECOMENDADO) 

![visual_block_notas](Img_Readme/visual_block_notas.png)

#### Notepad++ (USO RECOMENDADO)

![visual_notedpadd++](Img_Readme/visual_Notepad++.png)

--- 

### Contenido y estructura (Resumen)

#### Rutas de las Carpetas Insumos/Drivers/Ventas/Resultados
![Ruta_Drivers](Img_Readme/rutas_insumos.png)

Carpetas que contienen los insumos para correr toda la automatización, y además donde se  pueden consultar los resultados luego de ejecutarla. Así mismo, esta configuración da la   ruta para leer y guardar. **Esta parte no se cambia, no se toca, NO se modifica en  ninguna circunstancia.**

--- 

### Glosario de constantes de la automatización
Contiene palabras o frases clave, utilizadas repetidamente durante el proceso de automatización en todos los módulos correspondientes. El manejo de estas constantes permite invocar las “cadenas clave” usadas repetidamente en diferentes partes, sin la necesidad de quemar textos o crear variables adicionales. 

| # | Nombre en Mayúsculas | Significado |
|---|----------------------|-------------|
| 1 | TIPO_NO_DS           | "No_DS"     |
| 2 | TIPO_DS              | "DS"        |
| 3 | TIPO_CADENAS         | "Cadenas"   |
| 4 | TIPO_VENTA_COMP      | "Venta NETA (Comp)" |
| 5 | TIPO_VENTA_CADENAS   | "Venta NETA (Cadenas)" |
| 6 | VENTA_COMP           | "Venta_comp" |
| 7 | VENTA_CADENAS        | "Venta_cad" |
| 8 | CONCATENADA_GB_VN     | "Concatenada_gb_vn" |
| 9 | COLS_AGREGAR         | "cols_para_agregar" |
| 10| CONSULTAS            | "Consultas" |
| 11| VENTAS               | "Ventas" |
| 12| NUM_SHEET            | "num_sheet" |
| 13| CONSULTA_DS          | "consultas_ds" |
| 14| CONSULTA_NO_DS       | "consultas_no_ds" |
| 15| CONSULTA_CADENAS     | "consultas_cadenas" |
| 16| COLS_NUEVAS          | "nuevas_cols" |
| 17| SEGMENTO_AGRUP       | "Segmento_Agrup" |
| 18| CENTRO_COS           | "Centro_Costo" |
| 19| NOM_CENTRO_COS       | "Nombre_Centro_Costo" |
| 20| CONCATENADA          | "concatenada" |
| 21| CANAL                | "Canal" |
| 22| SUBCANAL             | "Subcanal" |
| 23| RAMO_CLAVE           | "Ramo_clave" |
| 24| CANAL_TRANS          | "Canal_Trans" |
| 25| SUBCANAL_TRANS       | "Subcanal_Trans" |
| 26| SEGMENTO_TRANS       | "Segmento_Trans" |
| 27| FORMATO              | "Formato" |
| 28| FORMATO_NIF          | "Formato N.I.F" |
| 29| FIL_SIN_ASIGNAR      | "Sin asignar" |
| 30| FIL_NUMERAL          | "#" |
| 31| FIL_DOBLE_NUMERAL    | "#/#" |
| 32| FIL_NULL             | "NaN" |
| 33| FILLNA               | "fillna" |
| 34| DROP                 | "drop" |
| 35| ASTYPE               | "astype" |
| 36| UNION                | "Union" |
| 37| NIF                  | "NIF" |
| 38| FORMAT               | "FORMAT" |
| 39| CLASIFICACION        | "Clasificacion" |
| 40| CLIENTE_CET          | "Cliente CET" |
| 41| CLIENTE              | "Cliente" |
| 42| DISTRIBUIDORES       | "Distribuidores" |
| 43| TRADICIONAL          | "Tradicional" |
| 44| AGENTE_COMERCIAL     | "Agente comercial" |
| 45| CANAL_DIST           | "Canal Distribucion / Segmento 1" |
| 46| COLS_NECESARIAS_VENTAS_M | "cols_necesarias_v_malas" |
| 47| COLS_NECESARIAS_VENTAS_SA | "cols_necesarias_v_sin_asignar" |
| 48| COL_GRANDES_CADENAS  | "Grandes Cadenas" |
| 49| SECTOR               | "Sector" |
| 50| SUBCANAL_SEGMENTO_2  | "Sub Canal / Segmento 2" |
| 51| DEVS_SA              | "Devs. Sin Asignar" |
| 52| DEVS_MALAS           | "Devoluciones Malas" |
| 53| DEVS_MALAS_COL_FINAL | "Devoluciones_malas" |
| 54| DEVS_COL_FINAL_MA    | "Devoluciones_MA" |
| 55| DEVS_COL_FINAL_SA    | "Devoluciones_SA" |
| 56| CONCATENADA_COMP     | "concatenada_COMP" |
| 57| CONCATENADA_CAD      | "concatenada_CADENAS" |
| 58| OFICINA_VENTAS       | "Oficina_ventas" |
| 59| OFICINA_VENTAS_AGRUP | "Oficina_ventas_Agrup" |
| 60| VENTA_EFECTIVA       | "Ventas_Efectivas" |
| 61| VENTA_NETAS_CN       | "Ventas_Netas_CN" |
| 62| VENTA_NETAS_GRUPO    | "Ventas_Netas_Grupo" |
| 63| VENTA_EFECTIVA_GRUPO | "Ventas_Efectivas_Grupo" |
| 64| VENTA_EFECTIVA_FINAL | "Ventas_Efectivas_Final" |
| 65| GASTO_PROM_COMER     | "Gasto_Prom_Comercializadores" |
| 66| DESCUENTOS           | "Descuentos" |
| 67| DESCUENTOS_NG        | "Descuentos_NG" |
| 68| DESCUENTOS_CN        | "Descuentos_CN" |
| 69| DEPURACION_DCTOS     | "Depuracion_Dctos" |
| 70| DESCUENTOS_GRUPO     | "Dctos_Grupo" |
| 71| DEVS_PARAMETRO       | 840612330 |


**Nota:**
Todo lo contenido en el glosario de constantes NO debe ser alterado ni modificado, cualquier cambio en el glosario llevaría a errores en la automatización. 

**Excepción:** Puede y debe ser modificada la última constante del Glosario: 

![DEVS_PARAMETRO](Img_Readme/DEVS_PARAMETRO.png)

--- 

### Parametrizaciones requeridas para el proceso de CxS.

#### Consultas: 
Existen 3 consultas principales de información ya tratadas en este manual. Las 3 consultas deben ser modificadas en 3 parámetros específicos.

1.	El nombre de la consulta.
2.	El nombre de la hoja u Hojas de Excel que vamos a utilizar. 
3.	El número de hojas que poseen las consultas. 

Estos tres parámetros están identificados como: 

![DEVS_PARAMETRO](Img_Readme/parametro_consultas.png)

Podemos apreciar que se trata de la **Consulta CXS Cliente NO_DS.xlsx** y evidentemente el nombre el archivo de Excel es exactamente este. 

<p align="center">
  <img src="Img_Readme/consulta_cliente NO_DS.png">
</p>

Al abrirlo, podemos encontrar coincidencias con el nombre de la hoja y el numero de hojas disponibles. En efecto, tenemos una sola hoja y con el nombre especificado. 

<p align="center">
  <img src="Img_Readme/Hoja_consulta.png">
</p>

Similarmente este mismo proceso se comparte para las otras dos consultas. 

<p align="center">
  <img src="Img_Readme/parametro_consultas_2.png">
</p>

Podemos notar que esta vez hay dos hojas. Correspondientes a las dos hojas que tenemos en Sheet. Y adicionalmente notar que como tenemos `2 hojas` =  `num_sheet = 2.`

**Finalmente, para la consulta cadenas tenemos.** 

<p align="center">
  <img src="Img_Readme/parametro_consultas_3.png">
</p>

Podemos notar que el titulo se pone exactamente igual al nombre del archivo que tenemos Además, pasa exactamente lo mismo con el nombre de la hoja a la cual nos estamos refiriendo. 

---

### Parametrización de hojas (casos posibles)

#### Caso 1

Cuando se trata de una consulta de **varias hojas**, como en este caso DS que contiene las hojas **"Otros"** y **"Cafe y Chocolates"**, la forma de parametrizarlas es escribir entre dos corchetes una al lado de las otras, ambas separadas por comas.

<p align="center">
  <b>[Otros, Cafe y Chocolates]</b>
</p>

#### Caso 2

Supongamos que tenemos un archivo de Excel para esta automatización que contiene 3 hojas llamadas: **“Cárnicos”**, **“Helados y Galletas”**, y **“Pastas”**. Hay que recordar que no debemos incluir ortografía, por lo que debemos entrar al archivo de Excel correspondiente y reemplazar el nombre **(Cárnicos)** a **(Carnicos)**. Posteriormente, en el reglón **sheet** escribir

<p align="center">
  <b>[Carnicos, Helados y Galletas, Pastas]</b>
</p>

#### Caso 3

Si por algún motivo solo tenemos una hoja no olvidar que debemos usar también los corchetes. Supongamos que tenemos una hoja llamada **“Hoja1”** entonces debemos en el reglón **Sheet** escribir 

<p align="center">
  <b>[Hoja1]</b>
</p>

---
### Advertencia
A pesar de ser repetitivo, es preciso señalar que son muy importantes las mayúsculas y la ortografía, y en este tipo de archivos NO se usan tildes, ni caracteres especiales, ya que causan inconvenientes a la hora de procesar el archivo.**Los espacios sonimportantes: Si una hoja en Excel contiene un espacio al principio o al final se debeeliminar ya que podría generar conflictos e incompatibilidades.** 

---
---

### NO modificable 


#### 1. Consultas
| Parámetro         | ¿Es valido modificar? |
|-------------------|------------------------|
| file_name         | SI                     |
| type              | NO                     |
| num_sheet         | SI                     |
| cols              | SI                     |
| nuevas_cols       | SI                     |
| cols_para_agregar | NO                     |

***Se aplica para todas las consultas***

#### 2. Drivers

<p align="center">
  <img src="Img_Readme/Drivers_config.png">
</p>

Nada debe modificarse del archivo correspondiente ninguno de los parámetros en la imagen anterior. En caso de modificaciones necesarias para los drivers requiere modificaciones de todo el proceso. 

#### 3. Archivos de ventas 

Totalmente igual a la gestión de las consultas se hace la gestión de los archivos de ventas
1.	 El nombre de la hoja u Hojas de Excel que vamos a utilizar. 

2.	El nombre del archivo de ventas.

3.	El número de hojas que poseen las consultas. 

Estos tres parámetros están identificados de igual manera que los parámetros de las consultas que vimos anteriormente. 

<p align="center">
  <img src="Img_Readme/ventas_config.png">
</p>

| Parámetro         | ¿Es valido modificar? |
|-------------------|------------------------|
| file_name         | SI                     |
| type              | NO                     |
| num_sheet         | NO                     |
| cols              | NO                     |
| cols_necesarias_v_malas       | NO                     |
| cols_necesarias_v_sin_asignar | NO                     |


#### SI modficable

##### Diccionario sin_asignar DS
<p align="center">
  <img src="Img_Readme/Dict_SA_DS.png">
</p>

Este diccionario se encarga de modificar los clientes sin asignar de todo el archivo consulta_DS, este diccionario debe ser modificado si se quiere o espera cambiar los sin asignar de la consulta DS 

##### Diccionario de regiones.
<p align="center">
  <img src="Img_Readme/Regiones.png">
</p>

Este diccionario se encarga de actualizar las regiones si sufren algunos cambios. Sirve para asociar las varias regiones a una region agrupadadora. 

#### 6. Reemplazos. 
<p align="center">
  <img src="Img_Readme/Reemplazos.png">
</p>

Si se debe hace algún reemplazo en específico sobre la data se eliminan los textos a la derecha de los: y se dentro de las comillas se hace el cambio especifico. Tanto las comillas, como las comas al final son importantes para el proceso. 

### Listas de información adicionales NO modificables

![DEVS_PARAMETRO](Img_Readme/No_modificable_1.png)

![DEVS_PARAMETRO](Img_Readme/No_modificable_2.png)

---
---
 
## Responsables
### Provededor - XpertGroup.
* Daniel jaramillo Bustamante - daniel.jaramillo@xpertgroup.co

### Receptor - Comercial Nutresa.
* **Aréa TI:**
    * Sebastián Caro Aguirre scaro@comercialnutresa.com.co

## Enlace al manual de usuario. 
[Manual de Usuario](ManualDeUsuario.md) 

<link rel="stylesheet" href="Readme.css">
