# 🎮 NESLab: aprender cómo funciona una computadora con una consola de juegos de 8 bits

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ip-arch/NESLab/blob/main/NESLab_Notebook.ipynb)

**NESLab** es un material educativo que usa el hardware de la Family Computer (NES) como escenario para experimentar, mediante programación en lenguaje C, cómo funciona realmente una computadora.

A diferencia de las PC y los teléfonos inteligentes modernos, que suelen ocultar sus mecanismos internos tras capas de abstracción, una consola de 8 bits permite ver con claridad la interacción entre el **CPU, la memoria y el sistema de video (PPU)**. Esa transparencia la convierte en una plataforma ideal para estudiar los fundamentos de la computación de forma práctica.

---

## 🛠️ Qué se puede aprender (núcleo del recorrido)

A diferencia de una introducción típica a C centrada solo en mostrar texto por pantalla, este material apunta a una comprensión más esencial de la informática, conectada directamente con el hardware y los niveles bajos del sistema.

* **Historia de los sistemas operativos y los lenguajes de alto nivel**: por qué fue necesario usar **C** en lugar de programar únicamente en lenguaje máquina o ensamblador.
* **Arquitectura de programa almacenado**: cómo el CPU lee instrucciones desde la memoria (ROM/RAM) y las ejecuta.
* **Control de hardware**: la experiencia de manipular pantalla y sonido escribiendo directamente en direcciones específicas de memoria (registros).
* **Algoritmos y transiciones de estado**: la estructura de un ciclo de 1/60 de segundo que procesa entrada, detección de colisiones y dibujo.
* **La esencia de la compilación**: el proceso por el cual el código escrito por una persona en C (`.c`) se traduce, pasando por ensamblador (`.s`), hasta convertirse en código máquina (`.nes`).

---

## 🚀 Cómo empezar (para estudiantes y lectorado)

No hace falta instalar el entorno manualmente. Se puede comenzar simplemente abriendo el notebook en Google Colab y ejecutando sus celdas.

### 1. Abrir el notebook
Hacé clic en el botón **[Open In Colab]** que aparece al inicio de la página, guardá una copia en tu Google Drive y ejecutalo desde allí.

### 2. Construcción automática del entorno (dentro del notebook)
Al ejecutar la celda de configuración del entorno dentro del notebook, este repositorio se clona automáticamente en segundo plano y se instala `cc65`, el compilador de C para Family Computer / NES.

```python
# Código para clonar o actualizar el repositorio en Colab
!git clone https://github.com/ip-arch/NESLab.git /content/NESLab
%cd /content/NESLab
```

Una vez completada esa preparación, se pueden compilar y ejecutar los ejemplos directamente en Colab.

---

## 💡 En qué se diferencia de un curso tradicional de programación

El objetivo de NESLab no es únicamente enseñar sintaxis de C. Su propósito es ayudar a entender, mediante experiencia directa, temas como:

- cómo una computadora ejecuta instrucciones;
- cómo interactúan memoria, CPU y periféricos;
- cómo se representa una imagen en pantalla;
- cómo se construye un programa que responde a entradas en tiempo real.

En otras palabras, busca que quien aprende no se limite a “usar una computadora”, sino que también pueda comprender cómo está hecha por dentro.
