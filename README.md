# Notificador de Registro de Equipo en Laboratorio Distribuido

**Integrantes:**
- Jhon Guamán
- Fabian Palma

**Universidad de las Fuerzas Armadas ESPE**

---

## Título o tema de la práctica
Implementación de un sistema de notificación en tiempo real para el registro de equipos en laboratorio distribuido usando Socket.io y React. 

**Nombre de los estudiantes:**
Jhon Guamán, Fabian Palma 

---

## RESUMEN
Se desarrolló un sistema que permite notificar en tiempo real al docente cuando un estudiante registra un equipo en el laboratorio. El propósito fue mejorar la gestión y supervisión de los recursos, permitiendo al docente visualizar instantáneamente qué equipos están siendo ocupados. La solución utiliza Socket.io para la comunicación persistente entre el frontend y el backend, y React para la interfaz de usuario. Se logró una integración eficiente, cumpliendo los objetivos de la práctica y demostrando la utilidad de los eventos en tiempo real en ambientes educativos.

**Palabras Claves:** Socket.io, Notificación, Laboratorio

---

## 1. INTRODUCCIÓN
Se incluyen aspectos relacionados con los objetivos, resaltando la realización de las actividades en función al manejo y disciplina en el laboratorio. El sistema busca optimizar la comunicación entre estudiantes y docentes, facilitando la supervisión de equipos ocupados.

## 2. OBJETIVO(S)
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

- ![Panel Estudiante](https://i.imgur.com/f38u4bW.png)

  **Descripción:**
  A la izquierda se muestra el Panel Estudiante, donde el usuario tiene la opción de registrar un equipo en la columna de acciones. Se observan tres botones “Registrar Equipo” para cada práctica disponible. A la derecha está el Panel Docente, el cual se encuentra vacío y sin notificaciones, esperando la acción de algún estudiante.

- ![Panel Docente](https://i.imgur.com/33dJ9lQ.png)

  **Descripción:**
  En la izquierda, el estudiante ha presionado el botón “Registrar Equipo”, lo que genera una confirmación en su pantalla. En la derecha, el Panel Docente muestra instantáneamente una notificación azul en la parte inferior, indicando que el estudiante ha ocupado el equipo (por ejemplo: “El estudiante Estudiante prueba ha ocupado el equipo PC-05”). Esto evidencia la comunicación en tiempo real entre ambos paneles mediante Socket.io.

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
