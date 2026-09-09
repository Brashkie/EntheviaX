# EntheviaX

### High-Performance Scientific Computing for JavaScript & TypeScript

**EntheviaX** es un ecosistema de **computación científica y de alto rendimiento** para JavaScript y TypeScript, diseñado para combinar una API moderna con backends nativos, computación paralela y aceleración mediante CPU, SIMD, WebAssembly y GPU.

El proyecto nació originalmente como **QuantixJS**, enfocado principalmente en proporcionar herramientas científicas dentro del ecosistema JavaScript/TypeScript.

Con el tiempo, la visión evolucionó.

QuantixJS pasó de ser una librería científica orientada principalmente a JS/TS a convertirse en una arquitectura **multi-language y multi-backend**, donde cada tecnología se utiliza según sus fortalezas.

Por esta razón, el proyecto adopta un nuevo nombre:

> **QuantixJS → EntheviaX**

---

# 🔄 From QuantixJS to EntheviaX

El cambio de **QuantixJS** a **EntheviaX** no es solamente un cambio de nombre.

Representa una evolución en la arquitectura, objetivos y alcance del proyecto.

### QuantixJS

La visión inicial estaba centrada en:

* JavaScript.
* TypeScript.
* Computación numérica.
* DataFrames.
* Matemáticas simbólicas.
* Visualización.
* Procesamiento paralelo.
* WebAssembly.
* JIT.

El problema era que esta arquitectura podía terminar dependiendo demasiado del ecosistema JS para tareas donde otros lenguajes ofrecen mejores herramientas y rendimiento.

### EntheviaX

La nueva visión separa la **API** de los **motores de ejecución**.

```text
                     EntheviaX
                         │
                  TypeScript API
                         │
                 EntheviaX Runtime
                         │
        ┌────────────────┼────────────────┐
        │                │                │
      Native          Portable           GPU
        │                │                │
   ┌────┼────┐          WASM            WebGPU
   │    │    │
 Rust  Zig  Fortran
   │    │    │
   └────┼────┘
        │
    Assembly
        │
        ▼
     CPU / SIMD
```

Esto permite que EntheviaX no dependa de un solo lenguaje para resolver todos los problemas.

---

# 🧠 Why Multiple Languages?

EntheviaX sigue una filosofía:

> **Use the right language for the right problem.**

Utilizar varios lenguajes no es un objetivo en sí mismo.

Cada lenguaje tiene una responsabilidad concreta dentro del ecosistema.

---

## 🟦 TypeScript — Public API

TypeScript será la principal interfaz para los desarrolladores de JavaScript.

Se utilizará para:

* API pública.
* Tipos.
* Interfaces.
* Integración con Node.js.
* Integración con aplicaciones web.
* Developer experience.
* Tooling e IntelliSense.

La idea es que el usuario pueda trabajar con EntheviaX sin tener que conocer Rust, Zig, Fortran o Assembly.

```ts
import { entheviax } from "entheviax";

const A = entheviax.array([
  [1, 2],
  [3, 4],
]);

const B = entheviax.array([
  [5, 6],
  [7, 8],
]);

const C = entheviax.linalg.matmul(A, B);

console.log(C);
```

---

# 🦀 Rust — Runtime & Core

Rust será una de las piezas centrales de EntheviaX.

Se utilizará principalmente para:

* Runtime.
* Gestión de memoria.
* Concurrencia.
* Paralelismo.
* Scheduling.
* FFI.
* Integración con Node.js.
* Orquestación de backends.
* Componentes críticos del núcleo.

Rust ofrece una combinación importante de:

* Rendimiento nativo.
* Seguridad de memoria.
* Concurrencia segura.
* Control de recursos.
* Excelente interoperabilidad con otros lenguajes.

Por ello, Rust será principalmente el **runtime y núcleo de ejecución**.

---

# ⚡ Zig — Native Kernels & Low-Level Computing

Zig tendrá un papel especialmente importante en los componentes de bajo nivel.

Se utilizará para:

* Native kernels.
* SIMD.
* Operaciones numéricas críticas.
* FFI.
* Componentes con control explícito de memoria.
* Integración con C.
* Cross-compilation.
* Código portable de bajo nivel.

Zig permite construir componentes pequeños y especializados sin introducir una capa innecesaria de abstracción.

La intención no es reemplazar Rust, sino utilizar ambos donde sean más adecuados.

```text
Rust
 │
 ├── Runtime
 ├── Memory
 ├── Concurrency
 └── Orchestration

Zig
 │
 ├── Kernels
 ├── SIMD
 ├── FFI
 └── Low-level components
```

---

# 🧮 Fortran — Scientific Algorithms

Fortran tendrá un propósito mucho más específico.

No será utilizado para construir toda la plataforma.

Se utilizará cuando sea ventajoso aprovechar:

* Algoritmos numéricos científicos.
* Álgebra numérica.
* Métodos matemáticos especializados.
* Algoritmos científicos maduros.
* Computación científica de alto rendimiento.

Fortran posee décadas de desarrollo en computación científica y continúa siendo relevante para determinadas cargas numéricas.

EntheviaX podrá integrar algoritmos Fortran dentro de sus backends nativos mediante FFI.

```text
EntheviaX
    │
    ▼
Rust Runtime
    │
    ▼
Native Backend
    │
    └── Fortran Scientific Kernels
```

---

# 🔩 Assembly — Critical Optimizations

Assembly será utilizado de forma extremadamente selectiva.

No se pretende escribir EntheviaX entero en Assembly.

Su propósito será optimizar determinados kernels donde el control a nivel de instrucciones pueda proporcionar una ventaja real.

Posibles usos:

* SIMD especializado.
* Kernels matemáticos críticos.
* Operaciones específicas de arquitectura.
* Micro-optimizaciones.
* Hot paths extremadamente sensibles al rendimiento.

La regla será:

> **Benchmark first, Assembly second.**

Si Rust o Zig producen el rendimiento necesario, no habrá razón para utilizar Assembly.

---

# 🌐 WebAssembly — Portability

WebAssembly no reemplaza al backend nativo.

Su función principal será proporcionar un **backend portable**.

```text
EntheviaX
    │
    ├── Native
    │     ├── Rust
    │     ├── Zig
    │     ├── Fortran
    │     └── Assembly
    │
    └── WebAssembly
          ├── WASM
          └── WASM SIMD
```

WASM permitirá ejecutar determinados componentes científicos en:

* Navegadores.
* Web Workers.
* Aplicaciones web.
* Entornos JavaScript compatibles.

También permitirá reutilizar kernels desarrollados en Rust o Zig en entornos donde el código nativo tradicional no sea una opción.

**Native será prioritario para máximo rendimiento en entornos donde esté disponible.**

**WASM será prioritario cuando la portabilidad sea más importante.**

---

# 🎮 WebGPU — GPU Computing

WebGPU será el backend destinado a workloads que puedan beneficiarse de una GPU.

Especialmente:

* Operaciones matriciales.
* Procesamiento masivamente paralelo.
* Simulaciones.
* Procesamiento de grandes volúmenes de datos.
* Kernels científicos paralelizables.
* Computación en navegador.

La intención es que EntheviaX pueda seleccionar diferentes backends dependiendo del workload.

```text
                    Workload
                       │
                       ▼
                EntheviaX Runtime
                       │
             ┌─────────┼─────────┐
             ▼         ▼         ▼
           Native     WASM     WebGPU
             │         │         │
           CPU       Portable    GPU
           SIMD
```

---

# 🚀 Core Features

## Numerical Computing

* NDArray.
* Multidimensional arrays.
* Vectorized operations.
* Broadcasting.
* Linear algebra.
* Statistical functions.
* Advanced mathematical functions.
* Numerical solvers.
* SIMD acceleration.

## Data Computing

* High-performance DataFrames.
* Columnar processing.
* Filtering.
* Grouping.
* Aggregations.
* Joins.
* Lazy execution.
* CSV.
* JSON.
* Parquet.

## Symbolic Mathematics

* Symbolic variables.
* Symbolic expressions.
* Differentiation.
* Integration.
* Algebraic simplification.
* Expression manipulation.
* Numerical evaluation.

## Optimization

* Mathematical optimization.
* Minimization.
* Maximization.
* Iterative methods.
* Numerical solvers.
* Constraint optimization.

## Scientific Visualization

* Line plots.
* Bar charts.
* Scatter plots.
* Histograms.
* Function visualization.
* Scientific data visualization.
* Canvas.
* WebGL.
* WebGPU.

## Parallel Computing

* Worker Threads.
* Multithreading.
* Parallel kernels.
* Lazy execution.
* Task-based processing.
* Parallel pipelines.
* Distributed computing.

---

# 📦 Ecosystem

EntheviaX será modular.

### Core

* `entheviax-core` — Core runtime and numerical foundations.
* `entheviax-native` — Native backend integration.

### Numerical & Scientific

* `entheviax-linear` — Linear algebra.
* `entheviax-symbolic` — Symbolic mathematics.
* `entheviax-opt` — Mathematical optimization.

### Data

* `entheviax-data` — DataFrames and scientific data processing.

### Visualization

* `entheviax-plot` — Scientific visualization.

### Parallel & Distributed

* `entheviax-parallel` — Parallel computing.
* `entheviax-distributed` — Distributed computing.

### Acceleration

* `entheviax-wasm` — WebAssembly backend.
* `entheviax-webgpu` — GPU backend.
* `entheviax-jit` — JIT compilation and runtime optimization.

### Advanced

* `entheviax-quantum` — Quantum computing abstractions and experimentation.

---

# 🏗️ Architecture

```text
                         EntheviaX
                             │
                    ┌────────┴────────┐
                    │ TypeScript API  │
                    └────────┬────────┘
                             │
                    EntheviaX Runtime
                             │
              ┌──────────────┼──────────────┐
              │              │              │
           Native         Portable          GPU
              │              │              │
       ┌──────┼──────┐      WASM          WebGPU
       │      │      │
      Rust   Zig   Fortran
       │      │      │
       └──────┼──────┘
              │
          Assembly
              │
              ▼
          CPU / SIMD
```

El runtime podrá seleccionar el backend apropiado dependiendo de:

* Entorno.
* Hardware disponible.
* Tipo de operación.
* Tamaño del workload.
* Necesidad de portabilidad.
* Requisitos de rendimiento.

---

# 🗺️ Roadmap

## Phase 0 — Foundation

* [ ] EntheviaX Core.
* [ ] Project architecture.
* [ ] NDArray.
* [ ] Basic numerical operations.
* [ ] TypeScript API.
* [ ] Native runtime foundation.
* [ ] Benchmark infrastructure.

## Phase 1 — Numerical Engine

* [ ] Advanced vectorization.
* [ ] Linear algebra.
* [ ] Statistical functions.
* [ ] SIMD kernels.
* [ ] Native CPU backend.
* [ ] Optimized memory management.

## Phase 2 — Data Engine

* [ ] DataFrame engine.
* [ ] Columnar processing.
* [ ] CSV.
* [ ] JSON.
* [ ] Parquet.
* [ ] Lazy execution.

## Phase 3 — Symbolic Engine

* [ ] Symbolic expressions.
* [ ] Differentiation.
* [ ] Integration.
* [ ] Algebraic simplification.
* [ ] Expression evaluation.

## Phase 4 — Native Acceleration

* [ ] Rust runtime.
* [ ] Zig kernels.
* [ ] SIMD.
* [ ] Native FFI.
* [ ] Specialized numerical kernels.
* [ ] Fortran integration.

## Phase 5 — WebAssembly

* [ ] WASM backend.
* [ ] WASM SIMD.
* [ ] Rust → WASM.
* [ ] Zig → WASM.
* [ ] Web Worker execution.
* [ ] Portable numerical kernels.

## Phase 6 — GPU & JIT

* [ ] WebGPU backend.
* [ ] GPU kernels.
* [ ] GPU data processing.
* [ ] JIT compiler.
* [ ] Runtime kernel optimization.
* [ ] Automatic backend selection.

## Phase 7 — Parallel & Distributed

* [ ] Multithreaded runtime.
* [ ] Worker-based parallelism.
* [ ] Parallel DataFrames.
* [ ] Distributed computation.
* [ ] Distributed DataFrames.
* [ ] Task scheduler.

## Phase 8 — Advanced Scientific Computing

* [ ] Advanced mathematical models.
* [ ] Scientific simulations.
* [ ] Specialized numerical solvers.
* [ ] High-performance algorithms.
* [ ] Quantum computing abstractions.
* [ ] Hardware-specific optimizations.

---

# 🎯 Target Audience

EntheviaX está pensado para:

* Data scientists.
* Engineers.
* Researchers.
* Students and educators.
* Scientific software developers.
* AI and machine learning developers.
* Simulation developers.
* Numerical computing applications.
* High-performance computing workloads.
* Scientific data processing.

---

# 📊 Performance Philosophy

EntheviaX prioriza:

1. **Correctness**
2. **Memory efficiency**
3. **Native performance**
4. **Parallel execution**
5. **Hardware acceleration**
6. **Portability**
7. **Developer experience**

El proyecto no busca hacer que absolutamente todo sea nativo.

Busca utilizar **el backend más adecuado para cada workload**.

```text
                         Workload
                            │
                            ▼
                     EntheviaX Runtime
                            │
              ┌─────────────┼─────────────┐
              ▼             ▼             ▼
           Native          WASM        WebGPU
              │             │             │
          CPU / SIMD     Portable          GPU
              │             │             │
              └─────────────┼─────────────┘
                            ▼
                         Result
```

---

# 🔬 Project Vision

EntheviaX busca convertirse en una plataforma científica moderna para el ecosistema JavaScript/TypeScript.

La meta no es simplemente crear otra librería matemática.

La meta es construir una infraestructura donde:

* JavaScript/TypeScript proporcione la experiencia del desarrollador.
* Rust proporcione el runtime.
* Zig proporcione kernels y componentes low-level.
* Fortran aporte algoritmos científicos especializados.
* Assembly optimice los puntos realmente críticos.
* WebAssembly proporcione portabilidad.
* WebGPU proporcione aceleración GPU.
* JIT permita optimización dinámica.
* La computación paralela permita aprovechar hardware moderno.

Todo ello bajo una única API y un único ecosistema.

> **EntheviaX — Scientific computing without choosing a single language.**

---

# 📄 License

Apache-2.0 License
