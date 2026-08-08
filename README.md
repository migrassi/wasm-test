# Experimento: Rust + WebAssembly (Wasm)

Este repositorio contiene un proyecto experimental para probar la integración y el rendimiento de **WebAssembly (Wasm)** utilizando **Rust**. El desarrollo se realizó por completo en un entorno virtual utilizando **GitHub Codespaces**.

## Resultados de Rendimiento

El experimento consistió en calcular el elemento 40 de la sucesión de Fibonacci (`102334155`) evaluando dos enfoques algorítmicos diferentes y los niveles de optimización del compilador de Rust:

| Algoritmo | Modo de Compilación | Tiempo de Ejecución | Observaciones |
| :--- | :--- | :--- | :--- |
| **Recursivo** | `Debug` | **245.70 ms** | Sobrecarga por información de depuración. |
| **Recursivo** | `Release` | **239.90 ms** | Cuello de botella en la Pila de Llamadas (*Call Stack*) del navegador. |
| **Iterativo** | `Release` | **0.20 ms** | **Optimización máxima (~120,000% más rápido).** Ejecución directa en registros del CPU. |

---

## Tecnologías 

*   **Rust (v1.97.1)**: Para el código que hace el cálculo.
*   **WebAssembly**: Formato binario para ejecutar el código de Rust en el navegador a velocidad casi nativa.
*   **wasm-pack**: Herramienta CLI para compilar Rust a Wasm y generar el puente (*bindings*) de JavaScript.
*   **JavaScript / HTML5**: Interfaz de usuario interactiva y consumo del módulo asíncrono `.wasm`.
*   **GitHub Codespaces**: Entorno de desarrollo en la nube basado en contenedores Docker de desarrollo (`devcontainers`).

---
## Cómo probarlo

Se puede ejecutar la prueba directamente en https://migrassi.github.io/wasm-test/mi_proyecto_wasm/
---
## Cómo Ejecutarlo

Para levantar este entorno en un Codespace o de forma local:

1. Instalar las dependencias y compilar el módulo optimizado para producción:
   ```bash
   cd mi_proyecto_wasm
   wasm-pack build --target web --release
   ```

2. Levantar un servidor web local (necesario debido a las políticas de seguridad de los navegadores para módulos Wasm):
   ```bash
   python3 -m http.server 8080
   ```

3. Abrir el navegador en `http://localhost:8080` y presiona el botón para ejecutar el binario de Rust.
