# QuantixJS

### Scientific Computing for JavaScript & TypeScript

QuantixJS es una librería completa de **computación científica**,
diseñada para ofrecer capacidades avanzadas de cálculo numérico,
análisis de datos, matemáticas simbólicas, visualización y procesamiento
paralelo, totalmente en **JavaScript y TypeScript**.

Su misión es proporcionar una alternativa moderna, rápida y accesible
dentro del ecosistema JS/TS para aplicaciones científicas, analíticas y
de ingeniería.

------------------------------------------------------------------------

## 🚀 Características principales

### 🔢 Cómputo Numérico

-   Arreglos multidimensionales (NDArray)
-   Operaciones vectorizadas
-   Álgebra lineal optimizada
-   Funciones estadísticas y matemáticas avanzadas

### 📊 DataFrames

-   Estructuras tabulares de alto rendimiento
-   Filtros, agrupaciones, joins, transforms
-   Lectura de CSV, JSON y Parquet

### 🧮 Matemáticas Simbólicas

-   Variables simbólicas
-   Derivación e integración
-   Simplificación y manipulación algebraica

### 📈 Visualización Moderna

-   Gráficos de líneas, barras, dispersión, histogramas
-   Estilos preconfigurados
-   Render basado en Canvas o WebGL

### 🧵 Procesamiento Paralelo

-   Workers y clusters
-   Ejecución distribuida
-   Evaluación perezosa

### ⚡ Aceleración

-   Núcleo optimizable con WebAssembly
-   Optimización automática de kernels numéricos
-   Integración opcional con GPU

### 🟦 Soporte Total para TypeScript

-   Tipos completos
-   IntelliSense avanzado
-   API clara y segura

------------------------------------------------------------------------

## 📦 Instalación

    npm install quantixjs

------------------------------------------------------------------------

## 🧪 Ejemplo rápido

``` ts
import { qx } from "quantixjs";

// Matrices
const A = qx.array([[1, 2], [3, 4]]);
const B = qx.array([[5, 6], [7, 8]]);

console.log(qx.dot(A, B));
```

------------------------------------------------------------------------

## 🧩 Módulos principales

-   **quantix-core** --- núcleo matemático y numérico\
-   **quantix-data** --- DataFrames y herramientas de datos\
-   **quantix-symbolic** --- motor simbólico\
-   **quantix-opt** --- optimización matemática\
-   **quantix-plot** --- sistema de gráficos\
-   **quantix-distributed** --- computación paralela/distribuida\
-   **quantix-jit** --- aceleración con compilación dinámica

------------------------------------------------------------------------

## 🗺️ Roadmap

-   [ ] Motor numérico basado en WebAssembly\
-   [ ] Sistema simbólico completo\
-   [ ] Backend gráfico con WebGPU\
-   [ ] DataFrames distribuidos\
-   [ ] Compilador JIT automático\
-   [ ] Modelos matemáticos avanzados

------------------------------------------------------------------------

## 🧑‍💻 Público objetivo

-   Científicos de datos\
-   Ingenieros\
-   Estudiantes y docentes\
-   Investigadores\
-   Desarrolladores que trabajan con simulaciones, análisis o IA clásica

------------------------------------------------------------------------

## 📄 Licencia

Apache-2.0 License
