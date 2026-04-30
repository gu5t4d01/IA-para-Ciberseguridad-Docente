# Unidad 1: El Paisaje de Amenazas Moderno

Esta unidad establece la base del curso, explorando la transformación de la ciberseguridad y cómo los atacantes generan rastros digitales en los entornos corporativos.

## Resultado de Aprendizaje
Identificar los tipos de ciberataques vigentes, comprender cómo los atacantes generan rastros en los registros corporativos y reconocer el valor de los datos como insumo fundamental para la detección automatizada de amenazas.

## Temas de Estudio
* ¿Por qué la ciberseguridad necesita inteligencia artificial hoy?
* Evolución de los ciberataques: de los virus a las amenazas persistentes avanzadas (APT).
* Cómo los atacantes dejan rastros en los datos: las cinco fases del ataque y los eventos que generan.
* Introducción a los datos de seguridad: logs de autenticación, tráfico de red, endpoint y email.

## Caso de Estudio
* **El ataque a SolarWinds (2020):** Análisis de cómo una operación de alta sofisticación permaneció activa durante nueve meses y qué señales dejó en los datos que modelos analíticos podrían haber detectado.

## Actividad Evaluativa: Cazador de rastros
Análisis de un conjunto de eventos de seguridad simplificados correspondientes a un ataque real anonimizado para identificar la fase del ataque y proponer modelos de detección.

# Lab 01 — Exploración de Datos de Ciberseguridad

## 1. Propósito del laboratorio

Este laboratorio introduce al estudiante en la exploración inicial de datos de ciberseguridad usando Python y Google Colab.

El objetivo no es construir todavía un modelo de inteligencia artificial, sino aprender a leer, explorar e interpretar un dataset de seguridad.

Durante el laboratorio se trabajará con un dataset público utilizado en ejercicios académicos de detección de intrusiones.

La pregunta guía del laboratorio es:

> ¿Qué podemos aprender sobre posibles amenazas observando únicamente los datos?

---

## 2. Objetivos de aprendizaje

Al finalizar este laboratorio, el estudiante será capaz de:

- Cargar un dataset público de ciberseguridad.
- Reconocer la estructura básica de un dataset de red.
- Identificar protocolos, servicios y etiquetas de ataque.
- Diferenciar tráfico normal de tráfico malicioso.
- Calcular proporciones básicas del dataset.
- Identificar eventos asociados a reconocimiento o escaneo.
- Generar una gráfica sencilla.
- Redactar hallazgos en lenguaje de ciberseguridad.

---

## 3. Herramientas necesarias

Para este laboratorio se requiere:

- Cuenta de Google.
- Acceso a Google Colab.
- Navegador web actualizado.
- Conexión a internet.

No se requiere instalar:

- Python local.
- Anaconda.
- Jupyter Notebook.
- Herramientas de hacking.
- Librerías manualmente.

---

## 4. Apertura del notebook en Google Colab

Ingresar a Google Colab y crear un nuevo notebook.

Renombrar el archivo como:

```text
Lab_01_Exploracion_Datos_Ciberseguridad.ipynb
```

Google Colab guardará el notebook en Google Drive.

---

# 5. Desarrollo del laboratorio

A continuación se presentan los pasos que debe ejecutar el estudiante dentro de Google Colab.

Cada paso incluye:

- explicación breve;
- celda de código;
- preguntas orientadoras.

---

## Paso 1 — Importar pandas

### Código

```python
import pandas as pd
```

### Explicación

`pandas` es una librería de Python que permite trabajar con datos en forma de tablas.

En este laboratorio se utilizará para cargar, visualizar y explorar el dataset.

### Pregunta

1. ¿Para qué se usa `pandas` en este laboratorio?

---

## Paso 2 — Definir las columnas del dataset

### Código

```python
column_names = [
    "duration","protocol_type","service","flag","src_bytes",
    "dst_bytes","land","wrong_fragment","urgent","hot",
    "num_failed_logins","logged_in","num_compromised",
    "root_shell","su_attempted","num_root",
    "num_file_creations","num_shells","num_access_files",
    "num_outbound_cmds","is_host_login","is_guest_login",
    "count","srv_count","serror_rate","srv_serror_rate",
    "rerror_rate","srv_rerror_rate","same_srv_rate",
    "diff_srv_rate","srv_diff_host_rate","dst_host_count",
    "dst_host_srv_count","dst_host_same_srv_rate",
    "dst_host_diff_srv_rate","dst_host_same_src_port_rate",
    "dst_host_srv_diff_host_rate","dst_host_serror_rate",
    "dst_host_srv_serror_rate","dst_host_rerror_rate",
    "dst_host_srv_rerror_rate","label","difficulty"
]
```

### Explicación

El archivo original del dataset no trae nombres de columnas claros para el análisis.

Por eso se define una lista llamada `column_names`, que permite asignar nombres comprensibles a cada campo.

### Pregunta

2. ¿Por qué es importante asignar nombres de columnas antes de analizar un dataset?

---

## Paso 3 — Cargar el dataset

### Código

```python
url = "https://raw.githubusercontent.com/defcom17/NSL_KDD/master/KDDTrain+.txt"

data = pd.read_csv(url, names=column_names)
```

### Explicación

Este paso carga el dataset desde una URL pública y lo convierte en una tabla llamada `data`.

### Pregunta

3. ¿Qué representa la variable `data` dentro del laboratorio?

---

## Paso 4 — Ver los primeros registros

### Código

```python
data.head()
```

### Explicación

Este paso permite observar las primeras filas del dataset.

Cada fila representa un evento o conexión de red.

Cada columna representa una característica del evento.

### Preguntas

4. ¿Qué observa en las primeras filas del dataset?  
5. ¿Qué representa una fila del dataset?  
6. Mencione tres columnas que podrían ser útiles para un análisis de seguridad.

---

## Paso 5 — Ver el tamaño del dataset

### Código

```python
data.shape
```

### Explicación

Este paso permite conocer cuántos registros y columnas tiene el dataset.

### Preguntas

7. ¿Cuántos registros tiene el dataset?  
8. ¿Cuántas columnas tiene el dataset?  
9. ¿Por qué es relevante conocer el tamaño del dataset antes de analizarlo?

---

## Paso 6 — Analizar protocolos

### Código

```python
data["protocol_type"].value_counts()
```

### Explicación

Este paso permite identificar qué protocolos aparecen en el dataset y cuántas veces aparece cada uno.

### Preguntas

10. ¿Qué protocolos aparecen en el dataset?  
11. ¿Cuál es el protocolo más frecuente?  
12. ¿Qué puede indicar la distribución de protocolos desde el punto de vista de seguridad?

---

## Paso 7 — Analizar servicios

### Código

```python
data["service"].value_counts().head(10)
```

### Explicación

Este paso permite identificar los servicios más frecuentes registrados en el dataset.

### Preguntas

13. ¿Cuáles son los servicios más frecuentes?  
14. ¿Qué servicios considera más relevantes desde el punto de vista de ciberseguridad?  
15. ¿Qué podría representar un servicio como `private`?  
16. ¿Un servicio poco claro o no clasificado debe considerarse automáticamente malicioso? Justifique.

---

## Paso 8 — Analizar etiquetas de eventos

### Código

```python
data["label"].value_counts().head(15)
```

### Explicación

La columna `label` permite identificar si un evento corresponde a tráfico normal o a un tipo de ataque.

### Preguntas

17. ¿Cuál es la etiqueta más frecuente?  
18. ¿Qué etiquetas corresponden a tráfico normal?  
19. ¿Qué etiquetas corresponden a posibles ataques?  
20. ¿Cuál parece ser el ataque más frecuente?  
21. ¿El ataque más frecuente es necesariamente el más crítico? Justifique.

---

## Paso 9 — Separar tráfico normal y ataque

### Código

```python
data["tipo_evento"] = data["label"].apply(lambda x: "normal" if x == "normal" else "ataque")

data["tipo_evento"].value_counts()
```

### Explicación

Este paso crea una nueva columna llamada `tipo_evento`.

Esta columna agrupa los registros en dos categorías:

- `normal`
- `ataque`

### Preguntas

22. ¿Cuántos eventos normales existen?  
23. ¿Cuántos eventos de ataque existen?  
24. ¿Qué utilidad tiene agrupar las etiquetas en dos categorías: `normal` y `ataque`?

---

## Paso 10 — Calcular porcentaje de tráfico normal y ataque

### Código

```python
data["tipo_evento"].value_counts(normalize=True) * 100
```

### Explicación

Este paso permite calcular qué porcentaje del dataset corresponde a tráfico normal y qué porcentaje corresponde a ataques.

### Preguntas

25. ¿Qué porcentaje del dataset corresponde a tráfico normal?  
26. ¿Qué porcentaje corresponde a ataques?  
27. ¿Este balance se parece a lo que esperaría encontrar en un entorno real de SOC? Explique.

---

## Paso 11 — Comparar bytes enviados

### Código

```python
data.groupby("tipo_evento")["src_bytes"].describe()
```

### Explicación

La columna `src_bytes` representa los bytes enviados desde el origen.

En este paso se comparan los valores de `src_bytes` entre eventos normales y eventos de ataque.

### Preguntas

28. ¿Qué diferencias observa en `src_bytes` entre tráfico normal y ataques?  
29. ¿El promedio de bytes enviados es suficiente para sacar una conclusión?  
30. ¿Por qué es importante revisar también la mediana, los mínimos y los máximos?  
31. ¿Qué podría indicar un valor extremadamente alto en `src_bytes`?

---

## Paso 12 — Ver eventos con más bytes enviados

### Código

```python
data.sort_values("src_bytes", ascending=False)[
    ["protocol_type", "service", "flag", "src_bytes", "dst_bytes", "label", "tipo_evento"]
].head(10)
```

### Explicación

Este paso permite revisar los eventos con mayor cantidad de bytes enviados desde el origen.

El objetivo es observar si existen valores atípicos y analizar su contexto.

### Preguntas

32. ¿Qué etiquetas aparecen entre los eventos con más bytes enviados?  
33. ¿Qué servicios aparecen en esos eventos?  
34. ¿Un evento con muchos bytes enviados debe considerarse automáticamente malicioso? Justifique.  
35. ¿Qué otras columnas revisaría antes de concluir que hay un incidente?

---

## Paso 13 — Identificar ataques de reconocimiento

### Código

```python
recon_labels = ["portsweep", "ipsweep", "nmap", "satan"]

data[data["label"].isin(recon_labels)]["label"].value_counts()
```

### Explicación

En este paso se agrupan algunas etiquetas asociadas a reconocimiento o escaneo.

El reconocimiento puede ser una fase temprana del ataque, donde un atacante intenta descubrir hosts, puertos, servicios o posibles vulnerabilidades.

### Preguntas

36. ¿Qué etiquetas se agruparon como reconocimiento?  
37. ¿Cuál de estas etiquetas aparece con mayor frecuencia?  
38. ¿Por qué el reconocimiento es relevante aunque todavía no exista robo de información?

---

## Paso 14 — Calcular total de eventos de reconocimiento

### Código

```python
recon_total = data[data["label"].isin(recon_labels)].shape[0]

recon_total
```

### Explicación

Este paso calcula cuántos eventos del dataset están asociados a reconocimiento.

### Pregunta

39. ¿Cuántos eventos de reconocimiento hay en total?

---

## Paso 15 — Calcular porcentaje de reconocimiento

### Código

```python
(recon_total / len(data)) * 100
```

### Explicación

Este paso calcula qué porcentaje del dataset corresponde a eventos de reconocimiento.

### Preguntas

40. ¿Qué porcentaje del dataset corresponde a eventos de reconocimiento?  
41. ¿Ese porcentaje le parece bajo, medio o alto? Justifique.

---

## Paso 16 — Crear tabla resumen de reconocimiento

### Código

```python
resumen_recon = data[data["label"].isin(recon_labels)]["label"].value_counts().reset_index()

resumen_recon.columns = ["tipo_ataque", "cantidad"]

resumen_recon["porcentaje_dataset"] = (resumen_recon["cantidad"] / len(data)) * 100

resumen_recon
```

### Explicación

Este paso crea una tabla resumen con:

- tipo de ataque;
- cantidad de eventos;
- porcentaje dentro del dataset.

### Preguntas

42. ¿Cuál es el evento de reconocimiento más frecuente?  
43. ¿Cuál es el evento de reconocimiento menos frecuente?  
44. ¿Qué conclusión puede obtener a partir de esta tabla?

---

## Paso 17 — Crear gráfica de eventos de reconocimiento

### Código

```python
resumen_recon.plot(
    x="tipo_ataque",
    y="cantidad",
    kind="bar",
    legend=False,
    title="Eventos de reconocimiento por tipo de ataque"
)
```

### Explicación

Este paso genera una gráfica de barras para visualizar los eventos de reconocimiento por tipo de ataque.

### Preguntas

45. ¿Qué muestra la gráfica?  
46. ¿Qué dos tipos de reconocimiento parecen más relevantes?  
47. ¿Cómo explicaría esta gráfica a un equipo SOC?

---

## Paso 18 — Conclusión del laboratorio

Al final del notebook, crear una celda de texto y redactar una conclusión propia.

La conclusión debe incluir:

- descripción breve del dataset;
- tamaño del dataset;
- protocolos principales;
- servicios relevantes;
- distribución entre tráfico normal y ataques;
- hallazgos sobre eventos de reconocimiento;
- recomendación inicial para un equipo de seguridad.

No se trata de copiar números únicamente.

Se espera una interpretación desde el punto de vista de ciberseguridad.

---

# 6. Entregable del estudiante

El estudiante debe entregar:

1. Notebook ejecutado en Google Colab. - Enlace al notebook de Google Colab con permisos de lectura.
2. Reporte corto de máximo dos páginas.

El notebook debe estar ejecutado completamente y debe incluir una conclusión escrita al final.

---

# 7. Preguntas resumen para el reporte

## A. Comprensión del dataset

1. ¿Qué dataset se utilizó en el laboratorio?
2. ¿Qué representa una fila del dataset?
3. ¿Cuántos registros y columnas tiene el dataset?
4. ¿Qué columnas considera más relevantes para un análisis inicial de ciberseguridad?

## B. Protocolos y servicios

5. ¿Cuál es el protocolo más frecuente?
6. ¿Qué servicios aparecen con mayor frecuencia?
7. ¿Qué servicios considera más sensibles o interesantes desde seguridad?
8. ¿Qué significa el servicio `private` y por qué no debe considerarse automáticamente malicioso?

## C. Tráfico normal y ataques

9. ¿Cuántos eventos normales y cuántos eventos de ataque existen?
10. ¿Qué porcentaje corresponde a tráfico normal?
11. ¿Qué porcentaje corresponde a ataques?
12. ¿Por qué este balance puede ser diferente al de un entorno real de SOC?

## D. Análisis de etiquetas

13. ¿Cuál es el ataque más frecuente?
14. ¿Qué ataques se relacionan con reconocimiento o escaneo?
15. ¿Por qué el ataque más frecuente no necesariamente es el más crítico?

## E. Análisis de bytes enviados

16. ¿Qué diferencias observó en `src_bytes` entre tráfico normal y ataques?
17. ¿Por qué no basta con revisar solo el promedio?
18. ¿Qué eventos aparecen con mayor cantidad de bytes enviados?
19. ¿Un valor alto de bytes enviados implica automáticamente exfiltración? Explique.

## F. Reconocimiento

20. ¿Cuántos eventos de reconocimiento se identificaron?
21. ¿Qué porcentaje del dataset representan?
22. ¿Cuáles fueron los tipos de reconocimiento más frecuentes?
23. ¿Por qué el reconocimiento es una fase importante dentro de un ataque?

## G. Interpretación de seguridad

24. Mencione tres hallazgos relevantes del laboratorio.
25. ¿Qué hallazgo explicaría primero a un equipo SOC?
26. ¿Qué recomendación inicial haría a partir del análisis?
27. ¿Qué dato adicional le gustaría tener para mejorar la investigación?

---

# 8. Formato sugerido del reporte

El reporte puede tener esta estructura:

```text
Título:
Exploración inicial del dataset NSL-KDD

1. Descripción del dataset
2. Tamaño del dataset
3. Protocolos y servicios principales
4. Distribución entre tráfico normal y ataques
5. Análisis de ataques de reconocimiento
6. Hallazgos relevantes
7. Recomendación para el equipo de seguridad
```

---

# 9. Criterios de evaluación

| Criterio | Peso |
|---|---:|
| Ejecución correcta del notebook | 20% |
| Comprensión de la estructura del dataset | 20% |
| Identificación de protocolos, servicios y etiquetas | 20% |
| Interpretación de eventos de reconocimiento | 20% |
| Claridad del reporte final | 20% |

---

# 10. Resultado esperado

Al finalizar este laboratorio, el estudiante debe poder explicar por qué antes de aplicar inteligencia artificial es necesario entender los datos.

El resultado esperado no es un código perfecto.

El resultado esperado es una interpretación razonable de los datos desde el punto de vista de ciberseguridad.




