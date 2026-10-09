# Escritura Rápida ⌨️⏱

Mini proyecto #1 — **750014C Fundamentos de Programación Orientada a Eventos** (Universidad del Valle).

Juego de habilidad en el que el jugador debe escribir exactamente la palabra o frase que aparece en pantalla antes de que se acabe el tiempo. Cada acierto sube un nivel y, cada 5 niveles, el tiempo disminuye 2 segundos (mínimo 2 s).

## Integrantes

| Nombre | Código | Rama |
|---|---|---|
| Integrante 1 | 000000 | `xx` |
| Integrante 2 | 000000 | `yy` |
| Integrante 3 | 000000 | `zz` |

## Tecnologías

- Java 17+ (probado con Java 21)
- JavaFX 21 (controls + fxml)
- FXML diseñado con Scene Builder
- Maven
- Javadoc (HTML en la carpeta `docs/`)

## Cómo ejecutar

**IntelliJ IDEA:** `File → Open` → seleccionar la carpeta del proyecto (se importa como proyecto Maven) → ejecutar la clase `com.example.fastwriting.Main`.

**Terminal:**

```bash
mvn clean javafx:run
```

**Pruebas unitarias de las reglas del juego:**

```bash
mvn test
```

**Regenerar el Javadoc:**

```bash
mvn javadoc:javadoc
```

## Estructura (MVC)

```
src/main/java/com/example/fastwriting/
├── Main.java                     Punto de entrada (Application)
├── view/GameStage.java           Ventana: carga el FXML y crea la Scene
├── controller/GameController.java  Eventos de teclado, mouse y temporizador
└── model/
    ├── Game.java                 Reglas: nivel, validación exacta, tiempo por nivel
    ├── IWordProvider.java        Interfaz: proveedor de palabras
    ├── WordBank.java             Implementación: banco de palabras aleatorias
    ├── ITimerListener.java       Interfaz: escucha del temporizador
    ├── TimerAdapter.java         Clase adaptadora de ITimerListener
    └── GameTimer.java            Temporizador con Timeline
src/main/resources/com/example/fastwriting/
├── game-view.fxml                Vista
└── styles.css                    Estilos
```

## Requisitos técnicos

| Requisito | Implementación |
|---|---|
| Interfaces | `IWordProvider`, `ITimerListener` |
| Clase adaptadora | `TimerAdapter` (implementaciones vacías de `ITimerListener`) |
| Clases internas | `AnswerKeyHandler`, `TypingFeedbackHandler`, `HoverHandler` y la clase anónima que extiende `TimerAdapter` (en `GameController`) |
| Eventos de teclado | Enter valida, Esc borra, cada tecla soltada colorea el campo (azul si va bien, rojo si hay error); Enter en la pantalla inicial/final comienza el juego |
| Eventos de mouse | Clic en los botones, efecto *hover* (crece y cursor de mano) |

## Historias de usuario

- **HU-1:** palabra/frase aleatoria por nivel, campo de texto, validación con botón, Enter o al acabarse el tiempo; comparación exacta con `String.equals`.
- **HU-2:** 20 s iniciales, temporizador y barra de progreso en tiempo real (en rojo los últimos 5 s); al llegar a 0 se valida automáticamente y, si es incorrecto o vacío, termina la partida.
- **HU-3:** el nivel sube con cada acierto; cada 5 niveles −2 s (mínimo 2 s). Un error al validar no hace perder: solo se pierde si el tiempo se acaba con la respuesta incorrecta.
- **HU-4:** mensajes de éxito, error y aumento de dificultad; resumen final (niveles completados, tiempo restante, última palabra, récord) y botón para reiniciar desde el nivel 1. La partida también termina al completar 50 niveles.
