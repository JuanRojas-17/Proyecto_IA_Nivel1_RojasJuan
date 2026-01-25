# AgendaBot Services 🤖📅

![n8n](https://img.shields.io/badge/Automation-n8n_Community-red?style=for-the-badge&logo=n8n)
![Telegram](https://img.shields.io/badge/Interface-Telegram_Bot-blue?style=for-the-badge&logo=telegram)
![Google Sheets](https://img.shields.io/badge/Database-Google_Sheets-green?style=for-the-badge&logo=google-sheets)

**AgendaBot Services** es una solución avanzada de automatización conversacional diseñada para centralizar la gestión de citas, tareas y hábitos. Este proyecto ha sido desarrollado bajo la premisa de **"Cero Costo Operativo"**, utilizando herramientas de código abierto y niveles gratuitos de APIs, eliminando la necesidad de tarjetas de crédito o suscripciones de pago.

## 🌟 Características Destacadas

- **Interfaz Conversacional Intuitiva:** Sistema de navegación basado en menús numéricos que garantiza una curva de aprendizaje mínima para el usuario (Art. 3, 8 y 9).
- **Máquina de Estados Eficiente:** El bot gestiona sesiones individuales, permitiendo que varios usuarios interactúen simultáneamente sin pérdida de contexto.
- **Wizard de Agendamiento:** Flujo guiado de 6 pasos para la creación de citas con resumen de confirmación y persistencia de datos (Art. 10).
- **Gestión de Tareas:** Módulo dinámico para visualizar y registrar pendientes en tiempo real.
- **Automatización de Reportes:** Envío programado de un resumen diario de citas cada mañana a las 08:00 AM (Art. 11).
- **Auditoría y Logs:** Sistema de trazabilidad total que registra cada interacción en una base de datos centralizada para fines de control (Art. 11).

## 🛠️ Stack Tecnológico

- **Lógica de Negocio:** [n8n Community Edition](https://n8n.io/) (Self-hosted).
- **Interfaz de Usuario:** [Telegram Bot API](https://core.telegram.org/bots).
- **Base de Datos:** [Google Sheets API](https://developers.google.com/sheets/api) mediante Service Account.
- **Túnel de Comunicación:** [Ngrok](https://ngrok.com/) para exposición segura de Webhooks locales.

## 📁 Estructura del Repositorio

Siguiendo el **Artículo 15** del reglamento, el proyecto se organiza de la siguiente manera:

```text
Proyecto_IA_Nivel1_ApellidoNombre/
├── README.md                # Descripción general y guía de inicio.
├── docs/
│   └── AgendaBot.md         # Manual técnico y especificaciones de arquitectura.
├── workflows/
│   ├── AgendaBot_Main.json      # Flujo principal (Menús y Wizard).
│   └── AgendaBot_Resumen.json   # Flujo de automatización (Resumen Diario).
└── evidencias/              # Capturas de pantalla del bot y base de datos funcionando.

Desarrollado por: Juan Rojas
Proyecto de IA - Nivel 1
Fecha: Enero 2026

