# 🤖 Finanzas1bot – Agente Inteligente de Finanzas Personales

Este proyecto implementa un **agente de finanzas personales automatizado** utilizando [n8n](https://n8n.io), [Ollama](https://ollama.com/), Google Sheets, Gmail y Telegram. El bot detecta automáticamente tus correos bancarios, extrae la información financiera con IA, la organiza por categorías en una hoja de cálculo y responde a tus preguntas vía Telegram con resúmenes, gráficos y consejos de ahorro.

## 📦 Características

- Clasifica automáticamente los gastos por categoría: hogar, ocio, universidad, carro, etc.
- Extrae valor, comercio y fecha desde los correos de notificación bancaria.
- Guarda los datos en **Google Sheets** para consulta y análisis.
- Responde en lenguaje natural desde Telegram con resúmenes y tips personalizados.
- Ejecuta IA en local mediante modelos como **Mistral**, **LLaMA3**, u otros usando **Ollama**.
- Todo el flujo corre de forma segura y local en tu máquina usando Docker.

## 🚀 Pasos para instalar y ejecutar

### 1. 📥 Instalar n8n localmente

Sigue la guía oficial para instalar n8n en tu máquina:  
👉 [Instalar n8n localmente](https://docs.n8n.io/integrations/creating-nodes/test/run-node-locally/)

### 2. 📝 Crear una cuenta en n8n

Una vez instales n8n, accede a `http://localhost:5678` y crea tu cuenta.

### 3. 🤖 Tener un modelo de IA disponible

Puedes elegir entre dos opciones:
- Tener corriendo **Ollama local** con un modelo descargado (`mistral`, `llama3`, etc.)
- O usar una API externa de otro modelo LLM (opcional)

Para Ollama local, corre:

```bash
docker run -d --name ollama -p 11434:11434 -v ollama-data:/root/.ollama ollama/ollama
docker exec -it ollama ollama run mistral
```

### 4. 🐳 Ejecutar Docker Compose

Este proyecto se despliega fácilmente usando Docker Compose. Usa:

```bash
docker compose up -d
```

### 5. 📁 Importar el flujo en n8n

1. Inicia sesión en n8n.
2. Clic en **"Create Workflow"**.
3. En la esquina superior derecha, haz clic en los 3 puntos `⋮` → **Import from file...**
4. Carga el archivo `Finanzas1bot.json`.

¡Listo! Ya tienes el flujo configurado.

![image](https://github.com/user-attachments/assets/1edcad17-3871-48a0-812a-9d48ea20af25)

### 6. 🔐 Crear credenciales en Google Cloud Console

1. Ve a 👉 [https://console.cloud.google.com/](https://console.cloud.google.com/)
2. Activa la API de **Gmail** y **Google Sheets**.
3. Crea un proyecto y configura OAuth 2.0.
4. Descarga el archivo JSON de credenciales y súbelo a n8n como conexión para:
   - Gmail
   - Google Sheets

### 7. ⚙️ Configurar conexión a Ollama en el `AI Agent`

En el nodo de tipo `AI Agent`, configura la URL base de Ollama así:

```
http://host.docker.internal:11434
```

Esto permite que n8n se comunique con Ollama local desde el contenedor Docker.

### 8. 💬 Crear tu bot en Telegram

1. Busca el usuario `@BotFather` en Telegram.
2. Escribe `/newbot`, elige nombre y username.
3. Copia el token que te entrega y guárdalo como credencial de Telegram en n8n.

## ✅ ¡Listo!

Ya puedes disfrutar de un asistente financiero automatizado que:

- Lee tus correos bancarios
- Clasifica tus gastos
- Los guarda en una hoja de cálculo
- Te responde por Telegram con resúmenes y consejos

💸 Automatiza el control de tus finanzas y deja de preocuparte por hacer cuentas manuales.

![image](https://github.com/user-attachments/assets/e2bb4867-6689-4884-b493-2c9132c59459)

