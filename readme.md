# 📊 Automatización de Alertas de la tendencia de Bitcoin

![Estado del Proyecto](https://img.shields.io/badge/Status-Finalizado-success)
![n8n](https://img.shields.io/badge/Workflow-n8n-orange)
![AI](https://img.shields.io/badge/AI-Google_Gemini-blue)

Este proyecto implementa un **flujo automatizado en n8n** que analiza el comportamiento del precio de **Bitcoin** en las últimas 24 horas utilizando **Price Action**, genera un **reporte técnico con IA**, lo registra en **Google Sheets** y envía una **alerta por email** cuando se detecta una tendencia relevante.

## Descripción del Proyecto

El objetivo es eliminar el monitoreo manual de precios. El bot consulta el precio de Bitcoin, se lo envía a un LLM (Modelo de Lenguaje) con un rol de "Analista Experto" para que determine la tendencia e informe mediante un email un cambio de tendencia.

## Funcionalidades principales

- ⏱️ Ejecución automática mediante **Schedule Trigger**
- 📡 Obtención de precios de Bitcoin desde **CoinGecko API**
- 📈 Análisis técnico basado en:
  - Open, High, Low, Close
  - Estructura de mercado
  - Detección de tendencia: **ALCISTA, BAJISTA o LATERAL**
- 🤖 Uso de **IA** para:
  - Clasificar la tendencia del mercado
  - Generar un reporte financiero formal en español
- 📄 Registro histórico de resultados en **Google Sheets**
- ✉️ Envío de alertas por email cuando la tendencia **no es lateral**

---

## Lógica del flujo

1. **Schedule Trigger**  
   Inicia el flujo de forma automática según el intervalo configurado.

2. **API CoinGecko**  
   Obtiene el histórico de precios de Bitcoin de las últimas 24 horas en USD.

3. **Análisis Técnico con IA**  
   - Se envían los precios a un modelo LLM
   - El modelo calcula:
     - Precio de apertura y cierre
     - Máximos y mínimos
     - Variación porcentual
     - Tipo de tendencia

4. **Condición de Tendencia**
   - Si la tendencia es **LATERAL**, no se envía alerta
   - Si es **ALCISTA** o **BAJISTA**, continúa el flujo

5. **Registro en Google Sheets**
   Se guarda:
   - Fecha y hora
   - Precio actual
   - Tendencia detectada
   - Justificación técnica
   - Cambio porcentual 24h

6. **Generación de Reporte Financiero**
   - Se crea un email en español formal utilizando **Gemini**
   - Formato HTML tipo briefing financiero

7. **Envío de Alerta por Email**
   - Asunto dinámico según tendencia y variación
   - Contenido profesional y objetivo
---


## Tecnologías Utilizadas

* **Orquestador:** [n8n](https://n8n.io/) (Workflow Automation).
* **Inteligencia Artificial:** Google Gemini API (Modelos `gemini-2.5-flash`).
* **Base de Datos:** Google Sheets API.
* **Seguridad:** Google Cloud Platform (OAuth 2.0 Client ID & Secret).
* **Fuente de Datos:** CoinGecko API.

---

## Datos de prueba

El workflow incluye nodos con **datos simulados** para probar distintos escenarios de mercado:
- Tendencia alcista
- Tendencia bajista
- Mercado lateral

Esto permite validar el comportamiento del flujo sin depender de la API externa.

---

## Estructura del Repositorio

El proyecto se organiza de la siguiente manera para facilitar su despliegue y revisión:

```text
├── README.md                    # Documentación técnica y funcional
├── workflow/
│   └── worlflow_n8n.json        # Archivo fuente para importar en n8n
├── prompts/
│   ├── analista_prompt          # Archivo txt con el prompt que utiliza el primer nodo
│   └── redactor_prompt          # Archivo txt con el prompt que utiliza el segundo nodo
└── evidencia/
    ├── n8n_workflow.png         # Captura de la arquitectura del flujo
    ├── sheets_log.png           # Captura del log de auditoría en Sheets
    ├── email_bajista.png        # Captura de pantalla del email enviado en una tendencia bajista
    └── email_alcista.png        # Captura de pantalla del email enviado en una tendencia alcista
```
---

## Evidencias de Funcionamiento

A continuación se presentan las pruebas de ejecución exitosa del sistema.

### 1. Vista General del Workflow
Arquitectura completa de nodos en n8n, mostrando las conexiones y la lógica condicional.

![Workflow Completo](./evidencia/n8n_workflow.png)

### 2. Log de Auditoría (Google Sheets)
Prueba de persistencia de datos. Se observa cómo el bot escribe la fecha, el precio detectado, el razonamiento de la IA y el porcentaje de cambio de las ultimas 24 HS.

![Log en Google Sheets](./evidencia/sheets_log.png)

*(Nota: El resto de imágenes se encuentran en la carpeta `/evidencia` de este repositorio).*

---

## Seguridad y Configuración

Este proyecto se diferencia por implementar **estándares de seguridad empresarial**:

* **No se utilizan Service Accounts inseguras.**
* Se implementó **OAuth 2.0** a través de Google Cloud Console.
* El bot tiene permisos de "Mínimo Privilegio" (Scope): solo puede editar las hojas de cálculo creadas por la aplicación, sin acceso al correo personal ni al resto del Drive del usuario.

---

## Cómo ejecutar este proyecto

1.  Tener una instancia de **n8n** instalada (Desktop o Cloud).
2.  Importar el archivo `workflow/Workflow_Bitcoin_AI.json` incluido en este repositorio.
3.  Configurar las credenciales en n8n:
    * **Google Gemini:** Crear API Key en Google AI Studio.
    * **Google Sheets:** Configurar credencial OAuth2 en Google Cloud Console.
4.  Activar el workflow.

---

## Licencia

Este proyecto se distribuye bajo la **Licencia MIT**.

Se permite el uso, copia, modificación, fusión, publicación, distribución, sublicencia y/o venta del software, siempre que se incluya el aviso de copyright y esta misma licencia en todas las copias o partes sustanciales del software.

El software se proporciona **“tal cual”**, sin garantía de ningún tipo, expresa o implícita, incluyendo —pero no limitándose a— garantías de comercialización, idoneidad para un propósito particular y no infracción.  
En ningún caso los autores o titulares de los derechos serán responsables por cualquier reclamo, daño u otra responsabilidad, ya sea en una acción de contrato, agravio o de otro tipo, que surja de, fuera de o en conexión con el software o su uso.


---

## Autor

**Desarrollado por Franco Valentin Guerrero**

* 🚀 **Especialidad:** Data Science & Automatización de Procesos.
* 🐙 **GitHub:** [Ver perfil](https://github.com/franvg99)
* 💼 **LinkedIn:** [Ver perfil](https://linkedin.com/in/fguerrero99)

---
*Este proyecto forma parte de una entrega para la carrera de AI Automation en **CODERHOUSE**.*