# ITAM System - The Home Depot

Sistema ligero de Gestión de Activos de TI (ITAM) diseñado para administrar 1,800 líneas telefónicas corporativas. Implementa el patrón **Service Slot** para garantizar la trazabilidad inmutable de los activos.

## 🚀 Inicio Rápido

### Requisitos Previos

- Node.js (v20 o superior recomendado)
- npm

### Instalación

1. Clona o descarga el repositorio.
2. Instala las dependencias:
   ```bash
   npm install
   ```
3. Configura las variables de entorno en el archivo `.env`:
   ```env
   PORT=3000
   DATABASE_URL="file:./dev.db"
   ```
4. Inicializa la base de datos y genera el cliente Prisma:
   ```bash
   npm run prisma:push
   npm run prisma:generate
   ```

### Ejecución

- **Modo Desarrollo**: `npm run dev` (reinicia automáticamente con cambios).
- **Modo Producción**: `npm start`.

---

## 🛠️ Stack Tecnológico

- **Backend**: Node.js & Express
- **ORM**: Prisma
- **Base de Datos**: SQLite (Local)
- **Utilidades**: CORS, Dotenv, Multer, XLSX

---

## 📂 Estructura del Proyecto

```
/
├── prisma/             # Schema de base de datos y migraciones
├── src/
│   ├── config/         # Configuraciones globales
│   ├── controllers/    # Controladores de la API
│   ├── middlewares/    # Middlewares de Express
│   ├── routes/         # Definición de rutas (Endpoints)
│   ├── services/       # Lógica de negocio
│   └── utils/          # Funciones de ayuda
├── server.js           # Punto de entrada de la aplicación
└── project_context.md  # Documentación detallada del contexto
```

---

## 📜 Scripts Disponibles

- `npm start`: Inicia el servidor.
- `npm run dev`: Inicia el servidor en modo observación (watch mode).
- `npm run prisma:generate`: Genera el cliente Prisma.
- `npm run prisma:push`: Sincroniza el schema con la base de datos local.
- `npm run prisma:studio`: Abre una interfaz web para explorar la base de datos.

---

## 📝 Documentación Adicional

Para una explicación detallada del modelo de datos y la arquitectura "Service Slot", consulta el archivo:
👉 [**project_context.md**](./project_context.md)
