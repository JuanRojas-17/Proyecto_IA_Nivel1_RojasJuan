# 🤖 AgendaBot Services

> **Tu asistente personal automatizado para Telegram.**
> Gestiona citas, tareas, hábitos y listas sin suscripciones ni servidores costosos.

![Status](https://img.shields.io/badge/Estado-En_Desarrollo-orange?style=flat-square)
![Stack](https://img.shields.io/badge/Stack-n8n_|_Google_Sheets_|_Telegram-blue?style=flat-square)
![License](https://img.shields.io/badge/Licencia-Open_Source-green?style=flat-square)

---

## 📌 Sobre el Proyecto

**AgendaBot Services** es un bot conversacional diseñado para ayudar a usuarios a organizar su vida digital de forma sencilla y gratuita. A diferencia de las soluciones premium, este proyecto utiliza herramientas accesibles (Low-Code/No-Code) para ofrecer una experiencia robusta de gestión personal.

El sistema opera bajo un enfoque de **"Máquina de Estados"**, permitiendo recordar el contexto de la conversación (wizard de citas, pasos de tareas) sin necesidad de una base de datos compleja.

## ✨ Características Principales

* **📅 Gestión de Citas:** Flujo guiado paso a paso para agendar, reprogramar y cancelar citas.
* **✅ Control de Tareas:** Organización por prioridad y seguimiento de estados.
* **🔁 Hábitos y Rutinas:** Automatización de recordatorios y tracking de cumplimiento.
* **📋 Listas Personalizadas:** Gestión dinámica de items (compras, ideas, pendientes).
* **🧠 Memoria Contextual:** El bot "recuerda" en qué paso estás (gracias a la lógica de Sesiones).
* **🎨 UI Moderna:** Interfaz basada en **Botones Interactivos (Inline Buttons)** y mensajes con formato rico (Markdown) para una experiencia tipo App.

---

## ⚙️ Stack Tecnológico

El proyecto ha sido construido integrando servicios gratuitos y de código abierto:

| Componente | Herramienta | Función |
| :--- | :--- | :--- |
| **Interfaz** | 📲 **Telegram API** | Canal de comunicación con el usuario (Front-end). |
| **Lógica** | ⚡ **n8n** (Community) | Cerebro del bot: Router, lógica de negocio y automatización. |
| **Base de Datos** | 📊 **Google Sheets** | Persistencia de datos, sesiones, logs y usuarios. |

---

## 🗂️ Modelo de Datos (Google Sheets)

El sistema utiliza un libro principal `AgendaBot_DB` con las siguientes hojas conectadas a n8n:

### 📌 Principales
| Hoja | Columnas Clave | Descripción |
| :--- | :--- | :--- |
| **CITAS** | `id_cita`, `fecha`, `hora`, `nombre`, `motivo`, `estado` | Registro histórico y futuro de agendamientos. |
| **TAREAS** | `id_tarea`, `titulo`, `prioridad`, `estado`, `fecha_objetivo` | Backlog de tareas personales. |
| **HABITOS** | `id_habito`, `nombre`, `frecuencia`, `hora`, `estado` | Configuración de rutinas recurrentes. |
| **LISTAS** | `id_lista`, `nombre`, `items` | Contenedores para items varios. |

### ⚙️ Sistema (Core)
| Hoja | Columnas Clave | Descripción |
| :--- | :--- | :--- |
| **USUARIOS** | `telegram_user`, `rol`, `permitido` | Control de acceso (Lista blanca). |
| **SESSIONS** | `telegram_user`, `pantalla_actual`, `datos_parciales` | **Vital:** Mantiene el estado del usuario en el flujo. |
| **LOGS** | `timestamp`, `accion`, `resultado` | Auditoría de interacciones y errores. |

---

## 🧩 Flujos de Conversación

El bot no utiliza comandos de texto simples, sino una navegación estructurada:

### 1. Menú Principal (Dashboard)
El usuario recibe un panel de control con botones táctiles:
* [📅 Agenda]
* [✅ Tareas]
* [🔁 Hábitos]
* [⚙️ Configuración]

### 2. Wizard de Agendamiento (Ejemplo)
Un flujo lineal de 6 pasos gestionado por el Router de n8n:
1.  **Inicio:** Botón "Nueva Cita".
2.  **Fecha:** Input de usuario (validado).
3.  **Hora:** Input de usuario.
4.  **Detalles:** Cliente, Motivo, Canal.
5.  **Confirmación:** Tarjeta resumen con botones [Guardar] o [Editar].
6.  **Éxito:** Ticket generado con ID único.

---

## 🚀 Instalación y Despliegue

### Requisitos Previos
1.  Cuenta de Telegram y un Bot creado con `@BotFather`.
2.  Instancia de n8n (Local, Docker o Cloud).
3.  Cuenta de Google (para Sheets API).

### Pasos
1.  **Base de Datos:**
    * Crea un Google Sheet nuevo.
    * Replica las hojas y columnas descritas en la sección "Modelo de Datos".
2.  **n8n:**
    * Importa el workflow JSON (disponible en la carpeta `/workflows`).
    * Configura las credenciales de **Telegram Bot API**.
    * Configura las credenciales de **Google Sheets OAuth2**.
    * Enlaza los Nodos de Google Sheets con el ID de tu hoja de cálculo.
3.  **Activación:**
    * Activa el workflow en n8n.
    * En Telegram, envía `/start` a tu bot.

---

## 🧪 Pruebas Realizadas

Se ha seguido un plan de pruebas exhaustivo (QA):
- [x] Navegación completa por menús (Botones).
- [x] CRUD de Citas (Crear, Leer, Actualizar, Borrar).
- [x] Validación de fechas pasadas y formatos incorrectos.
- [x] Persistencia de sesiones (el bot no "olvida" lo que estabas haciendo).
- [x] Bloqueo de usuarios no autorizados.

---

## 👨‍💻 Autores y Créditos

Desarrollado con ❤️ y enfoque en automatización accesible por:

* **Carlos Andres Caceres Orduz** - *Desarrollo y Arquitectura*
* **Juan Rojas** - *Desarrollo e Implementación*

**Licencia:** MIT (Gratuito para uso personal y educativo).

---
*Este proyecto es parte de una iniciativa para democratizar el uso de Chatbots sin dependencias de servicios de pago.*
