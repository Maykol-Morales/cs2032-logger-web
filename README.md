# cs2032-logger-web

> Proyecto del curso **CS2032 – Cloud Computing** · UTEC

Visor web para los archivos de log generados por [**utec-logger**](https://github.com/Maykol-Morales/cs2032-logger). Lee los `.log` al momento del build y genera un sitio estático para explorarlos y filtrarlos.

## Funcionalidades

- Vista con todos los logs, ordenados del más reciente al más antiguo
- Una página por archivo de origen (por ejemplo `/app-py` para `app.py`)
- Filtros por nivel, mensaje, archivo de origen, fecha y hora
- Tolera líneas con formato inválido (las omite y avisa en el build)

## Formato esperado

Cada línea del log debe seguir el formato de utec-logger:

```
2025-05-03 12:30:01.123 | INFO | main.py:23 | Mensaje
```

## Stack

- Gatsby 5 · React 18
- Tailwind CSS 3 · lucide-react
- Docker

## Configuración

| Variable | Por defecto | Descripción |
|---|---|---|
| `LOGS_DIR` | `./logs` | Carpeta con los archivos `.log` |
| `MAX_LOGS_PER_FILE` | `10000` | Máximo de líneas a procesar por archivo |

## Desarrollo

Requiere **Node 20** (ver `.nvmrc`); Gatsby 5 no compila con versiones recientes de Node.

```bash
npm install
LOGS_DIR=/ruta/a/logs npm run develop   # http://localhost:8000
LOGS_DIR=/ruta/a/logs npm run build     # genera public/
```

## Docker

El contenedor construye el sitio al iniciar, así que toma los logs presentes en ese momento:

```bash
docker build -t cs2032-logger-web .
docker run -d -p 3000:3000 -e LOGS_DIR=/logs -v /home/ubuntu/logs:/logs cs2032-logger-web
# http://localhost:3000
```

## Estructura

```
gatsby-node.js          # Lee y parsea los .log, crea las páginas
src/
├── components/         # TopBar, LogFilter
├── templates/logger.js # Página de logs
└── pages/404.js
```

## Proyectos relacionados

- [cs2032-logger](https://github.com/Maykol-Morales/cs2032-logger) — librería `utec-logger` (PyPI)
- [Documentación](https://utec-logger.github.io)

## Autores

Gino Daza y Maykol Morales
