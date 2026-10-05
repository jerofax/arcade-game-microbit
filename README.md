# arcade-game---microbit

Juego arcade para la **micro:bit** escrito en TypeScript/JavaScript con **Microsoft MakeCode**. Se juega en la pantalla de LEDs de 5×5: el jugador se mueve con los botones **A** y **B** y debe esquivar los bloques que van cayendo.

## Cómo se juega

- El jugador es un LED encendido en la fila inferior (posición inicial: columna 2, fila 4).
- **Botón A**: mueve al jugador una columna a la izquierda.
- **Botón B**: mueve al jugador una columna a la derecha.
- El movimiento es circular: si sales por un borde, apareces por el opuesto.
- Cada ronda cae un bloque desde la fila 0 hasta la fila 4, avanzando una fila cada 250 ms. Los bloques se eligen al azar entre 15 formas posibles (de 1 a 9 LEDs, ocupando una o dos filas de alto).
- Si el bloque toca al jugador, suena la melodía de *game over*, se muestra la puntuación (el contador de bloques de la partida) y el contador se reinicia a 0.
- Al iniciar el programa suena una melodía de introducción.

## Cómo ejecutarlo

El código está en el archivo [`arcade game`](arcade%20game) (sin extensión). Para probarlo:

1. Abre el editor de MakeCode para micro:bit (<https://makecode.microbit.org>) y crea un proyecto nuevo.
2. Cambia al modo **JavaScript** y pega el contenido del archivo `arcade game`.
3. Prueba el juego en el simulador del editor, o descárgalo y cópialo a tu micro:bit conectada por USB.

El juego usa el altavoz (`music`), por lo que necesitas una micro:bit con altavoz (o activar el sonido en el simulador) para oír las melodías.

## Tecnologías

- TypeScript/JavaScript en la variante de **Microsoft MakeCode para micro:bit**.
- APIs de MakeCode utilizadas: `input.onButtonPressed`, `basic.forever`, `basic.pause`, `basic.showNumber`, `basic.clearScreen`, `led.plotBrightness` y `music`.

## Estructura del repositorio

```
.
├── arcade game   # Código fuente completo del juego
└── README.md
```

Organización del código dentro de `arcade game`:

| Elemento | Función |
|---|---|
| `jugador` | Posición del jugador como `[x, y, intensidad]` |
| `intro()` / `gameover()` | Melodías de inicio y de fin de partida |
| `izquierda()` / `derecha()` | Movimiento del jugador (con ajuste circular en 5 columnas) |
| `crearBloque()` | Elige al azar un bloque de la lista `bloquesPosibles` |
| `colisiona()` | Comprueba si algún LED del bloque coincide con el del jugador |
| `mostrarBloques()` | Dibuja jugador y bloque, detecta colisión y baja el bloque una fila |
| `basic.forever` | Bucle principal: crea un bloque, suma al contador y lo muestra |

### Añadir bloques nuevos

Los bloques se definen en `bloquesPosibles` dentro de `crearBloque()`, como una lista de LEDs con la estructura `[ejeX, ejeY, intensidad]`. Basta con añadir una nueva entrada a esa lista.
