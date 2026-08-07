# 🦀 Experimento: Rust + WebAssembly (Wasm) en la Nube

Este repositorio contiene un proyecto experimental para probar la integración y el rendimiento de **WebAssembly (Wasm)** utilizando **Rust**. El desarrollo se realizó por completo en un entorno virtual utilizando **GitHub Codespaces**, optimizando el uso de recursos locales al consumir **0 bytes** de espacio en disco físico.

## 📊 Resultados de Rendimiento

El experimento consistió en calcular el elemento 40 de la sucesión de Fibonacci (`102334155`) evaluando dos enfoques algorítmicos diferentes y los niveles de optimización del compilador de Rust:

| Algoritmo | Modo de Compilación | Tiempo de Ejecución | Observaciones |
| :--- | :--- | :--- | :--- |
| **Recursivo** | `Debug` | **245.70 ms** | Sobrecarga por información de depuración. |
| **Recursivo** | `Release` | **239.90 ms** | Cuello de botella en la Pila de Llamadas (*Call Stack*) del navegador. |
| **Iterativo** | `Release` 🚀 | **0.20 ms** | **Optimización máxima (~120,000% más rápido).** Ejecución directa en registros del CPU. |

---

## 🛠️ Tecnologías Utilizadas

*   **Rust (v1.97.1)**: Lenguaje de sistemas para el procesamiento matemático de alta velocidad.
*   **WebAssembly**: Formato binario para ejecutar el código de Rust en el navegador a velocidad casi nativa.
*   **wasm-pack**: Herramienta CLI para compilar Rust a Wasm y generar el puente (*bindings*) de JavaScript.
*   **JavaScript / HTML5**: Interfaz de usuario interactiva y consumo del módulo asíncrono `.wasm`.
*   **GitHub Codespaces**: Entorno de desarrollo en la nube basado en contenedores Docker de desarrollo (`devcontainers`).

---

## 🚀 Cómo Ejecutarlo

Si deseas levantar este entorno en un Codespace o de forma local:

1. Instala las dependencias y compila el módulo optimizado para producción:
   ```bash
   cd mi_proyecto_wasm
   wasm-pack build --target web --release
   ```

2. Levanta un servidor web local (necesario debido a las políticas de seguridad de los navegadores para módulos Wasm):
   ```bash
   python3 -m http.server 8080
   ```

3. Abre el navegador en `http://localhost:8080` y presiona el botón para ejecutar el binario de Rust.
