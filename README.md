# 🏦 Transformación y Limpieza de Datos Bancarios con Pandas

![Python](https://img.shields.io/badge/python-v3.8+-blue.svg)
![Pandas](https://img.shields.io/badge/pandas-v1.3+-green.svg)
![Status](https://img.shields.io/badge/status-completed-success.svg)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

## 📋 Caso de Estudio: Base de Datos de Clientes Bancarios

En este proyecto apliqué técnicas de **limpieza y transformación de datos textuales** utilizando Pandas en un caso real
de una institución bancaria. La base de datos de clientes contenía información desorganizada que requería
estandarización para análisis posteriores y operaciones bancarias eficientes.

## 🎯 Objetivos del Proyecto

> **Transformar una base de datos desordenada en información estructurada y lista para análisis**

### 🔍 Problemática Identificada

La base de datos bancaria presentaba las siguientes inconsistencias:

| Problema                      | Descripción                            | Impacto                              |
|-------------------------------|----------------------------------------|--------------------------------------|
| 📝 **Nombres inconsistentes** | Diferentes capitalizaciones y formatos | Dificultad en búsquedas y duplicados |
| 📞 **Teléfonos sin formato**  | Paréntesis, espacios irregulares       | Problemas de contacto                |
| 🏠 **Direcciones mezcladas**  | Códigos postales dentro de direcciones | Análisis geográfico deficiente       |
| 🎯 **Falta de segmentación**  | Calle y número juntos                  | Dificultad en análisis de ubicación  |

## 🚀 Soluciones Implementadas

### 1. 📝 Estandarización de Nombres de Clientes

```python
df["nombre"] = df["nombre"].str.upper()
```

- **Técnica**: Conversión a mayúsculas con `.str.upper()`
- **Resultado**: Eliminación de duplicados por capitalización
- **Beneficio**: Búsquedas más eficientes y consistentes

### 2. 📞 Normalización de Números Telefónicos

```python
df["telefono"] = df.telefono.str.replace("(", "", regex=False).str.replace(")", "", regex=False)
```

- **Técnica**: Eliminación de caracteres especiales
- **Formato objetivo**: `XX XXXXX-XXXX`
- **Beneficio**: Contacto uniforme y automatizable

### 3. 🗺️ Extracción de Códigos Postales

```python
df["CP"] = df.direccion.str.extract(r"(\d{5}-\d{3})")
```

- **Técnica**: Expresiones regulares `(\d{5}-\d{3})`
- **Resultado**: Columna independiente para CP
- **Beneficio**: Segmentación geográfica precisa

### 4. 🏠 Separación de Direcciones

```python
df[["calle", "numero"]] = df.direccion.str.replace(",", "").str.split(r'\s(?=\d+$)', regex=True, expand=True)
```

- **Técnica**: Regex con lookahead `\s(?=\d+$)`
- **Resultado**: Dos columnas separadas
- **Beneficio**: Análisis detallado de ubicaciones

## 📊 Transformación de Datos

### Antes de la Limpieza:

```
nombre               | direccion                             | telefono
Carlos Mendoza       | Calle 22 de Abril, 12 52614-524       | 11 99548-2578
JavieR Fernández     | Calle Alvarenga Borges, 573 29285-678 | 11 99999-1234
pedro martínez       | Calle Colombo, 789 45678-912          | 11 91234-5678
```

### Después de la Limpieza:

```
nombre           | telefono      | CP        | calle                    | numero
CARLOS MENDOZA   | 11 99548-2578 | 52614-524 | Calle 22 de Abril        | 12
JAVIER FERNÁNDEZ | 11 99999-1234 | 29285-678 | Calle Alvarenga Borges   | 573
PEDRO MARTÍNEZ   | 11 91234-5678 | 45678-912 | Calle Colombo            | 789
```

## 🎯 Impacto y Beneficios

### 💼 Para la Institución Bancaria:

- ✅ **Mejora en la calidad de datos** - Información consistente y confiable
- ✅ **Análisis geográfico eficiente** - Segmentación por códigos postales
- ✅ **Contacto optimizado** - Números telefónicos estandarizados
- ✅ **Reducción de duplicados** - Nombres normalizados

### 📈 Para Análisis Futuro:

- 🎯 Segmentación de clientes por ubicación
- 📊 Estudios demográficos por zona
- 💰 Análisis de rentabilidad por región
- 🔍 Detección de patrones de comportamiento

## 🛠️ Herramientas y Tecnologías

| Tecnología                                                                                      | Propósito              | Versión |
|-------------------------------------------------------------------------------------------------|------------------------|---------|
| ![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)    | Lenguaje principal     | 3.12    |
| ![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)    | Manipulación de datos  | 2.3.1   |
| ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white) | Entorno de desarrollo  | -       |
| ![Regex](https://img.shields.io/badge/Regex-000000?style=flat&logo=regex&logoColor=white)       | Procesamiento de texto | -       |

## 📁 Estructura del Proyecto

```
📂 Pandas-Limpieza-Transformacion-Datos/
├── 📊 banco_clientes.csv              # Dataset original
├── 📈 banco_clientes_procesado.csv    # Dataset limpio
├── 📓 Manipulacion_strings.ipynb      # Notebook con análisis
├── 📋 README.md                       # Documentación
└── 💾 banco_clientes.xlsx            # Archivo Excel original
```

## 🎓 Aprendizajes Clave

| Concepto                | Descripción                      | Aplicación                       |
|-------------------------|----------------------------------|----------------------------------|
| **String Methods**      | Métodos de manipulación de texto | `.str.upper()`, `.str.replace()` |
| **Regex**               | Expresiones regulares            | Extracción de patrones           |
| **Data Cleaning**       | Limpieza de datos                | Estandarización y normalización  |
| **Data Transformation** | Transformación estructural       | División y creación de columnas  |

## 🚀 Cómo Ejecutar

1. **Clonar el repositorio**
2. **Instalar dependencias**: `pip install pandas jupyter`
3. **Ejecutar el notebook**: `jupyter notebook Manipulacion_strings.ipynb`
4. **Revisar resultados**: Archivo `banco_clientes_procesado.csv`

---

<div align="center">

[![LinkedIn](https://img.shields.io/badge/LinkedIn-David_Sandoval-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/devsandoval)
[![GitHub](https://img.shields.io/badge/GitHub-@sandovaldavid-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/sandovaldavid)

Proyecto de Aprendizaje - Curso de Pandas y Limpieza de Datos - Programa ONE Education G8 - Alura

</div>
