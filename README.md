
# Proyecto de Visión por Computador con Deep Learning

## Autor: Rubén Ocaña Mena

Este repositorio contiene un flujo de trabajo completo para el tratamiento de un dataset de imágenes de flores (margaritas y dientes de león), desde el análisis exploratorio de datos hasta la generación de nuevas imágenes realistas.  

## Estructura del Proyecto

.
├── data/
│ ├── train/
│ │ ├── daisy/
│ │ └── dandelion/
│ ├── valid/
│ │ ├── daisy/
│ │ └── dandelion/
│ └── test/
│ ├── daisy/
│ └── dandelion/
├── modelos/
│ ├── 01_EDA.ipynb
│ ├── 02_ML_classifier.ipynb
│ ├── 03_Deep_Learning.ipynb
├── outputs/
└── README.md


## 1. Análisis Exploratorio de Datos (EDA)

En esta fase inicial se evalúan las características del dataset para orientar las siguientes técnicas:

- **Tipo y tamaño de imágenes**  
  Inspección de resoluciones, proporciones y formato de los ficheros.

- **Balanceo de clases**  
  Cómputo de número de muestras por categoría (`daisy` vs `dandelion`).

- **Histogramas de color y distribución de píxeles**  
  Análisis de canales RGB para identificar sesgos o necesidades de normalización.

- **Visualización de muestras**  
  Mosaicos de imágenes para comprobar variedad y calidad.

Los resultados del EDA se encuentran en `modelos/01_EDA.ipynb`.

## 2. Machine Learning Clásico

Se realiza una prueba rápida con algoritmos clásicos (SVM, RandomForest, KNN) usando características extraídas con un modelo CNN preentrenado (por ejemplo, vectores de activación de ResNet).  

- Extracción de features:  
  - Carga de imágenes y paso por la red hasta la penúltima capa.  
  - Reducción de dimensión con PCA si es necesario.

- Entrenamiento de clasificador:  
  - Validación cruzada para seleccionar hiperparámetros.  
  - Métricas de accuracy, precisión, recall y F1-score.

El notebook `modelos/02_ML_classifier.ipynb` detalla esta prueba.

## 3. Deep Learning

### 3.1 Clasificación de Imágenes

- **Modelo from scratch**  
  - Arquitectura `SimpleCNN` con capas convolucionales, ReLU, pooling y fully–connected.  
  - Entrenamiento con `CrossEntropyLoss` y `Adam`.

- **Transfer Learning**  
  - Uso de `ResNet18` preentrenada, congelando capas iniciales y adaptando la capa final.  

- **Curvas de entrenamiento**  
  - Gráficas de accuracy y loss para entrenamiento vs validación.  
  - Early stopping y weight decay para controlar overfitting.

- **Evaluación**  
  - Accuracy final en `test/`.  
  - Matriz de confusión y clasificación por clase.

Código principal y análisis en `modelos/03_Deep_Learning.ipynb`.

### 3.2 Detección de Objetos

- **Modelo preentrenado**  
  - `Faster R-CNN` con backbone `ResNet50-FPN` de `torchvision`.  

- **Inferencia**  
  - Recorrido de imágenes en `data/test` para localizar cada instancia.  
  - Umbral de confianza configurable.

- **Visualización**  
  - Dibujo de bounding boxes y scores sobre la imagen original.

La implementación y ejemplos están en `modelos/03_Deep_Learning.ipynb`.

### 3.3 Image-to-Image

- **Autoencoder simple**  
  - Codificador y decodificador convolucional que aprende a reconstruir imágenes.  
  - Uso como técnica generativa básica y para reducción de dimensión.

- **Stable Diffusion**  
  - Pipeline de `diffusers` para generar imágenes realistas condicionadas a la clase (`daisy`/`dandelion`).  
  - Ajuste de número de pasos, guidance scale y scheduler.

- **Evaluación**  
  - Comparación visual entre originales y reconstrucciones.  
  - Inspección cualitativa de imágenes generadas por Stable Diffusion.

Todos los ejemplos de generación están en `modelos/03_Deep_Learning.ipynb`.

---

