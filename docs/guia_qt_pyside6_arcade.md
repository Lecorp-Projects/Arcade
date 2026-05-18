# Guía de Qt con PySide6 para construir el Arcade en Python

**Objetivo de esta guía:**  
Aprender, desde cero y con explicaciones claras, los conceptos de **Qt / PySide6** necesarios para construir el proyecto **Arcade** con interfaces gráficas en Python, empezando por el juego **Adivina el número** y luego trasladando lo aprendido a Ahorcadito, Piedra Papel o Tijera, Cuatro en Línea y Buscaminas.

Esta guía no busca que memorices código. Busca que entiendas:

- qué es cada objeto;
- por qué existe;
- qué problema resuelve;
- cuándo usarlo;
- cómo encaja en la estructura de tu proyecto.

---

# 1. Qué es Qt, PySide6 y por qué lo vamos a usar

## 1.1. Qué es Qt

**Qt** es un framework para crear aplicaciones con interfaz gráfica.

Un framework es un conjunto organizado de herramientas, código y reglas que te da una base ya construida para desarrollar un programa más rápido y con una estructura definida, en lugar de tener que crear todo desde cero.

Sirve para construir programas con:

- ventanas;
- botones;
- cuadros de texto;
- menús;
- barras de herramientas;
- tablas;
- pestañas;
- diálogos;
- gráficos;
- manejo de eventos del mouse y teclado.

Qt se usa mucho para aplicaciones de escritorio profesionales.

Ejemplos del tipo de aplicación que se puede hacer con Qt:

- un reproductor multimedia;
- un gestor de gastos;
- un editor de texto;
- una calculadora gráfica;
- un juego sencillo con interfaz;
- herramientas internas para empresas.

---

## 1.2. Qué es PySide6

**PySide6** es la forma oficial de usar **Qt 6 desde Python**.

Dicho con plastilina:

- Qt es la “caja de herramientas”.
- PySide6 es el “adaptador” que permite usar esa caja desde Python.

Entonces, en Python puedes escribir:

```python
from PySide6.QtWidgets import QPushButton
```

y usar un botón de Qt sin programar en C++.

---

## 1.3. Por qué PySide6 encaja con este proyecto

Lo usaremos porque:

1. Permite aprender interfaces de verdad.
2. El Arcade permite practicar de forma divertida.
3. Qt te puede servir mucho si decides construir una app de escritorio.
4. Los conceptos de Qt te enseñan arquitectura de aplicaciones: eventos, pantallas, estado, separación de lógica y UI.

---

# 2. Cambio mental importante: de consola a interfaz gráfica

## 2.1. Cómo funciona un programa de consola

En consola, el flujo suele ser lineal:

```python
print("Hola")
nombre = input("¿Cómo te llamas?")
print("Mucho gusto", nombre)
```

El programa va línea por línea:

1. imprime;
2. espera el input;
3. continúa.

---

## 2.2. Cómo funciona una interfaz gráfica

En una GUI no escribes normalmente:

> “espera aquí hasta que el usuario pulse el botón”.

En cambio:

1. creas una ventana;
2. creas un botón;
3. le dices al botón qué función llamar cuando le hagan clic;
4. la app queda esperando eventos.

Ejemplo mental:

```python
boton.clicked.connect(iniciar_juego)
```

Esto significa:

> Cuando el botón sea presionado, ejecuta la función `iniciar_juego`.

---

## 2.3. Programación orientada a eventos

Una interfaz gráfica funciona con **eventos**.

Eventos típicos:

- clic de mouse;
- tecla presionada;
- texto cambiado;
- ventana cerrada;
- botón seleccionado;
- valor modificado.

En vez de que tu programa pregunte todo el tiempo “¿ya hicieron clic?”, Qt se encarga de escuchar y te avisa cuando ocurre algo.

---

# 3. El corazón de una aplicación Qt

## 3.1. `QApplication`

Toda aplicación Qt necesita un objeto `QApplication`.

Ejemplo mínimo:

```python
import sys
from PySide6.QtWidgets import QApplication, QLabel

app = QApplication(sys.argv)

etiqueta = QLabel("Hola desde Qt")
etiqueta.show()

sys.exit(app.exec())
```

---

## 3.2. Qué hace `QApplication`

`QApplication` administra:

- el ciclo de vida de la app;
- los eventos del mouse y teclado;
- el estilo general;
- las ventanas;
- la cola de eventos.

Piensa en él como el **director de orquesta** de toda la interfaz.

---

## 3.3. Qué hace `app.exec()`

```python
app.exec()
```

inicia el **bucle de eventos**.

Dicho simple:

> La aplicación queda viva, abierta y esperando clics, teclas y cambios.

Sin `app.exec()`, la ventana aparecería y se cerraría casi de inmediato.

---

## 3.4. Por qué se usa `sys.exit(app.exec())`

Forma común:

```python
sys.exit(app.exec())
```

Esto permite que el programa cierre correctamente y le devuelva al sistema operativo el código de salida.

Para empezar, basta con entender:

- `app.exec()` mantiene la interfaz funcionando;
- `sys.exit(...)` termina el proceso de forma ordenada.

---

# 4. `QWidget`: la base de casi todo lo visual

## 4.1. Qué es un widget

En Qt, un **widget** es un elemento visual o contenedor visual.

Ejemplos de widgets:

- un botón;
- una etiqueta;
- una caja de texto;
- una ventana;
- una tabla;
- un panel.

---

## 4.2. `QWidget`

`QWidget` es la clase base de muchísimos elementos visuales en Qt.

Puedes usarlo como:

1. una ventana simple;
2. un contenedor dentro de otra ventana;
3. la base para crear tus propios componentes.

Ejemplo:

```python
from PySide6.QtWidgets import QWidget

ventana = QWidget()
ventana.show()
```

---

## 4.3. Idea clave

Cuando veas una clase que empieza por `Q` y tiene que ver con interfaz, muchas veces está relacionada directa o indirectamente con `QWidget`.

---

# 5. `QMainWindow` vs `QWidget`

## 5.1. `QWidget` como ventana

Sirve muy bien para:

- juegos simples;
- formularios básicos;
- diálogos personalizados;
- prototipos.

---

## 5.2. `QMainWindow`

`QMainWindow` es una ventana principal más completa.  
Está pensada para aplicaciones que pueden necesitar:

- barra de menú;
- barra de herramientas;
- barra de estado;
- área central de contenido.

Ejemplo típico:

```python
from PySide6.QtWidgets import QMainWindow

class VentanaPrincipal(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Mi aplicación")
```

---

## 5.3. Qué usar en el Arcade

Para aprender y crear una app ordenada, tienes dos rutas válidas:

### Ruta simple
Usar `QWidget` como ventana principal.

### Ruta más escalable
Usar `QMainWindow` y colocar dentro un widget central.

Para el Arcade, recomiendo usar **QMainWindow** si vas a pensar la app completa como un programa con varias pantallas y navegación. Para empezar con el primer juego también se puede comenzar con `QWidget` y migrar después.

---

# 6. Cómo crear una ventana en PySide6

Ejemplo limpio con clase:

```python
import sys
from PySide6.QtWidgets import QApplication, QWidget

class Ventana(QWidget):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Adivina el número")
        self.resize(500, 400)

def main():
    app = QApplication(sys.argv)
    ventana = Ventana()
    ventana.show()
    sys.exit(app.exec())

if __name__ == "__main__":
    main()
```

---

## 6.1. Qué está pasando aquí

### `class Ventana(QWidget)`
Creamos nuestro propio tipo de ventana a partir de `QWidget`.

### `super().__init__()`
Inicializa correctamente la parte Qt de la clase.

### `self.setWindowTitle(...)`
Cambia el título de la ventana.

### `self.resize(500, 400)`
Define un tamaño inicial.

### `ventana.show()`
Muestra la ventana.

### `app.exec()`
Mantiene viva la app.

---

# 7. Los widgets más importantes para tu Arcade

---

## 7.1. `QLabel`: mostrar texto

Sirve para mostrar:

- títulos;
- instrucciones;
- resultados;
- intentos restantes;
- mensajes de error.

Ejemplo:

```python
from PySide6.QtWidgets import QLabel

titulo = QLabel("Adivina el número")
mensaje = QLabel("Elige un modo de juego")
```

Puedes cambiar su texto luego:

```python
mensaje.setText("El número secreto es mayor")
```

---

## 7.2. `QPushButton`: botones

Sirve para opciones clicables.

Ejemplo:

```python
from PySide6.QtWidgets import QPushButton

boton_facil = QPushButton("Modo fácil")
```

Conectar clic a función:

```python
boton_facil.clicked.connect(iniciar_modo_facil)
```

---

## 7.3. `QLineEdit`: caja de texto de una línea

Sirve para que el usuario escriba:

- un número;
- un nombre;
- una respuesta breve.

Ejemplo:

```python
from PySide6.QtWidgets import QLineEdit

entrada = QLineEdit()
entrada.setPlaceholderText("Escribe tu número")
```

Leer lo escrito:

```python
texto = entrada.text()
```

Limpiar:

```python
entrada.clear()
```

---

## 7.4. `QSpinBox`: entrada numérica controlada

Para números, muchas veces es mejor que `QLineEdit`.

Permite:

- definir mínimo y máximo;
- subir o bajar con flechas;
- obtener directamente un entero.

Ejemplo:

```python
from PySide6.QtWidgets import QSpinBox

selector = QSpinBox()
selector.setMinimum(1)
selector.setMaximum(100)
numero = selector.value()
```

### Cuándo usarlo

En el modo “usuario adivina”, podrías usar:

- `QLineEdit` si quieres practicar validación;
- `QSpinBox` si quieres una UI más cómoda y restringida.

Para aprender, puede ser interesante empezar con `QLineEdit` y luego comparar con `QSpinBox`.

---

## 7.5. `QVBoxLayout` y `QHBoxLayout`

Los layouts ordenan los widgets.

### `QVBoxLayout`
Coloca elementos uno debajo del otro.

```python
from PySide6.QtWidgets import QVBoxLayout

layout = QVBoxLayout()
layout.addWidget(titulo)
layout.addWidget(boton_facil)
layout.addWidget(boton_normal)
```

### `QHBoxLayout`
Coloca elementos de izquierda a derecha.

```python
from PySide6.QtWidgets import QHBoxLayout

fila = QHBoxLayout()
fila.addWidget(boton_mayor)
fila.addWidget(boton_menor)
```

---

# 8. Layouts: por qué no conviene poner posiciones a mano

## 8.1. Colocar a mano

Podrías hacer:

```python
boton.move(100, 50)
```

Pero no conviene para una app que quieres que crezca.

Problemas:

- se desordena al cambiar tamaño de ventana;
- queda mal en otras resoluciones;
- cuesta mantenerlo;
- es más frágil.

---

## 8.2. Usar layouts

Los layouts se encargan de:

- alinear;
- distribuir espacio;
- responder a tamaños de ventana;
- mantener la interfaz limpia.

En Qt, aprender layouts es fundamental.

---

# 9. Señales y slots: el idioma de las interacciones

## 9.1. Qué es una señal

Una **señal** es una notificación que emite un objeto cuando ocurre algo.

Ejemplos:

- un botón emite `clicked`;
- un texto emite algo cuando cambia;
- una casilla emite algo cuando se marca.

---

## 9.2. Qué es un slot

Un **slot** es una función que recibe o responde a una señal.

Ejemplo:

```python
def saludar():
    print("Hola")
```

---

## 9.3. Conectar señal y función

```python
boton.clicked.connect(saludar)
```

Se lee:

> Cuando el botón sea clicado, llama a `saludar`.

---

## 9.4. Ejemplo completo

```python
from PySide6.QtWidgets import QWidget, QPushButton, QVBoxLayout, QLabel

class Ventana(QWidget):
    def __init__(self):
        super().__init__()

        self.etiqueta = QLabel("Aún no has pulsado el botón")
        self.boton = QPushButton("Haz clic")

        self.boton.clicked.connect(self.cambiar_texto)

        layout = QVBoxLayout()
        layout.addWidget(self.etiqueta)
        layout.addWidget(self.boton)

        self.setLayout(layout)

    def cambiar_texto(self):
        self.etiqueta.setText("¡Botón pulsado!")
```

---

# 10. `self`: por qué aparece tanto

En clases, `self` significa:

> este objeto actual.

Si escribes:

```python
self.etiqueta = QLabel("Hola")
```

esa etiqueta queda guardada dentro de la ventana.

Luego puedes acceder a ella desde otro método:

```python
self.etiqueta.setText("Nuevo texto")
```

---

## 10.1. Qué pasa si no usas `self`

Si haces:

```python
etiqueta = QLabel("Hola")
```

la variable existe solo dentro de `__init__`.  
Después otra función no la puede modificar fácilmente.

---

## 10.2. Regla práctica

Usa `self.` para elementos que necesitarás modificar después:

- labels cuyo texto cambia;
- botones que vas a ocultar o desactivar;
- input del usuario;
- variables de estado del juego.

---

# 11. Estado de la aplicación

## 11.1. Qué es estado

El **estado** son los datos que describen en qué momento se encuentra el programa.

En “Adivina el número”:

- modo actual;
- número secreto;
- intentos restantes;
- límite inferior;
- límite superior;
- si el juego terminó o no.

---

## 11.2. Ejemplo

```python
self.numero_secreto = 7
self.intentos_restantes = 3
self.juego_activo = True
```

---

## 11.3. Por qué importa separar estado y UI

Si mezclas todo, el código se vuelve confuso:

- un botón calcula;
- un label decide;
- la lógica imprime;
- la interfaz compara valores.

Mejor:

- la lógica decide;
- la UI muestra.

---

# 12. Separación entre lógica y UI en tu proyecto

Tu estructura pensada es muy buena:

```text
adivina_el_numero/
├── adivina_el_numero.py
├── logica.py
└── ui.py
```

---

## 12.1. `logica.py`

Debe contener reglas puras del juego.

Ejemplos de responsabilidades:

- generar número aleatorio;
- comparar intento con número secreto;
- saber si acertó;
- calcular pistas;
- manejar la búsqueda binaria para que la máquina adivine.

Idealmente, `logica.py` no debería depender de Qt.

---

## 12.2. `ui.py`

Debe contener lo visual:

- ventana;
- botones;
- labels;
- layouts;
- cambios de pantalla;
- conexión de eventos.

---

## 12.3. `adivina_el_numero.py`

Puede ser el archivo que:

- inicia `QApplication`;
- crea la ventana principal del juego;
- ejecuta la app.

---

# 13. El juego Adivina el número: diseño recomendado

## 13.1. Pantalla inicial

Elementos:

- título: “Adivina el número”;
- descripción breve;
- tres botones.

Botones:

1. **Modo fácil**
   - rango 1 a 10;
   - 3 intentos.

2. **Modo normal**
   - rango 1 a 100;
   - 7 intentos.

3. **La máquina adivina**
   - usuario piensa un número;
   - el programa intenta descubrirlo.

---

## 13.2. Pantalla modo fácil / normal

Elementos:

- texto del rango;
- intentos restantes;
- entrada del número;
- botón “Probar”;
- mensaje dinámico:
  - “Es mayor”;
  - “Es menor”;
  - “Adivinaste”;
  - “Se acabaron los intentos”;
- botón de volver al menú.

---

## 13.3. Pantalla modo máquina adivina

Elementos:

- texto: “Piensa un número del 1 al 100”;
- propuesta actual de la máquina:
  - “¿Tu número es 50?”;
- botones:
  - “Es mayor”;
  - “Es menor”;
  - “Adivinaste”;
- contador de intentos;
- botón volver.

---

# 14. Lógica del modo “la máquina adivina”

Aquí aprenderás una idea muy elegante: **búsqueda binaria**.

## 14.1. Idea simple

Si el número está entre 1 y 100:

1. la máquina pregunta 50;
2. si dices “mayor”, descarta 1–50;
3. si dices “menor”, descarta 50–100;
4. vuelve a preguntar el centro del rango que queda.

---

## 14.2. Ejemplo

Número pensado por el usuario: 73.

La máquina hace:

- 50 → usuario dice mayor;
- 75 → usuario dice menor;
- 62 → mayor;
- 68 → mayor;
- 71 → mayor;
- 73 → correcto.

---

## 14.3. Datos que necesita guardar

```python
limite_inferior = 1
limite_superior = 100
intento_actual = 50
```

Si el usuario dice “mayor”:

```python
limite_inferior = intento_actual + 1
```

Si dice “menor”:

```python
limite_superior = intento_actual - 1
```

Siguiente intento:

```python
intento_actual = (limite_inferior + limite_superior) // 2
```

---

# 15. Cambiar entre pantallas

Para una app con varias secciones, tienes varias formas.

## 15.1. Opción sencilla: reconstruir contenido

Cuando cambias de pantalla:

- limpias el layout;
- agregas nuevos widgets.

Sirve para aprender, pero hay que hacerlo con cuidado.

---

## 15.2. Opción recomendada: `QStackedWidget`

`QStackedWidget` permite tener varias “pantallas” dentro de una misma ventana y mostrar solo una a la vez.

Ejemplo conceptual:

- pantalla 0: menú;
- pantalla 1: modo usuario adivina;
- pantalla 2: modo máquina adivina.

Luego cambias así:

```python
stack.setCurrentIndex(1)
```

---

## 15.3. Por qué puede servirte mucho

El Arcade completo eventualmente podría tener:

- pantalla de menú principal;
- pantalla de cada juego;
- pantalla de instrucciones;
- pantalla de resultados.

`QStackedWidget` es una herramienta muy buena para eso.

---

# 16. Estilos visuales con Qt Style Sheets

## 16.1. Qué son

Qt permite estilizar widgets con una sintaxis parecida a CSS.

Ejemplo:

```python
boton.setStyleSheet(
    """
    QPushButton {
        font-size: 18px;
        padding: 12px;
        border-radius: 8px;
    }
    """
)
```

---

## 16.2. Qué puedes personalizar

- tamaño de fuente;
- margen interno;
- bordes;
- radios;
- colores;
- estados hover;
- fondo.

---

## 16.3. Recomendación

Primero haz que la interfaz funcione.  
Después la pones bonita.

Orden correcto:

1. ventana funcional;
2. botones conectados;
3. lógica correcta;
4. navegación;
5. estilos.

---

# 17. Mostrar mensajes: label, diálogo o barra de estado

## 17.1. `QLabel`

Para mensajes dentro de la interfaz:

```python
self.mensaje.setText("El número secreto es mayor")
```

Es ideal para el juego.

---

## 17.2. `QMessageBox`

Para ventanas emergentes:

- victoria;
- error importante;
- confirmaciones.

Ejemplo conceptual:

```python
QMessageBox.information(self, "Ganaste", "Adivinaste el número")
```

---

## 17.3. Cuándo usar cada uno

### Usa `QLabel` si:
- el mensaje forma parte del flujo normal;
- debe permanecer visible.

### Usa `QMessageBox` si:
- necesitas llamar mucho la atención;
- quieres pausar el flujo hasta que el usuario cierre el mensaje.

---

# 18. Habilitar, deshabilitar, ocultar y mostrar widgets

## 18.1. Deshabilitar

```python
boton.setEnabled(False)
```

Útil si:

- se acabó el juego;
- aún falta seleccionar un modo;
- una acción no está disponible.

---

## 18.2. Volver a habilitar

```python
boton.setEnabled(True)
```

---

## 18.3. Ocultar y mostrar

```python
boton.hide()
boton.show()
```

Esto ayuda si quieres mostrar elementos solo en ciertos momentos.

---

# 19. Validación de entradas

## 19.1. Problema típico

Si usas `QLineEdit`, el usuario puede escribir:

- letras;
- espacios;
- vacío;
- 999;
- -3.

---

## 19.2. Primera forma: validar con Python

```python
texto = self.entrada.text()

if not texto.isdigit():
    self.mensaje.setText("Escribe un número válido")
    return
```

Luego conviertes:

```python
numero = int(texto)
```

---

## 19.3. Segunda forma: usar `QIntValidator`

Qt puede impedir directamente que se escriban valores no válidos.

Ejemplo conceptual:

```python
from PySide6.QtGui import QIntValidator

self.entrada.setValidator(QIntValidator(1, 100))
```

---

## 19.4. Qué recomiendo para aprender

Primero entiende validación manual.  
Luego prueba `QIntValidator` para comparar.

---

# 20. Organización de funciones dentro de una UI

En una clase de interfaz, evita hacer un método monstruoso.

Mejor divide.

Ejemplo conceptual:

```python
class VentanaAdivina(QWidget):
    def __init__(self):
        super().__init__()
        self.configurar_ventana()
        self.crear_widgets()
        self.crear_layouts()
        self.conectar_eventos()
```

---

## 20.1. Qué hace cada método

### `configurar_ventana()`
- título;
- tamaño;
- configuración inicial.

### `crear_widgets()`
- crea labels, inputs, botones.

### `crear_layouts()`
- organiza todo.

### `conectar_eventos()`
- botones y señales.

Esto vuelve el código mucho más legible.

---

# 21. Ejemplo de arquitectura sencilla para una pantalla

```python
class PantallaMenu(QWidget):
    def __init__(self):
        super().__init__()
        self.crear_widgets()
        self.crear_layout()
        self.conectar_eventos()

    def crear_widgets(self):
        self.titulo = QLabel("Adivina el número")
        self.boton_facil = QPushButton("Modo fácil")
        self.boton_normal = QPushButton("Modo normal")

    def crear_layout(self):
        layout = QVBoxLayout()
        layout.addWidget(self.titulo)
        layout.addWidget(self.boton_facil)
        layout.addWidget(self.boton_normal)
        self.setLayout(layout)

    def conectar_eventos(self):
        self.boton_facil.clicked.connect(self.ir_modo_facil)
        self.boton_normal.clicked.connect(self.ir_modo_normal)

    def ir_modo_facil(self):
        pass

    def ir_modo_normal(self):
        pass
```

Este ejemplo no tiene la app completa; solo muestra cómo organizar una pantalla.

---

# 22. Cómo pensar el Arcade completo

A futuro, el proyecto podría verse conceptualmente así:

```text
main.py
utilidades/
juegos/
  adivina_el_numero/
  ahorcadito/
  piedra_papel_o_tijera/
  cuatro_en_linea/
  buscaminas/
```

---

## 22.1. Menú principal del Arcade

Pantalla con botones:

- Adivina el número
- Ahorcadito
- Piedra Papel o Tijera
- Cuatro en Línea
- Buscaminas

Cada botón abre la pantalla del juego correspondiente.

---

## 22.2. Cada juego con UI propia

Cada juego puede tener:

- su lógica;
- su interfaz;
- sus pantallas internas si las necesita.

---

## 22.3. Utilidades compartidas

A medida que avances, quizá aparezcan elementos reutilizables:

- estilos comunes;
- funciones para títulos;
- diálogos reutilizables;
- constantes de tamaño;
- navegación.

Solo los creas cuando realmente veas repetición.

---

# 23. Qué aprenderás al trasladarlo a cada juego

## 23.1. Adivina el número
Aprendes:
- botones;
- labels;
- entrada;
- cambios de texto;
- estado;
- pantallas.

## 23.2. Piedra Papel o Tijera
Aprendes:
- botones como opciones;
- imágenes o emojis;
- resultados instantáneos;
- reinicio de partida.

## 23.3. Ahorcadito
Aprendes:
- teclado o botones de letras;
- actualizar palabra oculta;
- mostrar letras usadas;
- imágenes por etapas.

## 23.4. Cuatro en Línea
Aprendes:
- cuadrículas;
- botones distribuidos;
- tablero visual;
- color de fichas;
- lógica de turnos.

## 23.5. Buscaminas
Aprendes:
- grillas grandes;
- botones dinámicos;
- clic izquierdo / derecho;
- actualización masiva de UI;
- lógica más compleja.

---

# 24. Widgets y clases que probablemente usarás en el Arcade

| Clase | Para qué sirve |
|---|---|
| `QApplication` | Iniciar y sostener la aplicación |
| `QWidget` | Base de ventanas y componentes |
| `QMainWindow` | Ventana principal completa |
| `QLabel` | Mostrar texto o imágenes |
| `QPushButton` | Botones |
| `QLineEdit` | Entrada de texto corta |
| `QSpinBox` | Entrada numérica |
| `QVBoxLayout` | Layout vertical |
| `QHBoxLayout` | Layout horizontal |
| `QGridLayout` | Layout en cuadrícula |
| `QStackedWidget` | Varias pantallas en una misma ventana |
| `QMessageBox` | Mensajes emergentes |
| `QIntValidator` | Validación numérica |
| `QPixmap` | Mostrar imágenes |
| `QTimer` | Temporizadores, retrasos o animaciones simples |

---

# 25. `QGridLayout`: esencial para tableros

## 25.1. Qué es

Organiza widgets en filas y columnas.

Muy útil para:

- Buscaminas;
- Cuatro en Línea;
- teclados de letras.

---

## 25.2. Ejemplo conceptual

```python
grid = QGridLayout()

grid.addWidget(boton_1, 0, 0)
grid.addWidget(boton_2, 0, 1)
grid.addWidget(boton_3, 1, 0)
```

---

## 25.3. Cómo imaginarlo

```text
fila 0: [botón 1] [botón 2]
fila 1: [botón 3] [        ]
```

---

# 26. Imágenes con `QPixmap`

Para mostrar una imagen:

```python
from PySide6.QtGui import QPixmap
from PySide6.QtWidgets import QLabel

imagen = QLabel()
pixmap = QPixmap("ruta/a/imagen.png")
imagen.setPixmap(pixmap)
```

Esto te puede servir para:

- estados del ahorcado;
- iconos de botones;
- adornos del menú.

---

# 27. Eventos de teclado y mouse

Qt permite reaccionar más allá de botones.

## 27.1. Teclado

Podrías permitir que en Ahorcadito el usuario escriba una letra sin hacer clic en la caja.

## 27.2. Mouse

En Buscaminas podrías diferenciar:

- clic izquierdo: revelar casilla;
- clic derecho: marcar bandera.

Esto ya es más avanzado, pero será muy útil.

---

# 28. Errores típicos al empezar con Qt

## 28.1. Crear widgets pero no agregarlos a un layout
Si no lo organizas o muestras bien, puede no aparecer como esperas.

## 28.2. Olvidar `show()`
Sin `show()`, la ventana no se ve.

## 28.3. Escribir `funcion()` al conectar
Incorrecto:

```python
boton.clicked.connect(mi_funcion())
```

Eso ejecuta la función de una vez.

Correcto:

```python
boton.clicked.connect(mi_funcion)
```

---

## 28.4. Hacer toda la lógica dentro del método del botón
Funciona al principio, pero luego el código se vuelve difícil de mantener.

Mejor:

- el botón toma el input;
- llama una función de lógica;
- actualiza la UI con el resultado.

---

## 28.5. Usar demasiados `print()` en una GUI
Los `print()` siguen sirviendo para depurar, pero la comunicación con el usuario debe vivir en la interfaz.

---

# 29. Método recomendado de aprendizaje para este proyecto

## Paso 1
Crear una ventana vacía.

## Paso 2
Mostrar título y botones de modos.

## Paso 3
Conectar botones a funciones temporales.

## Paso 4
Cambiar de pantalla o cambiar contenido.

## Paso 5
Implementar modo fácil.

## Paso 6
Implementar modo normal reutilizando estructura.

## Paso 7
Implementar modo máquina adivina.

## Paso 8
Pulir estilos.

## Paso 9
Conectar el juego al Arcade general.

---

# 30. Cómo no perderte al aprender Qt

Cuando veas código nuevo, pregúntate:

1. ¿Esto es un widget?
2. ¿Esto es un layout?
3. ¿Esto es una señal?
4. ¿Esto es un método que cambia estado?
5. ¿Esto pertenece a UI o a lógica?

Si puedes responder esas preguntas, estás entendiendo.

---

# 31. Mini glosario

## Framework
Conjunto grande de herramientas y reglas para construir aplicaciones.

## GUI
Interfaz gráfica de usuario.

## Widget
Elemento visual de una interfaz.

## Layout
Organizador automático de widgets.

## Señal
Aviso de que ocurrió algo.

## Slot
Función que responde a una señal.

## Evento
Acción del usuario o del sistema.

## Estado
Datos actuales que describen el momento del programa.

## `self`
Referencia al objeto actual.

## `QApplication`
Motor principal de una app Qt.

## `QMainWindow`
Ventana principal con estructura completa.

## `QStackedWidget`
Contenedor de varias pantallas.

---

# 32. Cuándo considerar Qt Designer

Qt Designer permite diseñar interfaces arrastrando widgets.

Puede servir mucho más adelante para:

- aplicaciones con formularios grandes;
- pantallas de gestión de gastos;
- prototipos visuales rápidos.

Pero para aprender fundamentos, conviene empezar haciendo interfaces por código. Así entiendes de verdad:

- qué objetos existen;
- cómo se acomodan;
- cómo se conectan.

---

# 33. Cómo se relaciona esto con tu proyecto de gastos e ingresos

Todo lo aprendido aquí se reutiliza.

## En el gestor de finanzas podrías tener:

- menú lateral o pestañas;
- formulario para añadir gasto;
- caja de monto;
- selector de categoría;
- calendario de fecha;
- tabla de transacciones;
- botones editar/eliminar;
- resúmenes;
- gráficas.

## Qt te enseñará desde ahora:
- cómo separar lógica de interfaz;
- cómo controlar pantallas;
- cómo reaccionar a eventos;
- cómo mantener datos en memoria;
- cómo escalar una interfaz.

---

# 34. Recomendación de arquitectura inicial para Adivina el número

Una forma ordenada de empezar sería:

```text
adivina_el_numero/
├── adivina_el_numero.py   # arranque del juego
├── ui.py                  # ventana y pantallas
└── logica.py              # reglas del juego
```

---

## 34.1. Dentro de `logica.py`

Funciones posibles:

```python
generar_numero_secreto(limite_minimo, limite_maximo)
comparar_intento(numero_usuario, numero_secreto)
crear_estado_maquina(limite_minimo, limite_maximo)
calcular_siguiente_intento(...)
```

No hace falta definirlas todas de una vez. Se van descubriendo mientras construyes.

---

## 34.2. Dentro de `ui.py`

Clases o pantallas posibles:

```python
VentanaAdivinaNumero
PantallaMenu
PantallaUsuarioAdivina
PantallaMaquinaAdivina
```

Para el primer intento, puedes empezar más simple y luego dividir.

---

# 35. Filosofía de trabajo para este proyecto

No busques terminarlo rápido.  
Busca entenderlo bien.

Cada avance debería responder:

- ¿qué aprendí hoy?;
- ¿qué objeto de Qt entendí?;
- ¿qué parte de la UI quedó más clara?;
- ¿qué parte de la lógica quedó separada?

Si haces eso, el juego será divertido, pero además se convertirá en una base muy buena para proyectos más serios.

---

# 36. Checklist de conocimientos que iremos cubriendo

Marca mentalmente estos puntos a medida que avances:

- [ ] Instalar PySide6
- [ ] Crear `QApplication`
- [ ] Crear una ventana
- [ ] Mostrar widgets
- [ ] Usar layouts
- [ ] Conectar botones con funciones
- [ ] Cambiar textos de labels
- [ ] Leer entradas de usuario
- [ ] Validar entradas
- [ ] Manejar estado de una partida
- [ ] Cambiar entre pantallas
- [ ] Separar UI y lógica
- [ ] Estilizar con Qt Style Sheets
- [ ] Crear grillas
- [ ] Mostrar imágenes
- [ ] Usar eventos de mouse/teclado cuando toque
- [ ] Preparar una interfaz escalable para el Arcade completo

---

# 37. Cierre

El juego **Adivina el número** es una muy buena puerta de entrada a Qt porque:

- la lógica es sencilla;
- permite crear una interfaz con varias pantallas;
- obliga a manejar estado;
- usa botones, texto, entradas y eventos;
- introduce una idea algorítmica elegante con el modo de la máquina;
- sirve como entrenamiento real antes de construir interfaces más complejas.

El objetivo no es solo que el juego funcione.  
El objetivo es que al terminarlo puedas decir:

> “Entiendo cómo se construye una aplicación gráfica en Python con Qt, y ya tengo bases para crear interfaces más grandes.”
