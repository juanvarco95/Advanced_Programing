🐍 Guía para crear un entorno en Python
📌 ¿Qué es un entorno virtual?

Un entorno virtual en Python es un espacio aislado donde puedes instalar librerías específicas para un proyecto, sin afectar a otros proyectos o a la instalación global de Python.

1️⃣ Verificar instalación de Python

Primero asegúrate de que Python está instalado:

python --version


o en algunos sistemas:

python3 --version

2️⃣ Crear un entorno virtual

En la carpeta de tu proyecto, ejecuta:

python -m venv venv


👉 Aquí, venv es el nombre del entorno. Puedes cambiarlo por otro nombre como env o myenv.

3️⃣ Activar el entorno

Dependiendo del sistema operativo:

Windows (CMD o PowerShell):

venv\Scripts\activate


Linux / MacOS:

source venv/bin/activate


Si la activación fue correcta, en la terminal verás algo así:

(venv) tu-usuario:~/proyecto$

4️⃣ Instalar librerías dentro del entorno

Con el entorno activo, instala las librerías necesarias. Ejemplo:

pip install fastapi uvicorn requests

5️⃣ Guardar dependencias

Para compartir tu proyecto o recrear el entorno en otra máquina:

pip freeze > requirements.txt


Esto genera un archivo requirements.txt con todas las librerías y versiones.

6️⃣ Instalar dependencias desde requirements.txt

En otra computadora (o después de clonar un proyecto):

pip install -r requirements.txt

7️⃣ Desactivar el entorno

Cuando termines de trabajar:

deactivate

✅ Buenas prácticas

Crea un entorno virtual por cada proyecto.

Usa requirements.txt para mantener el control de versiones.

Evita instalar librerías globalmente, así mantienes tu sistema limpio.