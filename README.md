# GrowBot AI Chatbot

A Claude-powered chatbot for GrowBot that demonstrates AI customer service for trades businesses and answers questions about GrowBot services.

## Features

- **Dual Mode Operation**: 
  - **Information Mode**: Answers questions about GrowBot pricing, features, and services
  - **Demo Mode**: Simulates handling customer enquiries for a heating/plumbing company
- **Claude AI**: Powered by Anthropic's Claude for natural, intelligent conversations
- **Lead Capture**: Webhook integration to send leads to GoHighLevel
- **Embeddable Widget**: Drop-in chat widget for any website
- **Session Management**: Maintains conversation context per user

## Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/growbot-chatbot.git
cd growbot-chatbot
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment

Copy the example env file and add your API key:

```bash
cp .env.example .env
```

Edit `.env` and add:
- `ANTHROPIC_API_KEY`: Your Anthropic API key (required)
- `GHL_WEBHOOK_URL`: Your GoHighLevel webhook URL (optional)

### 4. Run Locally

```bash
npm start
```

Visit `http://localhost:3000` to see the chatbot.

## Deployment to Render

### Step 1: Push to GitHub

1. Create a new repository on GitHub
2. Push this code to your repository:

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/your-username/growbot-chatbot.git
git push -u origin main
```

### Step 2: Deploy on Render

1. Go to [render.com](https://render.com) and sign in
2. Click **New** → **Web Service**
3. Connect your GitHub repository
4. Configure the service:
   - **Name**: `growbot-chatbot`
   - **Environment**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
5. Add Environment Variables:
   - `ANTHROPIC_API_KEY`: Your Anthropic API key
   - `GHL_WEBHOOK_URL`: Your GHL webhook (optional)
6. Click **Create Web Service**

Your chatbot will be live at `https://growbot-chatbot.onrender.com` (or similar).

## Embedding the Widget

### Option 1: Full Page (for demo)

Link directly to your Render URL:
```
https://your-growbot-app.onrender.com
```

### Option 2: Floating Widget

Add this script to any website to show the chat widget:

```html
<script>
(function() {
    var iframe = document.createElement('iframe');
    iframe.src = 'https://your-growbot-app.onrender.com/widget.html';
    iframe.style.cssText = 'position:fixed;bottom:0;right:0;width:420px;height:650px;border:none;z-index:9999;';
    document.body.appendChild(iframe);
})();
</script>
```

**Important**: Update the URL in `widget.html` to point to your Render deployment:

```javascript
const GROWBOT_API_URL = 'https://your-growbot-app.onrender.com';
```

### Option 3: Embed in GHL/Website Builder

1. Open `widget.html` in a text editor
2. Update `GROWBOT_API_URL` to your Render URL
3. Copy all the code
4. In your website builder, add a "Custom HTML" or "Embed Code" element
5. Paste the widget code

## File Structure

```
growbot-chatbot/
├── server.js           # Express server with Claude API integration
├── package.json        # Node.js dependencies
├── .env.example        # Environment variables template
├── README.md           # This file
└── public/
    ├── index.html      # Full page chat demo
    └── widget.html     # Embeddable floating widget
```

## API Endpoints

### POST /api/chat

Send a message and get a response from Sophie.

**Request:**
```json
{
  "message": "How much does GrowBot cost?",
  "sessionId": "unique_session_id"
}
```

**Response:**
```json
{
  "response": "GrowBot is £1,997 per month plus VAT...",
  "sessionId": "unique_session_id"
}
```

### POST /api/webhook/lead

Send lead data to GoHighLevel (if configured).

**Request:**
```json
{
  "name": "John Smith",
  "email": "john@example.com",
  "phone": "07700900123",
  "company": "Smith Plumbing",
  "message": "Interested in GrowBot",
  "source": "growbot-chatbot"
}
```

### GET /api/health

Health check endpoint for monitoring.

## Customisation

### Changing the AI Personality

Edit the `SYSTEM_PROMPT` constant in `server.js` to modify Sophie's personality, knowledge, or conversation style.

### Changing Branding

Edit the CSS in `public/index.html` and `public/widget.html`:
- `--primary`: Main brand colour (currently teal #0f766e)
- `--secondary`: Secondary colour (currently navy #1e3a5f)

### Adding More Demo Scenarios

Expand the "Demo Mode" section in the system prompt to handle additional scenarios (electrical, HVAC, etc.).

## Troubleshooting

### "Failed to get response from AI"

- Check your `ANTHROPIC_API_KEY` is correct
- Ensure you have API credits available
- Check the Render logs for error details

### Widget not appearing

- Verify the `GROWBOT_API_URL` in widget.html matches your Render URL
- Check browser console for CORS errors
- Ensure Render service is running (not sleeping on free tier)

### Slow responses

- Free Render instances sleep after 15 minutes of inactivity
- First request after sleeping takes ~30 seconds
- Upgrade to paid Render tier for always-on performance

## Support

For help with GrowBot, contact:
- Dan Andrews: dan.andrews@growbot.services
- Damian Smyth: damian.smyth@growbot.services
