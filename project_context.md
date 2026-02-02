# Contexto del Proyecto ITAM

## Resumen Ejecutivo

**Objetivo**: Desarrollar un sistema de gestión de activos de TI (ITAM) ligero para gestionar 1,800 líneas telefónicas corporativas de "The Home Depot".
**Meta**: MVP funcional, limpio y escalable en un plazo de 3 meses.
**Estado Actual**: Fase de Inicialización (Estructura, Base de Datos y Servidor Básico creados).

## Stack Tecnológico

- **Backend**: Node.js v20+ con Express.
- **ORM**: Prisma.
- **Base de Datos**: SQLite (archivo local `dev.db`).
- **Lenguaje**: JavaScript (ES6+).
- **Herramientas Adicionales**: `dotenv`, `cors`, `multer` (para carga de archivos), `xlsx` (procesamiento de Excel).

## Arquitectura de Datos: Patrón "Service Slot"

El sistema evita usar el IMEI o número telefónico como llave primaria. En su lugar, implementa el patrón **Service Slot**:

- **Inmutabilidad**: El `ServiceSlot` es una entidad lógica persistente (con UUID) que representa "un espacio de servicio asignable".
- **Mutabilidad**: Los dispositivos (IMEI) y líneas (Teléfono) entran y salen de este slot, pero el slot mantiene su identidad e historia.

### Diccionario de Datos (Schema Actual)

#### 1. Employee (Catálogo de RRHH)

Representa a los usuarios finales de los dispositivos.

- **PK**: `numero_empleado` (String) - ID real de la empresa.
- **Datos**: `nombre_completo`, `puesto`, `centro_costos`, `ubicacion`, `email`.
- **Estatus**: `estatus_rh` ("ACTIVO", "BAJA", etc).

#### 2. ServiceSlot (Entidad Central)

La "Verdad Única" que une hardware y línea.

- **PK**: `id` (UUID).
- **Relaciones**: `empleado` (FK).
- **Hardware**: `imei`, `marca`, `modelo`, `numero_serie` + Datos MDM (`mdm_last_seen`, `mdm_compliance`).
- **Línea**: `telefono`, `sim_card`, `plan_telcel`, `renta_mensual`.
- **Ciclo de Vida**:
  - `fecha_asignacion`, `fecha_inicio_plan`, `fecha_fin_plan`.
  - `estatus` ("ASIGNADO", "DISPONIBLE", "MANTENIMIENTO", "BAJA_PENDIENTE", "ROBADO").

#### 3. AuditLog (Historial)

Registro inmutable de cambios automáticos.

- **PK**: `id` (Int, Autoincremental).
- **Datos**: `slot_id`, `accion`, `campo_afectado`, `valor_anterior`, `valor_nuevo`, `usuario_responsable`, `motivo`.

## Estructura del Proyecto

```
w:\ITAM\
├── src\
│   ├── config\         # Configuración (DB, Env)
│   ├── controllers\    # Lógica de endpoints
│   ├── middlewares\    # Validaciones, Auth
│   ├── routes\         # Definición de rutas API
│   ├── services\       # Lógica de negocio compleja
│   └── utils\          # Helpers
├── prisma\
│   ├── schema.prisma   # Definición de modelos
│   └── dev.db          # Base de datos SQLite
├── public\             # Archivos estáticos
├── .env                # Variables de entorno
└── server.js           # Punto de entrada
```

## Próximos Pasos Recomendados

1.  **Sincronización DB**: Ejecutar `npx prisma db push` para aplicar los últimos cambios del schema manual.
2.  **Seed de Datos**: Crear scripts para cargar empleados de prueba.
3.  **API Endpoints**: Desarrollar CRUD para `ServiceSlot`.
