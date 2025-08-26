0) Requisitos previos

Cuenta en Neon (puedes registrarte con correo, GitHub o Google). 
Neon

(Opcional, para CLI) Node.js + neonctl o Homebrew para instalar la Neon CLI. Ej.: npm i -g neonctl o brew install neonctl. 
Neon
GitHub

1) Crear cuenta y proyecto en Neon (UI)

Regístrate en Neon Console (Sign up). Después del onboarding crea un Project (es el contenedor que agrupa branches, databases y roles). 
Neon

Durante la creación eliges nombre, región y versión de Postgres (Neon soporta PostgreSQL 14–17). 
Neon

Consejo: crea 1 proyecto por repo/aplicación para que las branches reflejen tus ramas de código. 
Neon

2) Invitar al equipo (Organization / Project)

Para que TODOS trabajen en la misma base de datos, crea (o usa) una Organization y invita a los miembros por email desde el panel de la consola o mediante la API de Neon (endpoint para crear invitaciones). También puedes crear project-scoped API keys para dar acceso limitado a un proyecto. No compartas keys personales; usa keys de proyecto/organización. 
Neon
Neon

3) Flujo recomendado: Branch por desarrollador

Neon permite crear branches (copias aisladas y casi instantáneas de la base de datos). Recomendación práctica para equipos:

Mantén production (root) para producción.

Crea una branch por desarrollador (ej. dev-juan, dev-maria) o una branch por feature/PR. Cada branch es aislada; los cambios no afectan a producción. 
Neon
+1

Crear branch (Consola): Proyecto → Branches → New branch → elegir nombre / punto en el tiempo / expiración → Create. 
Neon

Crear branch (CLI):

neon auth                 # inicia auth en navegador
neon branches create --name dev-juan
neon branches list


(La CLI soporta --name para nombrar la branch; después obtienes la connection string). 
Neon
+1

Nota: por defecto una branch hereda roles y passwords del parent; si quieres que la branch tenga passwords nuevas habilita protección/otras opciones. 
Neon

4) Obtener la connection string (Consola o CLI)

Consola: en el Project Dashboard haz clic en Connect → selecciona branch, compute, database y role → copia la connection string. Neon ofrece por defecto pooled connection strings (añade -pooler al host). 
Neon

CLI: usa neon connection-string <branch> o neon connection-string --pooled para obtenerla desde terminal. Ejemplos y opciones en la docs (puedes pedir --psql para abrir psql directamente). 
Neon
+1

Ejemplo de connection string (formato):

postgresql://usuario:Password123@ep-cool-darkness-123456-pooler.us-east-2.aws.neon.tech/dbname?sslmode=require&channel_binding=require


Neon requiere SSL/TLS y por defecto incluye sslmode=require. 
Neon
+1

5) Opciones para que todos usen la BD sin conflictos
Opción A — Branch por desarrollador (recomendada)

Cada dev usa su branch (con su connection string). Así pueden experimentar y resetear su branch sin afectar a otros. Usar Neon Local Connect (VSCode ext.) permite mapear cualquier branch a localhost:5432 y no tener que cambiar DATABASE_URL cuando se cambia de branch. 
Neon
+1

Opción B — Branch compartida para staging / QA

Tener una branch staging que varios testers usen. Para evitar sobrecarga usa el pooler (p. ej. con la connection string pooled). 
Neon

Opción C — Base de datos central en la nube (single DB)

Todos se conectan a la misma branch/compute (menos aislamiento; riesgo de conflictos). Si la usas, crea roles/usuarios específicos y controla acceso con API keys / IP allow. 
Neon
+1

6) Cómo poner la connection string en tu proyecto FastAPI

Copia la conn string desde Neon (Consola o CLI). 
Neon

Guarda en .env (no subir a Git):

DATABASE_URL="postgresql://user:Pass123@ep-...-pooler.us-east-2.aws.neon.tech/dbname?sslmode=require&channel_binding=require"


Ejemplo app/database.py (SQLAlchemy sync):

import os
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, declarative_base

DATABASE_URL = os.getenv("DATABASE_URL")

engine = create_engine(DATABASE_URL, pool_pre_ping=True)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
Base = declarative_base()

https://www.youtube.com/watch?v=7KglfRnIlfc