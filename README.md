# Practicas_Sistemas-Digitales
# Guía de Entorno Colaborativo local: VS Code + Git + LaTeX

Este repositorio contiene nuestro entorno de desarrollo para los reportes de laboratorio de la asignatura (como la implementación de circuitos lógicos). Hemos migrado de Overleaf a un flujo de trabajo estándar en ingeniería de software para eliminar los límites de compilación, restricciones de colaboradores y depender del almacenamiento en la nube, utilizando Git para el control de versiones asíncrono y Live Share para sesiones en tiempo real.

---

## 🛠️ Fase 1: Prerrequisitos del Sistema (Instalar una sola vez)

Estas tres herramientas conforman el "motor" que procesará nuestros documentos localmente.

1. **[MiKTeX](https://miktex.org/download?utm_source=gemini)**: Es el compilador de LaTeX.
* **CRÍTICO:** Durante la instalación, llegarás a una opción llamada *"Install missing packages on-the-fly"*. Debes cambiarla obligatoriamente de "Ask me first" a **"Yes"**. Esto permite descargar dependencias automáticamente como lo hace Overleaf.


2. **[Strawberry Perl](https://strawberryperl.com/?utm_source=gemini)**: Motor necesario para que las extensiones formateen y ordenen nuestro código automáticamente.
* **CRÍTICO:** Debes reiniciar tu computadora después de instalar esto para que Windows actualice las variables de entorno.


3. **[Git](https://www.google.com/search?q=https://git-scm.com/downloads&utm_source=gemini)**: El sistema de control de versiones. Instálalo dejando todas las opciones por defecto que marque el instalador.

## 💻 Fase 2: Configuración del Entorno de Desarrollo (VS Code)

Utilizaremos Visual Studio Code como nuestro editor principal. Una vez instalado, ve a la pestaña de **Extensiones** (`Ctrl+Shift+X`) e instala estrictamente estas tres:

* **LaTeX Workshop** (por James Yu): Habilita la compilación (`Ctrl+Alt+B`) y el visor de PDF integrado.
* **GitHub Pull Requests and Issues** (por GitHub): Facilita iniciar sesión y vincular tu cuenta.
* **Live Share** (por Microsoft): Permite la edición simultánea en tiempo real.

## 👤 Fase 3: Registro de Identidad en Git

Antes de guardar cualquier cambio en el historial del proyecto, Git exige saber quién eres. Abre una terminal dentro de VS Code (`Terminal > New Terminal` o `Ctrl+ñ`) y ejecuta los siguientes comandos.

> **⚠️ Nota para equipos compartidos:** Si estamos usando la misma laptop (por ejemplo, turnándonos en la sesión) **NO uses la palabra `--global**` en estos comandos. Escríbelos exactamente como están abajo para que tu identidad solo afecte a esta carpeta de *Sistemas Digitales* y no sobrescriba las configuraciones de los repositorios personales del dueño del equipo.

```bash
git config user.name "Tu Nombre Completo"
git config user.email "aXXXXXXXX@alumnos.uady.mx"

```

*(Usa el mismo correo con el que registraste tu cuenta de GitHub).*

## 📥 Fase 4: Descargar el Repositorio

Para obtener los archivos de la plantilla base IEEEtran a tu computadora:

1. Presiona `F1` en VS Code.
2. Escribe **Git: Clone** y selecciona la opción.
3. Pega la URL HTTPS de este repositorio de GitHub.
4. Selecciona una carpeta en tu computadora donde guardarás la materia y haz clic en "Open" cuando pregunte si deseas abrir el proyecto clonado.

---

## 🔄 Fase 5: El Flujo de Trabajo Asíncrono (Regla de Oro)

A diferencia de la nube, en Git el trabajo individual no se refleja automáticamente en la pantalla de los demás. Para evitar **Merge Conflicts** (donde dos personas editan la misma línea y el código choca), sigan este ciclo en cada sesión individual:

1. **Sincronizar (Pull):** Antes de modificar cualquier archivo, ve al panel de *Source Control* (el ícono de la rama a la izquierda) y presiona **Sync Changes** (o ejecuta `git pull`). Esto descarga lo que los demás hicieron mientras no estabas.
2. **Editar y Compilar:** Escribe el código en `main.tex`. Usa `Ctrl+Alt+B` para compilar y ver el PDF.
3. **Empaquetar (Commit):** Al terminar tu sección, ve a *Source Control*. En la caja de texto *"Message"*, escribe un resumen claro de lo que hiciste (ej. *"Se agregó la tabla de verdad del sumador"*). Haz clic en el botón azul **Commit**.
4. **Subir (Push):** Haz clic nuevamente en **Sync Changes** para subir tu Commit a GitHub.

### 🚫 Regla Estricta del Repositorio

**NUNCA hagan commit de archivos autogenerados por LaTeX (`.pdf`, `.aux`, `.log`, `.synctex.gz`).**
MiKTeX los sobrescribe cada vez que compilamos. Si los subimos, Git detectará colisiones masivas cada 5 minutos. El proyecto ya cuenta con un archivo `.gitignore` configurado para ocultar estos archivos, por favor no lo modifiquen. Solo se sube el código fuente (`.tex`) y las imágenes (`.png`, `.jpg`) de los circuitos.

---

## 🤝 Fase 6: Colaboración en Tiempo Real (Live Share)

Para cuando nos reunamos en Discord o Teams a redactar juntos de forma simultánea.

1. **Crear la sala (El Anfitrión):** Quien tenga el proyecto abierto y sincronizado, hace clic en el botón **Live Share** (barra inferior azul). Esto copia un link al portapapeles.
2. **Unirse (Los Invitados):** Los demás presionan `Ctrl+Shift+P`, escriben `Live Share: Join`, pegan el link y entrarán al documento viendo los cursores de todos.

**Protocolo para Live Share:**

* **Solo el anfitrión compila:** Como estamos escribiendo remotamente en el disco duro del anfitrión, su motor MiKTeX es el que procesa todo. El anfitrión compila (`Ctrl+Alt+B`) y comparte la pantalla del PDF en la llamada.
* **Solo el anfitrión guarda en Git:** Los invitados no tocan la pestaña de *Source Control*. Al terminar la llamada, el anfitrión hace un único Commit/Push englobando el trabajo de toda la sesión conjunta.
