🐬 Guía paso a paso: MySQL en la nube con PlanetScale + Laravel
1️⃣ Crear cuenta en PlanetScale

Ve a 👉 https://planetscale.com

Regístrate con GitHub o Google.

Desde el dashboard, haz clic en Create a database.

2️⃣ Configurar la base de datos

Dale un nombre a tu DB, por ejemplo: parkingdb.

Selecciona una región (elige la más cercana a tu país, por ejemplo, US East).

Haz clic en Create Database.

3️⃣ Obtener las credenciales de conexión

En la nueva base de datos, ve a la pestaña Connect.

Elige Laravel como framework.

PlanetScale te mostrará algo como:

DB_CONNECTION=mysql
DB_HOST=aws.connect.psdb.cloud
DB_PORT=3306
DB_DATABASE=parkingdb
DB_USERNAME=xxxx
DB_PASSWORD=yyyy


⚠️ Ojo: PlanetScale usa SSL, así que también necesitarás agregar en tu .env de Laravel:

DB_SSL_MODE=prefer
DB_SSL_CERT=/ruta/al/certificado.pem


Pero normalmente Laravel funciona solo con las variables que ellos te dan.

4️⃣ Configurar .env en Laravel

En tu proyecto Laravel, abre el archivo .env y reemplaza la sección de DB por lo que te dio PlanetScale:

DB_CONNECTION=mysql
DB_HOST=aws.connect.psdb.cloud
DB_PORT=3306
DB_DATABASE=parkingdb
DB_USERNAME=tu_usuario
DB_PASSWORD=tu_password

5️⃣ Migrar la base de datos

Ahora, en tu terminal:

php artisan migrate


Esto creará tus tablas en la base de datos en PlanetScale 🚀

6️⃣ Verificar conexión

Puedes usar phpMyAdmin local o clientes como TablePlus, Beekeeper Studio o DBeaver para conectarte a PlanetScale usando las credenciales.

https://www.youtube.com/watch?v=OCelTHywUpQ