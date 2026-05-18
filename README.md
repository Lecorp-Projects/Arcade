# Arcade en Python con PySide6

Proyecto personal de aprendizaje enfocado en construir un **arcade de juegos clásicos** usando **Python**, **programación orientada a objetos** e **interfaces gráficas con PySide6 / Qt**.

La idea principal no es solo terminar juegos, sino aprender de forma práctica:

- organización de proyectos en Python;
- separación entre lógica e interfaz;
- creación de interfaces gráficas;
- manejo de estados de juego;
- uso de Git y GitHub;
- diseño progresivo de software.

---

## Objetivo del proyecto

Construir una aplicación de escritorio tipo **Arcade** que reúna varios juegos clásicos, cada uno con su propia lógica e interfaz, integrados luego en un menú principal.

El primer juego que se desarrollará será:

### Adivinar el número
Con tres modos:

1. El usuario adivina un número entre **1 y 10** con **3 intentos**.
2. El usuario adivina un número entre **1 y 100** con **7 intentos**.
3. El programa intenta adivinar el número pensado por el usuario.

---

## Juegos planeados

### 1. Adivinar el número
- Modo fácil: 1 a 10, 3 intentos.
- Modo normal: 1 a 100, 7 intentos.
- Modo en el que la máquina adivina el número del usuario.

### 2. Piedra, papel o tijera
- Jugador contra jugador.
- Jugador contra máquina.
- Formatos:
  - una partida;
  - mejor de 3;
  - mejor de 5.

### 3. Tres en raya
- Jugador contra jugador.
- Jugador contra máquina.

### 4. Cuatro en línea
- Jugador contra jugador.
- Jugador contra IA.
- Tablero de 6 filas por 7 columnas.
- Elección de nombres y fichas.
- Sorteo de turno inicial.
- Detección de victorias horizontales, verticales y diagonales.
- Empate.
- Reinicio de partida.
- Posibilidad de jugar una columna aleatoria.

### 5. Ahorcadito
- El programa escoge una palabra y el usuario intenta adivinarla.
- Posible modo futuro en el que el usuario propone la palabra y el programa intenta adivinarla.

### 6. Buscaminas
- Juego avanzado dentro del Arcade.
- Será uno de los retos más completos del proyecto por su lógica de tablero e interacción con casillas.

---

## Tecnologías principales

- **Python**
- **PySide6 / Qt**
- **Visual Studio Code**
- **Git y GitHub**

---

## Estructura actual del proyecto

```text
ARCADE/
├── docs/
│   ├── guia_comandos_vscode_python_git.md
│   └── guia_qt_pyside6_arcade.md
│
├── juegos/
│   ├── adivinar_numero/
│   │   ├── adivinar_numero.py
│   │   ├── logica.py
│   │   └── ui.py
│   │
│   ├── ahorcadito/
│   │   ├── ahorcadito.py
│   │   ├── logica.py
│   │   └── ui.py
│   │
│   ├── buscaminas/
│   │   ├── buscaminas.py
│   │   ├── logica.py
│   │   └── ui.py
│   │
│   ├── cuatro_en_linea/
│   │   ├── cuatro_en_linea.py
│   │   ├── logica.py
│   │   └── ui.py
│   │
│   ├── piedra_papel_tijera/
│   │   ├── piedra_papel_tijera.py
│   │   ├── logica.py
│   │   └── ui.py
│   │
│   └── tres_en_raya/
│       ├── tres_en_raya.py
│       ├── logica.py
│       └── ui.py
│
└── main.py
```

---

## Organización de cada juego

Cada juego se organizará inicialmente con tres archivos:

### `logica.py`
Contiene las reglas del juego, el estado de las partidas y los cálculos necesarios.

Ejemplos:
- intentos restantes;
- tablero;
- turnos;
- detección de victoria;
- decisiones de la IA.

### `ui.py`
Contiene la interfaz gráfica construida con PySide6 / Qt.

Ejemplos:
- ventanas;
- botones;
- textos;
- layouts;
- eventos de clic;
- actualización visual.

### `nombre_del_juego.py`
Funciona como punto de entrada independiente para ejecutar ese juego por separado durante el desarrollo.

Más adelante, el `main.py` general del Arcade integrará los distintos juegos dentro de una aplicación principal.

---

## Interfaz global

Se contempla crear una carpeta de utilidades compartidas cuando sea necesario, especialmente para elementos reutilizables de interfaz como:

- menú de pausa;
- botón de volver al menú principal;
- reinicio de partida;
- estilos visuales comunes.

---

## Documentación del proyecto

Dentro de `docs/` se encuentran guías de apoyo:

- **Guía de Qt con PySide6 para el Arcade**
- **Guía de comandos de VS Code, Python, Git y entornos virtuales**

Estas guías funcionan como material de consulta durante el desarrollo.

---

## Estado actual

El proyecto se encuentra en fase inicial de arquitectura y preparación del entorno.

### Ya realizado
- organización general del repositorio;
- definición de la estructura por juego;
- instalación y verificación de PySide6;
- documentación inicial;
- planeación de los juegos principales.

### Siguiente paso
Comenzar el desarrollo de la lógica y la interfaz del juego:

> **Adivinar el número**

---

## Instalación básica

### 1. Crear entorno virtual

```bash
python3 -m venv .venv
```

### 2. Activarlo en macOS

```bash
source .venv/bin/activate
```

### 3. Instalar PySide6

```bash
python -m pip install pyside6
```

---

## Filosofía de desarrollo

Este proyecto se construirá de forma progresiva:

1. pensar bien la estructura;
2. crear lógica limpia;
3. desarrollar interfaces funcionales;
4. mejorar visualmente;
5. integrar juegos dentro del Arcade;
6. refactorizar solo cuando aparezcan necesidades reales.

La prioridad es **entender bien cada decisión técnica**, no solo escribir código que funcione.
