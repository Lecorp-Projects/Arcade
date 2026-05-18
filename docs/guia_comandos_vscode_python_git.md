# Guía de comandos básicos para trabajar en VS Code, Python, Git y entornos virtuales

**Propósito de esta guía**  
Este documento reúne, explica y organiza los comandos y conceptos básicos que ya hemos usado o que serán muy útiles mientras desarrollas tu proyecto **Arcade en Python con PySide6** desde **Visual Studio Code**.

La idea es que puedas volver a este archivo cuando te preguntes:

- “¿Dónde ejecuto este comando?”
- “¿Qué hace exactamente?”
- “¿Por qué lo usamos?”
- “¿Cómo verifico si algo quedó bien?”
- “¿Qué comandos de terminal, Python y Git debería conocer al empezar?”

---

# 1. Dónde se escriben los comandos

## 1.1. Terminal de VS Code

Los comandos como:

```bash
pwd
python3 -m venv .venv
source .venv/bin/activate
python -m pip install pyside6
git status
```

**no se escriben dentro de archivos `.py`**.

Se escriben en la **terminal integrada de VS Code**.

---

## 1.2. Cómo abrir la terminal en VS Code

Desde el menú superior:

```text
Terminal → New Terminal
```

## 1.3. Cómo reconocer que estás en la terminal

Verás algo parecido a esto:

```text
 ...Arcade %
```

o si el entorno virtual está activo:

```text
(.venv) ... Arcade %
```

La parte final suele indicar la carpeta en la que estás, y el símbolo `%` o `$` significa que la terminal está esperando un comando.

---

# 2. Qué es una terminal

La **terminal** es una forma de darle instrucciones directas al sistema operativo mediante texto.

Desde ella puedes:

- moverte entre carpetas;
- ver archivos;
- crear directorios;
- ejecutar Python;
- instalar librerías;
- usar Git;
- correr programas;
- consultar configuraciones.

No reemplaza a VS Code, sino que lo complementa.

---

# 3. Carpetas y rutas: conceptos esenciales

---

## 3.1. Working directory o directorio de trabajo

El **working directory** es:

> La carpeta en la que la terminal está “parada” en ese momento.

Si estás dentro de:

```text
/.../Arcade
```

y creas una carpeta, esa carpeta se crea **dentro de Arcade**.

---

## 3.2. Por qué importa

Muchos comandos actúan sobre la carpeta actual.

Ejemplo:

```bash
python3 -m venv .venv
```

crea `.venv` **en la carpeta en la que estés parado**.

Por eso primero usamos:

```bash
pwd
```

para confirmar que estábamos dentro del proyecto `ARCADE`.

---

# 4. Comandos básicos para moverte en la terminal

---

## 4.1. `pwd`

```bash
pwd
```

### Significado
`pwd` significa:

> **print working directory**

### Qué hace
Muestra la ruta completa de la carpeta actual.

### Ejemplo de salida

```text
/.../ARCADE
```

### Para qué sirve
Para confirmar en qué carpeta estás antes de ejecutar comandos importantes.

---

## 4.2. `ls`

```bash
ls
```

### Qué hace
Lista los archivos y carpetas del directorio actual.

### Ejemplo

```text
juegos
utilidades
main.py
README.md
```

---

## 4.3. `ls -a`

```bash
ls -a
```

### Qué hace
Muestra también los archivos ocultos.

En macOS y Linux, los archivos o carpetas que comienzan con punto `.` suelen considerarse ocultos.

Ejemplos:

```text
.git
.venv
.gitignore
```

---

## 4.4. `cd`

```bash
cd nombre_de_carpeta
```

### Significado
`cd` significa:

> **change directory**

### Qué hace
Te mueve a otra carpeta.

### Ejemplo

```bash
cd juegos
```

Ahora la terminal queda dentro de:

```text
ARCADE/juegos
```

---

## 4.5. Volver a la carpeta anterior con `cd ..`

```bash
cd ..
```

### Qué hace
Sube un nivel en la estructura de carpetas.

Ejemplo:

Si estás en:

```text
ARCADE/juegos
```

y escribes:

```bash
cd ..
```

vuelves a:

```text
ARCADE
```

---

## 4.6. Ir a tu carpeta personal con `cd ~`

```bash
cd ~
```

### Qué hace
Te lleva a tu carpeta de usuario en macOS.

Ejemplo aproximado:

```text
/Users/...
```

---

## 4.7. Limpiar la terminal con `clear`

```bash
clear
```

### Qué hace
Limpia visualmente el contenido anterior de la terminal.

No borra archivos ni historial real; solo despeja la pantalla.

---

# 5. Python en terminal

---

## 5.1. Ver versión de Python

En macOS normalmente usamos:

```bash
python3 --version
```

Ejemplo de salida:

```text
Python 3.13.3
```

También puede servir:

```bash
python --version
```

si el entorno virtual está activo o si tu sistema ya tiene esa configuración.

---

## 5.2. Abrir la consola interactiva de Python

```bash
python3
```

o dentro de un entorno virtual:

```bash
python
```

### Qué ocurre
Se abre una consola donde puedes escribir Python línea por línea.

Ejemplo:

```python
>>> 2 + 2
4
```

### Cómo salir
Puedes escribir:

```python
exit()
```

o usar:

```text
Control + D
```

---

## 5.3. Ejecutar un archivo Python

```bash
python archivo.py
```

Ejemplo:

```bash
python main.py
```

Si estás fuera de un entorno virtual, en macOS podría ser:

```bash
python3 main.py
```

---

## 5.4. Ejecutar un módulo simple desde la terminal con `-c`

Ejemplo que usamos:

```bash
python -c "import PySide6; print('PySide6 quedó instalado correctamente')"
```

### Qué significa `-c`
Le dice a Python:

> Ejecuta el código que escribo entre comillas.

### Para qué sirve
Para pruebas rápidas sin crear un archivo `.py`.

---

# 6. Entornos virtuales de Python

---

## 6.1. Qué es un entorno virtual

Un **entorno virtual** es una instalación aislada de Python y paquetes para un proyecto específico.

Dicho simple:

> Es una “cajita” independiente donde instalas las librerías de ese proyecto sin afectar las demás.

---

## 6.2. Por qué usamos uno en Arcade

Porque este proyecto necesita:

```text
PySide6
```

y queremos que esa librería quede asociada a **este proyecto**, no instalada de forma desordenada en todo el sistema.

---

## 6.3. Crear un entorno virtual

Comando que usamos:

```bash
python3 -m venv .venv
```

---

### Explicación por partes

#### `python3`
Usa Python 3.

#### `-m`
Significa:

> Ejecuta un módulo de Python como programa.

#### `venv`
Es el módulo integrado de Python para crear entornos virtuales.

#### `.venv`
Es el nombre de la carpeta que contendrá el entorno.

---

### En una frase completa

```bash
python3 -m venv .venv
```

significa:

> Usa Python 3 para ejecutar el módulo `venv` y crear un entorno virtual dentro de una carpeta llamada `.venv`.

---

## 6.4. Activar el entorno virtual en Mac

```bash
source .venv/bin/activate
```

### Qué hace
Activa el entorno virtual en la terminal actual.

### Cómo sabes que funcionó
Aparece algo como:

```text
(.venv)
```

al inicio de la línea de la terminal.

Ejemplo:

```text
(.venv) ... ARCADE %
```

---

## 6.5. Qué significa `source`

`source` ejecuta un archivo dentro de la terminal actual.

Aquí ejecutamos:

```text
.venv/bin/activate
```

para cambiar temporalmente el entorno que usa la terminal.

---

## 6.6. Desactivar el entorno virtual

```bash
deactivate
```

### Qué hace
Sale del entorno virtual.

### Qué cambia visualmente
Desaparece:

```text
(.venv)
```

de la terminal.

---

## 6.7. Reactivar el entorno cuando vuelvas al proyecto

Cada vez que abras una terminal nueva, puedes activar el entorno de nuevo con:

```bash
source .venv/bin/activate
```

En muchos casos VS Code lo activa automáticamente si seleccionaste correctamente el intérprete, pero conviene saber hacerlo manualmente.

---

# 7. Instalar librerías de Python con `pip`

---

## 7.1. Qué es `pip`

`pip` es el instalador de paquetes de Python.

Sirve para instalar librerías externas como:

- PySide6;
- requests;
- pandas;
- matplotlib;
- pytest.

---

## 7.2. Instalar una librería

Ejemplo usado:

```bash
python -m pip install pyside6
```

### Qué hace
Instala el paquete `PySide6` en el entorno Python activo.

---

## 7.3. Por qué recomiendo `python -m pip`

También existe esta forma:

```bash
pip install pyside6
```

Pero es muy buena práctica usar:

```bash
python -m pip install pyside6
```

### Por qué
Porque así te aseguras de que `pip` pertenece al mismo Python que estás usando.

---

## 7.4. Ver paquetes instalados

```bash
python -m pip list
```

---

## 7.5. Ver información de un paquete

Comando que usamos:

```bash
python -m pip show PySide6
```

### Qué muestra
- nombre;
- versión;
- ubicación;
- dependencias.

### Por qué lo usamos
Para confirmar que `PySide6` quedó instalado dentro del entorno virtual correcto.

---

## 7.6. Actualizar `pip`

A veces conviene actualizarlo:

```bash
python -m pip install --upgrade pip
```

---

## 7.7. Desinstalar una librería

```bash
python -m pip uninstall nombre_del_paquete
```

Ejemplo:

```bash
python -m pip uninstall pyside6
```

---

# 8. Verificaciones útiles de Python y del entorno

---

## 8.1. Saber qué Python está usando la terminal

```bash
which python
```

### Ejemplo de salida esperada con `.venv` activo

```text
/Users/hugo/.../ARCADE/.venv/bin/python
```

### Qué confirma
Que `python` apunta al intérprete del entorno virtual del proyecto.

---

## 8.2. Saber qué `pip` estás usando

```bash
which pip
```

También debería apuntar a `.venv`.

---

## 8.3. Probar si una librería se puede importar

Ejemplo:

```bash
python -c "import PySide6; print('PySide6 quedó instalado correctamente')"
```

Si no aparece error, la librería está disponible.

---

# 9. Seleccionar el intérprete correcto en VS Code

---

## 9.1. Qué es el intérprete

El **intérprete** es la instalación de Python que VS Code usará para:

- ejecutar archivos;
- hacer debugging;
- detectar paquetes;
- autocompletar imports;
- mostrar advertencias.

---

## 9.2. Cómo seleccionarlo

1. Presiona:

```text
Cmd + Shift + P
```

2. Escribe:

```text
Python: Select Interpreter
```

3. Elige el que apunte a:

```text
.venv/bin/python
```

---

## 9.3. Por qué esto importa

Si instalaste `PySide6` en `.venv`, pero VS Code ejecuta otro Python, podrías ver errores como:

```text
ModuleNotFoundError: No module named 'PySide6'
```

aunque la librería sí esté instalada.

---

# 10. Comandos y conceptos básicos de Git

---

## 10.1. Qué es Git

**Git** es un sistema de control de versiones.

Sirve para:

- guardar el historial de cambios;
- volver atrás;
- crear ramas;
- comparar versiones;
- colaborar con otras personas;
- subir cambios a GitHub.

---

## 10.2. Qué es GitHub

**GitHub** es una plataforma en internet donde alojas repositorios Git.

Dicho simple:

- Git = herramienta de historial;
- GitHub = sitio donde guardas y compartes ese historial.

---

# 11. Estados básicos de archivos en Git

En VS Code y Git puedes ver letras como:

- `U` = untracked, archivo nuevo no rastreado aún;
- `M` = modified, archivo modificado;
- `D` = deleted, archivo eliminado.

---

# 12. Comandos básicos de Git

---

## 12.1. `git status`

```bash
git status
```

### Qué hace
Muestra el estado actual del repositorio:

- rama en la que estás;
- archivos modificados;
- archivos nuevos;
- archivos eliminados;
- si hay cambios listos para commit.

---

## 12.2. `git add`

```bash
git add archivo.py
```

### Qué hace
Prepara un archivo para el siguiente commit.

---

## 12.3. Agregar todos los cambios

```bash
git add .
```

### Qué hace
Prepara todos los cambios detectados dentro del proyecto actual.

---

## 12.4. `git commit`

```bash
git commit -m "mensaje del commit"
```

### Qué hace
Guarda una fotografía del estado actual del proyecto en el historial de Git.

---

## 12.5. Ejemplo real de commit

```bash
git commit -m "refactor: reorganize arcade project structure"
```

---

# 13. Cómo escribir buenos mensajes de commit

---

## 13.1. Regla principal

Un commit debería describir **un cambio lógico concreto**.

No:

```text
arreglos
cosas
update
ya casi
```

Sí:

```text
feat: add number guessing game folder structure
fix: correct menu input validation
refactor: split UI and logic modules
docs: add Qt learning guide
```

---

## 13.2. Tipos recomendados

### `feat`
Nueva funcionalidad.

```text
feat: add easy mode to number guessing game
```

### `fix`
Corrección de error.

```text
fix: prevent invalid number input from crashing game
```

### `refactor`
Reorganización interna sin cambiar el comportamiento esperado.

```text
refactor: move shared utilities into utilities package
```

### `docs`
Documentación.

```text
docs: add PySide6 learning notes
```

### `chore`
Tareas de mantenimiento, configuración o limpieza.

```text
chore: configure Python virtual environment ignore rules
```

### `test`
Pruebas.

```text
test: add validation tests for guessing logic
```

---

# 14. Push, pull y sync

---

## 14.1. `git push`

```bash
git push
```

### Qué hace
Sube tus commits locales al repositorio remoto en GitHub.

---

## 14.2. `git pull`

```bash
git pull
```

### Qué hace
Trae a tu computador los cambios que estén en GitHub y no tengas localmente.

---

## 14.3. Sync Changes en VS Code

Cuando presionas **Sync Changes**, VS Code normalmente intenta hacer:

1. pull;
2. push.

Por eso a veces aparece un aviso diciendo que sincronizará cambios con `origin/main`.

---

# 15. Error que vimos: email privacy restrictions

Cuando intentaste hacer push, apareció un error parecido a:

```text
push declined due to email privacy restrictions
```

---

## 15.1. Qué significaba

GitHub rechazó el push porque el commit tenía un correo que chocaba con tu configuración de privacidad.

---

## 15.2. Qué se hizo

Se configura Git para usar un correo permitido por GitHub, normalmente un correo `noreply`.

Ejemplo:

```bash
git config --global user.email "tu_correo_noreply_de_github"
```

---

## 15.3. Ver el email configurado

```bash
git config --global user.email
```

---

## 15.4. Ver el nombre configurado

```bash
git config --global user.name
```

---

## 15.5. Cambiar el nombre de Git

```bash
git config --global user.name "Tu Nombre"
```

---

## 15.6. Corregir el último commit para que use la nueva configuración

```bash
git commit --amend --reset-author
```

### Qué hace
Reescribe el último commit para actualizar el autor según la configuración actual de Git.

---

## 15.7. Después se vuelve a subir

```bash
git push
```

---

# 16. Ramas en Git

---

## 16.1. Qué es una rama

Una **rama** es una línea de trabajo separada dentro del mismo proyecto.

Sirve para desarrollar algo nuevo sin afectar directamente la versión principal.

---

## 16.2. Rama principal

Normalmente se llama:

```text
main
```

---

## 16.3. Idea importante

Una rama no tiene por qué representar un juego para siempre.

Es mejor que represente:

> Un cambio en desarrollo que todavía no quieres integrar a `main`.

---

## 16.4. Ejemplos de nombres de ramas

```text
feature/adivina-el-numero
feature/menu-principal
fix/error-en-buscaminas
refactor/ui-ahorcadito
docs/comandos-y-entorno
```

---

## 16.5. Crear una rama

```bash
git branch nombre-de-la-rama
```

Ejemplo:

```bash
git branch feature/adivina-el-numero
```

---

## 16.6. Cambiar a una rama

```bash
git switch nombre-de-la-rama
```

Ejemplo:

```bash
git switch feature/adivina-el-numero
```

---

## 16.7. Crear y cambiar de rama en un solo comando

```bash
git switch -c feature/adivina-el-numero
```

Este comando:

1. crea la rama;
2. entra a ella inmediatamente.

---

## 16.8. Ver ramas disponibles

```bash
git branch
```

La rama activa aparece marcada con `*`.

---

## 16.9. Volver a `main`

```bash
git switch main
```

---

# 17. Comandos de Git útiles para consultar historial

---

## 17.1. Ver historial simple

```bash
git log --oneline
```

### Ejemplo

```text
6d668aa refactor: reorganize project structure
12ab431 feat: add initial arcade files
```

---

## 17.2. Ver historial más visual con ramas

```bash
git log --oneline --graph --all
```

Sirve para entender cómo se ramifica el proyecto.

---

# 18. Archivos que suelen agregarse al proyecto

---

## 18.1. `.gitignore`

Es un archivo que le dice a Git qué cosas **no debe subir**.

En proyectos Python suele contener, por ejemplo:

```text
.venv/
__pycache__/
.DS_Store
```

---

## 18.2. Por qué no subir `.venv`

La carpeta `.venv` puede ser muy pesada y se puede reconstruir en cualquier computador instalando las dependencias.

Por eso normalmente se ignora.

---

## 18.3. Verificar si tienes `.gitignore`

En la raíz del proyecto puedes mirar si existe:

```text
.gitignore
```

Si no está, más adelante conviene crearlo.

---

# 19. Comandos que sirven mucho en macOS mientras programas

---

## 19.1. Abrir la carpeta actual en Finder

```bash
open .
```

### Qué hace
Abre en Finder la carpeta en la que estás parado desde la terminal.

---

## 19.2. Abrir un archivo o carpeta

```bash
open nombre_del_archivo
```

Ejemplo:

```bash
open README.md
```

---

# 20. Tabla-resumen de comandos frecuentes

| Comando | Para qué sirve |
|---|---|
| `pwd` | Ver carpeta actual |
| `ls` | Listar archivos |
| `ls -a` | Ver también archivos ocultos |
| `cd carpeta` | Entrar a una carpeta |
| `cd ..` | Subir un nivel |
| `clear` | Limpiar terminal |
| `python3 --version` | Ver versión de Python |
| `python archivo.py` | Ejecutar archivo Python |
| `python3 -m venv .venv` | Crear entorno virtual |
| `source .venv/bin/activate` | Activar entorno virtual |
| `deactivate` | Salir del entorno virtual |
| `python -m pip install paquete` | Instalar paquete |
| `python -m pip list` | Ver paquetes instalados |
| `python -m pip show paquete` | Ver detalles de un paquete |
| `which python` | Ver qué Python usa la terminal |
| `which pip` | Ver qué pip usa la terminal |
| `git status` | Ver estado del repo |
| `git add .` | Preparar todos los cambios |
| `git commit -m "mensaje"` | Crear commit |
| `git push` | Subir commits a GitHub |
| `git pull` | Traer cambios de GitHub |
| `git branch` | Ver ramas |
| `git switch -c rama` | Crear y cambiar a una rama |
| `git switch main` | Volver a rama principal |
| `git log --oneline` | Ver historial resumido |

---

# 21. Flujo recomendado al trabajar en tu proyecto

Cuando abras el proyecto en otro momento:

1. Abre `ARCADE` en VS Code.
2. Abre la terminal integrada.
3. Verifica carpeta si hace falta:

```bash
pwd
```

4. Activa el entorno virtual si no se activó solo:

```bash
source .venv/bin/activate
```

5. Mira el estado de Git:

```bash
git status
```

6. Programa con calma.
7. Cuando completes un cambio lógico:
   - revisa archivos;
   - haz commit;
   - sube a GitHub.

---

# 22. Flujo recomendado para instalar una nueva librería

1. Activa `.venv`.
2. Instala con:

```bash
python -m pip install nombre_paquete
```

3. Verifica que quedó instalada:

```bash
python -m pip show nombre_paquete
```

4. Si el proyecto depende de ella, más adelante conviene registrar dependencias en un `requirements.txt`.

---

# 23. Comando útil para guardar dependencias en `requirements.txt`

Cuando ya tengas librerías instaladas y quieras registrarlas:

```bash
python -m pip freeze > requirements.txt
```

### Qué hace
Crea o reemplaza un archivo `requirements.txt` con la lista exacta de paquetes instalados en el entorno.

---

## 23.1. Instalar dependencias desde `requirements.txt`

En otro computador o entorno:

```bash
python -m pip install -r requirements.txt
```

### Qué hace
Instala todos los paquetes listados en ese archivo.

---

# 24. Nota importante sobre aprender comandos

No necesitas memorizar todo de golpe.

El objetivo es:

1. entender qué hace cada comando;
2. usarlo varias veces;
3. volver a esta guía cuando se te olvide.

Con la práctica, los más importantes se te vuelven naturales:

```bash
pwd
cd
ls
source .venv/bin/activate
python main.py
git status
git add .
git commit -m "..."
git push
```

---

# 25. Cierre

Con lo que ya hiciste, dejaste preparado un entorno serio para programar:

- proyecto abierto en VS Code;
- terminal usada correctamente;
- entorno virtual creado;
- PySide6 instalado;
- VS Code usando el Python correcto;
- Git funcionando;
- commits mejor estructurados;
- base para trabajar con ramas y documentación.

Esta guía debe servir como tu “manual de supervivencia” inicial para trabajar en Python, Qt y Git sin perderte en lo básico.
