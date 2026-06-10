# n8n-workflows
Flujos de n8n (auto-alojado) para automatización con IA — WhatsApp, agentes con herramientas, RAG y extracción de datos. Importa y conecta tus credenciales.

# n8n Workflows

Colección de flujos de automatización con **n8n** (instancia auto‑alojada). Cada archivo `.json` es una **plantilla lista para importar**: no contiene credenciales ni datos personales, solo marcadores (`YOUR_...`) que cada quien reemplaza con los suyos.

> Los exports de n8n **nunca incluyen los valores secretos** de las credenciales (API keys, tokens), solo una referencia interna. En estas plantillas esas referencias también se eliminaron, así que al importar cada nodo te pedirá conectar tu propia credencial.

## Cómo usar

1. En tu n8n, ve a **Workflows → menú (⋮) → Import from File** y selecciona el `.json` (o ábrelo y pega el contenido).
2. En cada nodo con icono de credencial, crea/selecciona **tus propias credenciales** (Google, WhatsApp, Groq, etc.).
3. Busca y reemplaza los **marcadores** (ver tabla) por tus valores reales.
4. Activa el flujo.

## Flujos incluidos

| Archivo | Qué hace | Integraciones | Marcadores a reemplazar |
|---|---|---|---|
| `whatsapp-ai-chatbot-groq.json` | Chatbot de WhatsApp: recibe mensajes por la Cloud API, verifica el token, los pasa a un LLM (Groq · Llama 3.3 70B) y responde. | WhatsApp Cloud API, Groq | `YOUR_VERIFY_TOKEN`, `YOUR_WHATSAPP_PHONE_NUMBER_ID`, `YOUR_RECIPIENT_PHONE_NUMBER` |
| `whatsapp-calendar-agent.json` | Asistente de agenda por WhatsApp **multimodal**: entiende texto, voz (transcripción) e imágenes (visión); un agente de IA con herramientas de Google Calendar agenda, reprograma, consulta y cancela citas, con memoria de conversación. | WhatsApp Cloud API, Groq (Whisper + visión + LLM), Google Calendar | `YOUR_VERIFY_TOKEN`, `YOUR_WHATSAPP_PHONE_NUMBER_ID`, `YOUR_RECIPIENT_PHONE_NUMBER`, `YOUR_GOOGLE_CALENDAR_ID` |
| `google-drive-to-pinecone-rag.json` | Ingesta para **RAG**: descarga un archivo de Drive, lo divide en fragmentos, genera embeddings (HuggingFace · all‑MiniLM‑L6‑v2) y los guarda en un índice de Pinecone. | Google Drive, HuggingFace, Pinecone | `YOUR_GOOGLE_DRIVE_FILE_ID`, `your-pinecone-index` |
| `email-to-sheets-ai-extractor.json` | Lee correos entrantes (Gmail), extrae datos estructurados con IA y los agrega como fila en Google Sheets. | Gmail, Groq, Google Sheets | `YOUR_GOOGLE_SHEET_ID` |
| `pdf-data-extractor-ai.json` | Lee adjuntos PDF de Gmail, extrae el texto, usa un agente de IA para devolver campos en JSON, los limpia/normaliza y los agrega a Google Sheets. | Gmail, Groq, Google Sheets | `YOUR_GOOGLE_SHEET_ID` |
| `form-lead-router-sheets.json` | Recibe respuestas de un formulario (webhook tipo Typeform), separa por edad (mayores/menores), guarda en Sheets según el interés y notifica por correo. | Webhook/Typeform, Google Sheets, Gmail | `YOUR_GOOGLE_SHEET_ID`, `your-email@example.com` |

## Notas

- Todos los flujos vienen **desactivados** (`active: false`) por defecto.
- En los nodos de WhatsApp, el destinatario está como marcador; lo habitual es responder al número que escribió (valor dinámico).
- Probado en n8n auto‑alojado.

## Licencia

MIT (ajústala a tu preferencia).
