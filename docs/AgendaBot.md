# Especificaciones Técnicas: AgendaBot Services 🤖📑

Este documento constituye el manual técnico oficial de la implementación de **AgendaBot**, diseñado bajo los lineamientos de cumplimiento del Reglamento General de AgendaBot Services.

---

## 1. Introducción (Artículo 1)
AgendaBot es un ecosistema de automatización diseñado para la gestión integral de citas, tareas y hábitos. La arquitectura está optimizada para operar de forma gratuita, sin dependencia de servicios de pago ni requisitos de tarjeta de crédito, cumpliendo con la restricción de costos operativos cero.

## 2. Stack Tecnológico (Artículo 2)
La implementación se basa exclusivamente en las siguientes tecnologías:
- **Telegram Bot API:** Interfaz de usuario conversacional.
- **n8n Community Edition:** Motor de flujos lógicos y orquestación (Self-hosted).
- **Google Sheets API:** Sistema de gestión de base de datos (DBMS).
- **Ngrok:** Protocolo de túnel para exposición de Webhooks locales bajo HTTPS.

## 3. Modelo de Datos "AgendaBot_DB" (Artículo 4)
La persistencia de datos se gestiona mediante un libro de Google Sheets con las siguientes tablas y estructuras de columnas:

- **CITAS:** `id_cita`, `fecha`, `hora`, `nombre`, `motivo`, `canal`, `estado`, `creado_por`, `timestamp_creacion`.
- **TAREAS:** `id_tarea`, `titulo`, `prioridad`, `estado`, `fecha_objetivo`, `creado_por`.
- **HABITOS:** `id_habito`, `nombre`, `frecuencia`, `hora_recordatorio`, `estado`.
- **LOGS:** `timestamp`, `telegram_user`, `pantalla`, `opcion_elegida`, `resultado`.
- **SESSIONS:** `telegram_user`, `pantalla_actual`, `paso_actual`, `datos_parciales`, `timestamp_ultima_interaccion`.

## 4. Arquitectura de Navegación y Lógica (Artículos 3, 5 y 8)
El bot opera bajo el paradigma de **Máquina de Estados (State Machine)**. El comportamiento del sistema varía dinámicamente según el estado almacenado en la tabla `SESSIONS`:

### 4.1 Master Router
Un nodo central de tipo *Switch* evalúa la variable `pantalla_actual` antes de cada procesamiento. Esto permite que el sistema identifique si el usuario se encuentra en el **MENU_PRINCIPAL**, **MENU_AGENDA** o dentro de un flujo guiado (**WIZARD_CITAS**).

### 4.2 Principios de Comunicación (Artículo 5)
Cada interacción ha sido diseñada para ser humanizada, incluyendo:
- Saludos cercanos y emojis contextuales.
- Opciones numeradas para facilitar la interacción móvil.
- Mensajes de error informativos (Fallback) que indican la ubicación actual del usuario (Art. 7).

## 5. Flujo Guiado: Wizard de Citas (Artículo 10)
Se implementó un motor de captura de datos de 6 etapas para el agendamiento de citas:
1. **Fecha:** Entrada en formato YYYY-MM-DD.
2. **Hora:** Entrada en formato 24h.
3. **Nombre:** Registro nominal del cliente.
4. **Motivo:** Descripción del servicio.
5. **Canal:** Selección numérica (1. Presencial, 2. Virtual, 3. Llamada).
6. **Confirmación:** Deserialización de un objeto JSON almacenado temporalmente en `datos_parciales` para mostrar un resumen final antes del `Append Row` en la tabla definitiva de **CITAS**.

## 6. Automatizaciones Obligatorias (Artículo 11)

### 6.1 Auditoría (Logs)
Se ha configurado un registro paralelo de auditoría. Cada entrada procesada por el Master Router dispara un guardado automático en la hoja `LOGS`, permitiendo la trazabilidad completa de las acciones de cada usuario.

### 6.2 Resumen Diario
Se implementó un flujo independiente activado por un `Schedule Trigger`. Este proceso:
1. Se activa diariamente a las 08:00 AM (Zona: America/Bogota).
2. Consulta la tabla `CITAS` filtrando por la fecha actual.
3. Envía un reporte consolidado vía Telegram detallando la agenda del día.

### 6.3 Gestión de Tareas
Módulo de consulta dinámica que permite al usuario visualizar sus pendientes registrados en la tabla `TAREAS` mediante un mapeo de datos en tiempo real.

## 7. Validaciones y Control (Artículo 12)
- **Control de Tipos:** Conversión automática de *String* a *Number* en nodos Switch para evitar discrepancias entre los datos de Telegram y Google Sheets.
- **Validación de Sesión:** El sistema limpia los datos parciales tras una confirmación exitosa para evitar basura de datos en futuras interacciones.
- **Always Output Data:** Configuración en nodos de lectura para garantizar que el flujo no se detenga ante resultados nulos.

---
**Autor:** Juan Rojas 
**Organización:** AgendaBot Services  
**Estatus:** Entregado - Versión 1.0.0

