# 📉 Predicción de Recesión en Perú (2000–2024)

## 1. Introducción
Este proyecto presenta una aplicación de **modelos de elección binaria** para predecir la ocurrencia de **recesiones en el Perú** durante el período **2000–2024**.

El análisis se enfoca en la construcción de un **modelo de clasificación binaria**, donde la variable dependiente indica la presencia o no de una recesión:


Para este propósito, se emplean **indicadores macroeconómicos clave** como variables explicativas:

- Inflación (% anual)
- Crecimiento del Producto Bruto Interno (PBI, % anual)
- Tasa de desempleo (% de la población económicamente activa)

El modelo utilizado es una **Red Neuronal Artificial (RNA)** con función de activación **sigmoide**, ampliamente empleada en problemas de clasificación binaria. Este enfoque permite capturar **relaciones no lineales** entre los indicadores macroeconómicos y la probabilidad de ocurrencia de una recesión.

---

## 2. Carga y Preparación de los Datos
Los datos corresponden a indicadores macroeconómicos reales del Perú para el período **2000–2024** e incluyen las siguientes variables:

- **AÑO**: Año de observación  
- **INFLACION**: Inflación anual (%)  
- **PBI**: Crecimiento del PBI anual (%)  
- **DESEMPLEO**: Tasa de desempleo (%)  
- **RECESION**: Variable binaria que indica la ocurrencia de una recesión  

📌 Las recesiones son identificadas en los años **2020** y **2023**.

Los datos se almacenan en un **DataFrame de pandas**. Previo al entrenamiento del modelo, las variables explicativas son **escaladas mediante StandardScaler**, y luego se dividen en conjuntos de **entrenamiento y prueba**.

---

## 3. Construcción del Modelo
El modelo se implementa utilizando una **red neuronal secuencial de Keras**, con la siguiente arquitectura:

### 🧠 Arquitectura de la Red
- Capa oculta:
  - 8 neuronas
  - Función de activación **ReLU**
- Capa de salida:
  - 1 neurona
  - Función de activación **sigmoide**

### ⚙️ Configuración
- Función de pérdida: `binary_crossentropy`  
- Optimizador: `Adam`  
- Número de épocas: **150**

La salida del modelo representa la **probabilidad de que ocurra una recesión** en un año determinado.

---

## 4. Evaluación del Modelo
El desempeño del modelo se evalúa utilizando el conjunto de prueba, generando un **reporte de clasificación** que incluye las siguientes métricas:

- **Precision**: proporción de predicciones positivas correctas  
- **Recall**: proporción de casos positivos reales correctamente identificados  
- **F1-score**: media armónica entre precisión y recall  

### 📊 Resultados de la Evaluación

| Clase | Precision | Recall | F1-score | Support |
|------|-----------|--------|----------|---------|
| 0 (No recesión) | 0.88 | 1.00 | 0.93 | 7 |
| 1 (Recesión) | 0.00 | 0.00 | 0.00 | 1 |
| **Accuracy** |  |  | **0.88** | 8 |
| **Macro avg** | 0.44 | 0.50 | 0.47 | 8 |
| **Weighted avg** | 0.77 | 0.88 | 0.82 | 8 |

---

## 5. Interpretación de Resultados
El modelo muestra un **buen desempeño al clasificar los años sin recesión** (clase 0), alcanzando valores altos de precisión y recall para esta categoría.

Sin embargo, el modelo **no logra identificar correctamente los años con recesión** (clase 1), obteniendo valores de **precision y recall iguales a 0.00**. 

Este resultado se explica principalmente por el **desequilibrio en la base de datos**:

- Años sin recesión: **23**
- Años con recesión: **2**

La fuerte desproporción entre clases limita la capacidad del modelo para aprender adecuadamente los patrones asociados a la ocurrencia de recesiones.

---

## 6. Conclusión
Este ejercicio muestra que las redes neuronales pueden ser útiles para modelar la probabilidad de recesión a partir de indicadores macroeconómicos. No obstante, en contextos con **datos altamente desbalanceados**, el desempeño para la clase minoritaria se ve seriamente afectado.

Para mejorar los resultados, sería recomendable explorar técnicas como:
- Rebalanceo de clases (SMOTE, undersampling)
- Ajuste de pesos de clase
- Modelos alternativos (Logit / Probit)
- Evaluación con métricas enfocadas en la clase minoritaria

---



