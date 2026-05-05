# 🏥 Inteligencia Artificial Explicativa (XAI) en Salud

Este repositorio contiene el desarrollo práctico de dos modelos predictivos de Machine Learning aplicados al sector sanitario. El objetivo principal no es solo lograr predicciones precisas, sino aplicar técnicas de **Inteligencia Artificial Explicativa (XAI)** utilizando las librerías **SHAP** y **LIME** para entender cómo y por qué los modelos toman sus decisiones médicas.

## 📂 Estructura del Proyecto

* `datos_costes.csv` y `datos_corazon.csv`: Contienen los datasets originales utilizados para entrenar a los modelos (fuente: Kaggle).
* `datos_costes.ipynb` y `datos_corazon.ipynb`: Contienen los cuadernos de Python (Jupyter/Colab) con el preprocesamiento, entrenamiento algorítmico, evaluación de métricas y análisis XAI.
* `README.md`: Explicación del enfoque y conclusiones del proyecto.


## 🔬 Caso de Uso 1: Modelo de Clasificación (Enfermedad Cardíaca)

**Objetivo:** Predecir si un paciente presenta una enfermedad cardíaca basándose en métricas clínicas y diagnósticas avanzadas.  
**Dataset:** *Heart Disease Dataset* (Kaggle). Contiene 14 variables clínicas reales de pacientes, incluyendo tipo de dolor de pecho, nivel de colesterol, electrocardiogramas en reposo y frecuencia cardíaca máxima.  
**Enfoque:** Tras iteraciones iniciales con otros conjuntos de datos clínicos que presentaban ruido excesivo, se optó por un enfoque *Data-Centric*. Se implementó un modelo `RandomForestClassifier` sobre este dataset enriquecido, logrando un **Accuracy y F1-Score superiores al 98%**. Se utilizó **SHAP** para explicabilidad global y **LIME** para auditorías locales de pacientes individuales.

### Resultados y Explicabilidad (XAI)
El uso combinado de herramientas XAI nos permite auditar el modelo a dos niveles:

* **Visión Global (SHAP):** El modelo determina que variables como el tipo de dolor de pecho (`cp`) y la frecuencia cardíaca máxima alcanzada (`thalach`) son los factores demográficos más críticos para detectar la enfermedad, alineando el razonamiento matemático con el consenso cardiológico.

* <img width="383" height="281" alt="image" src="https://github.com/user-attachments/assets/1b299c7a-835f-4679-9eaf-a2b264e686e7" />

* **Auditoría Local (LIME):** Permite aislar predicciones específicas (incluyendo *Falsos Negativos*). Por ejemplo, LIME nos muestra cómo la IA puede fallar al diagnosticar a un paciente enfermo si este presenta "síntomas atípicos", emulando las dudas clínicas que tendría un médico humano.

  <img width="707" height="161" alt="image" src="https://github.com/user-attachments/assets/70d6ba89-d295-4c35-a007-c00962be41e4" />


---

## 💸 Caso de Uso 2: Modelo de Regresión (Costes Médicos)

**Objetivo:** Predecir el coste exacto anual de la factura médica de una persona basándonos en sus características físicas y estilo de vida.  
**Dataset:** *Medical Cost Personal Dataset* (Kaggle). Incluye edad, sexo, IMC, cantidad de hijos, región y estado de fumador.  
**Enfoque:** Se implementó un modelo **`RandomForestRegressor`** capaz de predecir valores continuos. El modelo demostró un alto rendimiento con un **R² superior a 0.86**, logrando un Error Absoluto Medio (MAE) altamente competitivo dada la falta de dimensionalidad médica oculta (días de ingreso, tipo de cirugía, etc.). Posteriormente, se aplicó **SHAP** para cuantificar el impacto económico de cada variable.

### Resultados y Explicabilidad (XAI)
El análisis de impacto de SHAP nos muestra cómo cada factor empuja el precio de la factura hacia arriba o hacia abajo:

<img width="495" height="267" alt="image" src="https://github.com/user-attachments/assets/9b96c7e0-9b7e-46d5-8e70-72a2ff978f28" />


* **Conclusiones:** La explicabilidad revela de forma contundente que **ser fumador** es la variable que más encarece los costes médicos, desplazando la predicción económica drásticamente hacia valores altos. La edad avanzada y un IMC elevado (obesidad) son los siguientes factores que más peso económico añaden a la predicción y a las primas de los seguros.

---

## 🛠️ Tecnologías Utilizadas
* **Lenguaje:** Python
* **Librerías de Modelado:** `scikit-learn` (Random Forest)
* **Librerías XAI:** `shap`, `lime`
* **Manipulación de Datos:** `pandas`, `numpy`
