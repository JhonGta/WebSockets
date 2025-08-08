# Sistema de Gestión de Laboratorios

Sistema universitario para el control y registro del uso de laboratorios, desarrollado con Next.js, Node.js, Express y Sequelize.

## 🚀 Características

- **Arquitectura Full Stack**: Frontend Next.js + Backend Node.js/Express
- **Arquitectura Limpia**: Separación por capas (Models, Repositories, Services, Controllers)
- **Base de Datos**: PostgreSQL con Sequelize ORM
- **API RESTful**: Endpoints completos para todas las operaciones
- **Manejo de Errores**: Sistema robusto de manejo de excepciones
- **Docker**: Configuración lista para desarrollo
- **Validaciones**: Validación de datos en todos los niveles

## 📋 Requisitos Previos

- Node.js >= 16.0.0
- Docker y Docker Compose
- PostgreSQL (si no usas Docker)

## 🛠️ Instalación

1. **Clonar el repositorio**

   ```bash
   git clone https://github.com/fabianpd19/gestion_laboratorios.git
   cd gestion_laboratorios
   ```

2. **Instalar dependencias**

   ```bash
   npm install
   ```

3. **Configurar variables de entorno**

   ```bash
   cp .env.example .env
   # Editar .env con tus configuraciones
   ```

4. **Levantar base de datos con Docker**

   ```bash
   npm run db:setup
   ```

5. **Aplicar Migraciones**

   ```bash
   #Una vez levantado el contenedor:
   npx sequelize-cli db:migrate
   ```

6. **Iniciar el sistema**

   **Opción 1: Desarrollo completo (recomendado)**

   ```bash
   # Terminal 1: Backend en puerto 3001
   npm run backend:dev

   # Terminal 2: Frontend en puerto 3000
   npm run dev
   ```

   **Opción 2: Solo backend**

   ```bash
   npm run dev:backend-only
   ```

   **Opción 3: Solo frontend**

   ```bash
   npm run dev:frontend-only
   ```

## 🌐 Acceso a la aplicación

- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:3001
- **pgAdmin**: http://localhost:8080
  - Email: admin@lab.com
  - Password: admin123

## 🏗️ Estructura del Proyecto

```
gestion_laboratorios/
├── src/                         # Backend
│   ├── models/                  # Modelos de Sequelize
│   │   ├── usuario.model.js
│   │   ├── laboratorio.model.js
│   │   └── usoLaboratorio.model.js
│   ├── repositories/            # Acceso a datos
│   │   ├── usuario.repository.js
│   │   ├── laboratorio.repository.js
│   │   └── usoLaboratorio.repository.js
│   ├── services/                # Lógica de negocio
│   │   ├── usuario.service.js
│   │   ├── laboratorio.service.js
│   │   └── usoLaboratorio.service.js
│   ├── controllers/             # Controladores HTTP
│   │   ├── usuario.controller.js
│   │   ├── laboratorio.controller.js
│   │   └── usoLaboratorio.controller.js
│   ├── routes/                  # Rutas API
│   │   ├── usuario.routes.js
│   │   ├── laboratorio.routes.js
│   │   └── usoLaboratorio.routes.js
│   └── index.js                 # Servidor principal
├── pages/                       # Frontend Next.js
├── components/                  # Componentes React
├── config/
│   └── db.js                    # Configuración de base de datos
├── utils/
│   └── errorHandler.js          # Manejo global de errores
├── docker-compose.yml           # Configuración Docker
├── .env.example                 # Variables de entorno ejemplo
└── package.json
```

## 📚 API Endpoints

### Usuarios

- `POST /api/usuarios` - Crear usuario
- `GET /api/usuarios` - Obtener todos los usuarios
- `GET /api/usuarios/:id` - Obtener usuario por ID
- `PUT /api/usuarios/:id` - Actualizar usuario
- `DELETE /api/usuarios/:id` - Eliminar usuario
- `POST /api/usuarios/auth` - Autenticar usuario
- `GET /api/usuarios/estadisticas` - Estadísticas de usuarios

### Laboratorios

- `POST /api/laboratorios` - Crear laboratorio
- `GET /api/laboratorios` - Obtener todos los laboratorios
- `GET /api/laboratorios/:id` - Obtener laboratorio por ID
- `PUT /api/laboratorios/:id` - Actualizar laboratorio
- `DELETE /api/laboratorios/:id` - Eliminar laboratorio
- `GET /api/laboratorios/disponibles` - Obtener laboratorios disponibles

### Usos de Laboratorio

- `POST /api/usos` - Registrar uso de laboratorio
- `GET /api/usos` - Obtener todos los usos
- `GET /api/usos/:id` - Obtener uso por ID
- `PUT /api/usos/:id` - Actualizar uso
- `DELETE /api/usos/:id` - Eliminar uso
- `PATCH /api/usos/:id/iniciar` - Iniciar uso
- `PATCH /api/usos/:id/finalizar` - Finalizar uso
- `GET /api/usos/reporte` - Generar reporte
- `GET /api/usos/laboratorio/:laboratorioId/historial` - Historial por laboratorio

## 🧪 Ejemplos de Uso

### Crear Usuario

```bash
curl -X POST http://localhost:3001/api/usuarios \
  -H "Content-Type: application/json" \
  -d '{
    "nombre": "Juan Pérez",
    "email": "juan@universidad.edu",
    "password": "123456",
    "rol": "docente",
    "programa_academico": "Ingeniería de Sistemas"
  }'
```

### Crear Laboratorio

```bash
curl -X POST http://localhost:3001/api/laboratorios \
  -H "Content-Type: application/json" \
  -d '{
    "nombre": "Laboratorio de Química",
    "codigo": "LAB-QUI-01",
    "ubicacion": "Edificio A, Piso 2",
    "capacidad_maxima": 25,
    "tipo_laboratorio": "quimica",
    "equipos_disponibles": ["Microscopio", "Balanza", "pH metro"]
  }'
```

### Registrar Uso

```bash
curl -X POST http://localhost:3001/api/usos \
  -H "Content-Type: application/json" \
  -d '{
    "usuario_id": "uuid-del-usuario",
    "laboratorio_id": "uuid-del-laboratorio",
    "fecha_inicio": "2024-01-20T08:00:00Z",
    "proposito": "Práctica de síntesis orgánica",
    "asignatura": "Química Orgánica",
    "numero_estudiantes": 20,
    "equipos_utilizados": ["Microscopio", "Balanza"]
  }'
```

## 🐳 Docker

### Comandos disponibles

```bash
# Levantar servicios de base de datos
npm run db:setup

# Ver logs de los contenedores
docker-compose logs -f

# Parar servicios
npm run db:down

# Reset completo (elimina volúmenes)
npm run db:reset
```

### Servicios incluidos

- PostgreSQL (puerto 5432)
- pgAdmin (puerto 8080)

## 📋 Scripts NPM Disponibles

### Desarrollo

```bash
# Frontend Next.js (puerto 3000)
npm run dev

# Backend Node.js (puerto 3001)
npm run backend:dev

# Desarrollo completo (ambos servidores)
npm run dev:full

# Solo backend con BD
npm run dev:backend-only

# Solo frontend
npm run dev:frontend-only
```

### Producción

```bash
# Build del frontend
npm run build

# Iniciar frontend en producción
npm run start

# Iniciar backend en producción
npm run backend:start
```

### Base de datos

```bash
# Configurar BD con Docker
npm run db:setup

# Detener BD
npm run db:down

# Reset completo de BD
npm run db:reset
```

### Calidad de código

```bash
# Ejecutar linter
npm run lint
```

## 🧪 Testing

### Ejecutar pruebas

```bash
npm test
```

### Probar endpoints con curl

```bash
# Health check
curl http://localhost:3001/health

# Obtener usuarios
curl http://localhost:3001/api/usuarios

# Obtener laboratorios
curl http://localhost:3001/api/laboratorios
```

## 📊 Modelos de Datos

### Usuario

- `id`: UUID (Primary Key)
- `nombre`: String (100 chars)
- `email`: String único (150 chars)
- `password`: String encriptado
- `rol`: Enum (estudiante, docente, jefe_laboratorio)
- `codigo_estudiante`: String opcional
- `programa_academico`: String opcional
- `telefono`: String opcional
- `activo`: Boolean
- `created_at`: DateTime
- `updated_at`: DateTime

### Laboratorio

- `id`: UUID (Primary Key)
- `nombre`: String (100 chars)
- `codigo`: String único (20 chars)
- `ubicacion`: String (200 chars)
- `capacidad_maxima`: Integer
- `tipo_laboratorio`: Enum (quimica, fisica, biologia, computacion, electronica)
- `equipos_disponibles`: JSON Array
- `horario_disponible`: JSON Object
- `activo`: Boolean
- `observaciones`: Text
- `created_at`: DateTime
- `updated_at`: DateTime

### UsoLaboratorio

- `id`: UUID (Primary Key)
- `usuario_id`: UUID (Foreign Key → Usuario)
- `laboratorio_id`: UUID (Foreign Key → Laboratorio)
- `fecha_inicio`: DateTime
- `fecha_fin`: DateTime opcional
- `proposito`: String (200 chars)
- `asignatura`: String opcional
- `numero_estudiantes`: Integer
- `equipos_utilizados`: JSON Array
- `observaciones`: Text opcional
- `estado`: Enum (programado, en_curso, finalizado, cancelado)
- `calificacion`: Integer (1-5) opcional
- `comentarios_finales`: Text opcional
- `created_at`: DateTime
- `updated_at`: DateTime

## 🔧 Configuración de Desarrollo

### Variables de Entorno

```env
# Base de datos
DATABASE_URL=postgresql://lab_user:lab_password@localhost:5432/laboratorios_db
DB_HOST=localhost
DB_PORT=5432
DB_NAME=laboratorios_db
DB_USER=lab_user
DB_PASSWORD=lab_password

# Servidor
NODE_ENV=development
PORT=3001

# Autenticación (próximamente)
JWT_SECRET=tu_jwt_secret_muy_seguro_aqui

# Next.js
NEXT_PUBLIC_API_URL=http://localhost:3001
```

## 🚨 Manejo de Errores

El sistema implementa un manejo robusto de errores:

- **Errores de Validación**: Campos requeridos, formatos inválidos
- **Errores de Base de Datos**: Duplicados, referencias inexistentes
- **Errores de Negocio**: Capacidad excedida, estados inválidos
- **Errores HTTP**: 400, 401, 404, 500

### Estructura de respuesta de error

```json
{
  "error": true,
  "message": "Descripción del error",
  "details": "Información adicional (opcional)",
  "code": "ERROR_CODE"
}
```

## 📈 Características Avanzadas

### Validaciones de Negocio

- Verificación de capacidad de laboratorio
- Validación de fechas y horarios
- Control de transiciones de estado
- Verificación de disponibilidad

### Reportes y Estadísticas

- Uso por laboratorio
- Estadísticas por usuario
- Reportes de tiempo
- Análisis de ocupación

## 🔄 Flujo de Trabajo

1. **Registro de Usuario**: Docentes y estudiantes se registran
2. **Creación de Laboratorios**: Jefe de laboratorio configura espacios
3. **Programación de Uso**: Docentes programan sesiones
4. **Inicio de Sesión**: Se marca el inicio del uso
5. **Finalización**: Se registra el fin y se evalúa
6. **Reportes**: Se generan estadísticas y reportes

## 🔮 Próximas Características

### En desarrollo

- [ ] Sistema de autenticación JWT
- [ ] Testing completo (Jest + Supertest)
- [ ] Notificaciones en tiempo real
- [ ] Dashboard de administración
- [ ] Exportación de reportes (PDF/Excel)

# Notificador de Registro de Equipo en Laboratorio Distribuido

**Integrantes:**
- Jhon Guamán
- Fabian Palma

**Universidad de las Fuerzas Armadas ESPE**

---

## Título o tema de la práctica
Implementación de un sistema de notificación en tiempo real para el registro de equipos en laboratorio distribuido usando Socket.io y React. *(máx. 20 palabras, TL14)*

**Nombre de los estudiantes:**
Jhon Guamán, Fabian Palme *(TL12)*

---

## RESUMEN
Se desarrolló un sistema que permite notificar en tiempo real al docente cuando un estudiante registra un equipo en el laboratorio. El propósito fue mejorar la gestión y supervisión de los recursos, permitiendo al docente visualizar instantáneamente qué equipos están siendo ocupados. La solución utiliza Socket.io para la comunicación persistente entre el frontend y el backend, y React para la interfaz de usuario. Se logró una integración eficiente, cumpliendo los objetivos de la práctica y demostrando la utilidad de los eventos en tiempo real en ambientes educativos. *(TL11, 8-15 líneas)*

**Palabras Claves:** Socket.io, Notificación, Laboratorio

---

## 1. INTRODUCCIÓN
Se incluyen aspectos relacionados con los objetivos, resaltando la realización de las actividades en función al manejo y disciplina en el laboratorio. El sistema busca optimizar la comunicación entre estudiantes y docentes, facilitando la supervisión de equipos ocupados.

## 2. OBJETIVO(S)
2.1 Describir los alcances o metas de la práctica o experimento:
- Implementar un sistema de notificación instantánea para el registro de equipos.
- Mejorar la interacción y control de recursos en el laboratorio.

## 3. MARCO TEÓRICO
Socket.io permite la comunicación bidireccional en tiempo real entre clientes y servidores. El broadcasting de eventos facilita que un mensaje emitido por un cliente sea retransmitido a otros clientes conectados, permitiendo notificaciones instantáneas y sincronización de estados. React es una biblioteca para construir interfaces de usuario interactivas y dinámicas.

## 4. DESCRIPCIÓN DEL PROCEDIMIENTO
- Se configuró el backend con Express y Socket.io en el puerto 3001.
- El frontend en React se conectó al servidor de sockets desde el puerto 3000.
- El estudiante registra un equipo desde su panel, lo que emite un evento al servidor.
- El servidor retransmite el evento al docente, mostrando una notificación visual.

## 5. ANÁLISIS DE RESULTADOS
Se observa que la notificación se recibe de forma instantánea en el panel del docente al registrar un equipo desde el panel del estudiante. El sistema es robusto y permite la gestión eficiente de los equipos ocupados en el laboratorio.

| Acción              | Resultado en Estudiante | Resultado en Docente |
|---------------------|------------------------|----------------------|
| Registrar Equipo    | Mensaje de confirmación| Notificación visual  |

## 6. GRÁFICOS O FOTOGRAFÍAS
- **Panel Estudiante:** Se muestra la interfaz donde el estudiante puede registrar equipos. Cada registro genera un evento que es enviado al servidor.
- **Panel Docente:** Se observa la notificación visual en tiempo real, indicando qué estudiante ha ocupado qué equipo. Esto permite al docente monitorear la ocupación de los equipos de manera eficiente.

*(Agrega aquí los enlaces de tus imágenes en Imgur)*
- ![Panel Estudiante](https://i.imgur.com/f38u4bW.png)
- ![Panel Docente](https://i.imgur.com/33dJ9lQ.png)

## 7. DISCUSIÓN
La implementación demuestra la utilidad de los eventos en tiempo real para la gestión de laboratorios. El docente puede reaccionar rápidamente ante la ocupación de equipos, mejorando la supervisión y la experiencia de los estudiantes.

## 8. CONCLUSIONES
Se logró implementar un sistema de notificación eficiente y funcional, cumpliendo los objetivos planteados. El uso de Socket.io facilita la comunicación en tiempo real y puede ser extendido para otras funcionalidades en el laboratorio.

## 9. BIBLIOGRAFÍA
- Socket.io Documentation. https://socket.io/docs/
- React Documentation. https://react.dev/
- Express Documentation. https://expressjs.com/
- Autor: Jhon Guamán, Fabian Palme. Fecha de consulta: 08/08/2025

---

## INSTRUCCIONES DE EJECUCIÓN

1. **Instalar dependencias:**
   ```bash
   npm install
   ```
2. **Ejecutar el backend:**
   ```bash
   npm run backend:dev
   ```
   El backend se ejecuta en el puerto 3001.
3. **Ejecutar el frontend:**
   ```bash
   npm run dev
   ```
   El frontend se ejecuta en el puerto 3000.
4. **Abrir dos ventanas del navegador:**
   - Una como estudiante y otra como docente.
   - Al registrar un equipo desde el panel del estudiante, el docente recibirá una notificación instantánea.

---
"# WebSockets" 
