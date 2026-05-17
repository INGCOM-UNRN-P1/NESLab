# Manual de neslib para principiantes

## 1. ¿Qué es neslib?

**neslib** es una biblioteca pensada para desarrollar programas y juegos para **NES** usando **C** junto con **cc65**. Su objetivo es simplificar tareas comunes del hardware, como:

- manejo de paletas,
- escritura de fondo (*background*),
- manejo de sprites,
- lectura de controles,
- scroll,
- y organización de actualizaciones gráficas.

En lugar de escribir todo directamente contra registros del hardware, neslib ofrece funciones auxiliares más amigables para principiantes.

---

## 2. Herramientas que se usan junto con neslib

Lo habitual es trabajar con el toolchain **cc65**, que incluye:

- `cc65`: compila C a ensamblador 6502,
- `ca65`: ensambla,
- `ld65`: enlaza y genera el archivo final `.nes`.

Flujo general:

1. escribís código en `.c`,
2. el compilador lo transforma,
3. el ensamblador lo procesa,
4. el enlazador genera la ROM final.

---

## 3. Qué resuelve neslib

Sin una biblioteca auxiliar, programar para NES implica trabajar manualmente con:

- registros del PPU,
- memoria de video,
- sprites,
- lectura del gamepad,
- sincronización con v-blank.

neslib simplifica gran parte de eso con funciones reutilizables.

---

## 4. Conceptos mínimos antes de empezar

### 4.1 V-blank

Es el intervalo entre cuadros de imagen. Muchas actualizaciones gráficas deben realizarse en ese momento para evitar errores visuales.

### 4.2 PPU

Es el procesador gráfico de la NES. Se encarga del fondo, sprites, scroll y paletas.

### 4.3 OAM

Es el área de memoria que contiene los datos de sprites: posición, tile y atributos.

### 4.4 Nametable

Es la estructura de memoria que representa el fondo en tiles.

### 4.5 Paletas

La NES usa un conjunto limitado de colores. neslib facilita la carga y modificación de paletas.

---

## 5. Estructura básica de un programa con neslib

Un programa simple suele seguir este orden:

1. apagar el render,
2. cargar paletas,
3. preparar fondo,
4. inicializar sprites y variables,
5. activar el render,
6. entrar al bucle principal.

Dentro del bucle principal normalmente se hace:

- esperar el momento adecuado,
- leer controles,
- actualizar lógica,
- mover sprites,
- actualizar scroll o fondo.

Ejemplo esquemático:

```c
void main(void) {
  // inicialización
  // cargar paletas
  // cargar fondo
  // activar pantalla

  while (1) {
    // leer controles
    // actualizar lógica
    // actualizar gráficos
  }
}
```

---

## 6. Paletas

Las paletas determinan los colores que usan fondo y sprites.

Funciones típicas en muchas variantes de neslib:

- `pal_all(...)`
- `pal_bg(...)`
- `pal_spr(...)`
- `pal_col(...)`

Uso conceptual:

- `pal_all`: carga toda la paleta,
- `pal_bg`: carga la parte del fondo,
- `pal_spr`: carga la parte de sprites,
- `pal_col`: cambia un color individual.

Ejemplo:

```c
const unsigned char palette[32] = {
  0x0F,0x21,0x11,0x01,  0x0F,0x27,0x17,0x07,
  0x0F,0x2A,0x1A,0x0A,  0x0F,0x30,0x10,0x00,
  0x0F,0x16,0x27,0x18,  0x0F,0x21,0x11,0x01,
  0x0F,0x30,0x21,0x11,  0x0F,0x27,0x16,0x06
};
```

---

## 7. Fondo y escritura en pantalla

neslib suele incluir funciones para:

- escribir tiles,
- actualizar fondo,
- cargar bloques de datos,
- mostrar texto o elementos de interfaz.

La idea importante para principiantes es que no conviene escribir en VRAM en cualquier momento: muchas operaciones deben hacerse en el instante correcto o mediante buffers.

---

## 8. Sprites

Los sprites representan personajes, enemigos, disparos y objetos móviles.

Cada sprite suele tener:

- posición X,
- posición Y,
- tile gráfico,
- atributos.

Muchas veces un personaje completo no es un solo sprite, sino un **metasprite**, es decir, un conjunto de sprites pequeños formando una figura mayor.

Ejemplo conceptual:

```c
unsigned char player_x = 100;
unsigned char player_y = 120;
```

---

## 9. Controles

neslib también suele incluir ayuda para leer el gamepad.

Los botones habituales son:

- A,
- B,
- SELECT,
- START,
- ARRIBA,
- ABAJO,
- IZQUIERDA,
- DERECHA.

Ejemplo conceptual:

```c
if (pad & PAD_LEFT) player_x--;
if (pad & PAD_RIGHT) player_x++;
```

Para aprender, lo mejor es empezar haciendo que un sprite se mueva a izquierda y derecha.

---

## 10. Scroll

El scroll permite desplazar la cámara o el fondo.

Es útil para:

- niveles largos,
- seguimiento del jugador,
- escenas con movimiento horizontal o vertical.

Lo recomendable para principiantes es:

1. primero lograr una pantalla fija,
2. después probar un scroll simple,
3. luego pasar a mapas más grandes.

---

## 11. Audio

En proyectos para NES, el sonido suele manejarse con utilidades adicionales o funciones específicas del entorno.

Para una persona que recién empieza, conviene seguir este orden:

1. imagen,
2. entrada,
3. movimiento,
4. colisiones,
5. recién después sonido.

---

## 12. Errores comunes de principiantes

### 12.1 Escribir en VRAM en el momento incorrecto

Puede producir glitches o datos corruptos en pantalla.

### 12.2 Empezar con un proyecto demasiado grande

Es mejor comenzar con ejemplos pequeños:

- una pantalla fija,
- un sprite,
- un control,
- un disparo,
- una colisión simple.

### 12.3 Tratar a la NES como si fuera una PC moderna

La NES tiene muchas restricciones:

- menos memoria,
- CPU limitada,
- acceso al hardware muy controlado.

### 12.4 Suponer que todas las versiones de neslib son idénticas

Existen variantes y adaptaciones. Siempre conviene revisar los archivos reales del proyecto en el que se está trabajando.

---

## 13. Ruta de aprendizaje recomendada

### Nivel 1
- Cambiar paletas.
- Mostrar fondo o texto.

### Nivel 2
- Dibujar un sprite.
- Moverlo con controles.

### Nivel 3
- Disparar.
- Detectar colisiones.

### Nivel 4
- Agregar scroll.
- Organizar enemigos y objetos.

### Nivel 5
- Agregar sonido y efectos.
- Mejorar la estructura del juego.

---

## 14. Recomendación específica para NESLab

Si este manual se usa dentro de **NESLab**, conviene complementarlo con ejemplos del propio repositorio:

- mostrar cómo se compila un archivo `.c` a `.nes`,
- explicar los archivos de apoyo en `lib/`,
- describir cómo se usa el notebook,
- y conectar cada concepto con un ejemplo real del proyecto.

---

## 15. Resumen final

neslib es una ayuda para programar en NES sin tener que empezar desde cero con todos los detalles del hardware.

Para aprender bien:

- empezá con cosas pequeñas,
- entendé qué hacen paletas, sprites, controles y scroll,
- practicá con ejemplos cortos,
- y avanzá paso a paso.

La clave no es memorizar todas las funciones de una vez, sino entender cómo se organiza un programa simple para NES.
