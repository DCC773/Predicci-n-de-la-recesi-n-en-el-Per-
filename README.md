# 📉 Predicción de Recesión en Perú (2000–2024)

## 1. Introducción
Este proyecto presenta una aplicación de **modelos de elección binaria** para predecir la ocurrencia de **recesiones en el Perú** durante el período **2000–2024**.

El análisis se centra en la construcción de un **modelo de clasificación binaria**, donde la variable dependiente indica la presencia o no de una recesión:


Para este propósito, se utilizan los siguientes **indicadores macroeconómicos** como variables explicativas:

- Inflación (% anual)
- Crecimiento del Producto Bruto Interno (PBI, % anual)
- Tasa de desempleo (% de la población económicamente activa)

El modelo implementado es una **Red Neuronal Artificial (RNA)** con función de activación **sigmoide**, adecuada para problemas de clasificación binaria y capaz de capturar relaciones no lineales entre las variables.

---

## 2. Carga y Preparación de los Datos
Los datos corresponden a indicadores macroeconómicos reales del Perú para el período **2000–2024** y contienen las siguientes variables:

- **AÑO**: Año de observación  
- **INFLACION**: Inflación anual (%)  
- **PBI**: Crecimiento del PBI anual (%)  
- **DESEMPLEO**: Tasa de desempleo (%)  
- **RECESION**: Variable binaria que indica la ocurrencia de una recesión  

Las recesiones se identifican específicamente en los años **2020** y **2023**.

Los datos se almacenan en un **DataFrame de pandas**. Antes del entrenamiento del modelo, las variables predictoras se **escalan mediante StandardScaler** y luego se dividen en conjuntos de **entrenamiento y prueba**.

---

## 3. Construcción del Modelo
El modelo se construye utilizando una **red neuronal secuencial de Keras** con la siguiente configuración:

### 🧠 Arquitectura
- Una capa oculta con **8 neuronas** y función de activación **ReLU**  
- Una capa de salida con **1 neurona** y función de activación **sigmoide**

### ⚙️ Parámetros de entrenamiento
- Función de pérdida: `binary_crossentropy`  
- Optimizador: `Adam`  
- Número de épocas: **150**

La salida del modelo representa la **probabilidad de que ocurra una recesión** en un año determinado.

---

## 4. Evaluación del Modelo
El desempeño del modelo se evalúa utilizando el conjunto de prueba mediante un **reporte de clasificación**, el cual incluye las métricas de precisión, recall y F1-score.

### 📊 Resultados de la evaluación
- **Clase 0 (No recesión)**  
  - Precision: 0.88  
  - Recall: 1.00  
  - F1-score: 0.93  

- **Clase 1 (Recesión)**  
  - Precision: 0.00  
  - Recall: 0.00  
  - F1-score: 0.00  

- **Accuracy total**: 0.88  

Los resultados muestran que el modelo clasifica correctamente la mayoría de los años sin recesión, pero no logra identificar los años con recesión.

---

## 5. Interpretación de Resultados
El modelo presenta un **buen desempeño para la clase mayoritaria** (años sin recesión), con valores elevados de precisión y recall.

Sin embargo, el desempeño para la **clase minoritaria** (años con recesión) es deficiente. Esto se debe principalmente al **desequilibrio en la base de datos**:

- Años sin recesión: **23**
- Años con recesión: **2**

Este desbalance limita la capacidad de la red neuronal para aprender los patrones asociados a la ocurrencia de recesiones.

---

## 6. Conclusión
El análisis muestra que las redes neuronales pueden utilizarse para modelar la probabilidad de recesión a partir de indicadores macroeconómicos. No obstante, en presencia de **datos altamente desbalanceados**, el modelo tiende a favorecer la clase mayoritaria.

Para mejorar el desempeño, se recomienda explorar:
- Técnicas de rebalanceo de datos (SMOTE, undersampling)
- Ajuste de pesos de clase
- Modelos alternativos como **Logit y Probit**
- Métricas enfocadas en la clase minoritaria

---

