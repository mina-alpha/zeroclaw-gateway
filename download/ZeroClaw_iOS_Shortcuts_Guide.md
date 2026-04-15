# ZeroClaw v7.0 - iOS Shortcuts Configuration Guide

## Quick Setup

Your ZeroClaw gateway is running at:
```
https://zeroclaw-gateway.monmonbolbol85.workers.dev/
```

---

## Shortcut 1: Quick Chat

**Purpose**: Send a message to ZeroClaw and get a response

### Steps:
1. Open **Shortcuts** app on iOS
2. Tap **+** to create new shortcut
3. Add **Ask for Input** action:
   - Prompt: "Ask ZeroClaw..."
   - Input Type: Text
4. Add **Get Contents of URL** action:
   - URL: `https://zeroclaw-gateway.monmonbolbol85.workers.dev/chat`
   - Method: POST
   - Headers: `Content-Type: application/json`
   - Request Body: 
     ```json
     {"message": "YOUR_INPUT_HERE"}
     ```
   - Replace `YOUR_INPUT_HERE` with the variable from step 3 (tap "Ask for Input" variable)
5. Add **Get Dictionary Value** action:
   - Get: `response`
   - From: Contents of URL
6. Add **Show Result** or **Speak Text** action

### JSON Body Template:
```json
{"message": "Shortcut Input"}
```

---

## Shortcut 2: Voice Chat (Hands-Free)

**Purpose**: Voice-activated interaction with ZeroClaw

### Steps:
1. Create new shortcut named "ZeroClaw Voice"
2. Add **Dictate Text** action:
   - Language: Your preferred language
   - Stop Listening: After Pause
3. Add **Get Contents of URL** action:
   - URL: `https://zeroclaw-gateway.monmonbolbol85.workers.dev/chat`
   - Method: POST
   - Headers: `Content-Type: application/json`
   - Request Body: `{"message": "Dictated Text"}`
4. Add **Get Dictionary Value** for `response`
5. Add **Speak Text** action with the response

### Siri Activation:
- Go to Settings > Siri & Search > All Shortcuts
- Find "ZeroClaw Voice" and add a Siri phrase like "Hey ZeroClaw"

---

## Shortcut 3: Image Generation

**Purpose**: Generate AI images via ZeroClaw

### Steps:
1. Add **Ask for Input**: "Describe the image..."
2. Add **Get Contents of URL**:
   - URL: `https://zeroclaw-gateway.monmonbolbol85.workers.dev/tools/image_gen`
   - Method: POST
   - Headers: `Content-Type: application/json`
   - Request Body:
     ```json
     {"prompt": "YOUR_INPUT", "width": 1024, "height": 1024}
     ```
3. Add **Quick Look** to preview the result

---

## Shortcut 4: Web Search

**Purpose**: Quick web search through ZeroClaw

### Steps:
1. Add **Ask for Input**: "Search for..."
2. Add **Get Contents of URL**:
   - URL: `https://zeroclaw-gateway.monmonbolbol85.workers.dev/tools/web_search`
   - Method: POST
   - Headers: `Content-Type: application/json`
   - Request Body:
     ```json
     {"query": "YOUR_INPUT", "max_results": 5}
     ```
3. Parse and display results

---

## Shortcut 5: Memory Storage

**Purpose**: Store information for later recall

### Steps:
1. Add **Ask for Input**: "What should I remember?"
2. Add **Get Contents of URL**:
   - URL: `https://zeroclaw-gateway.monmonbolbol85.workers.dev/tools/memory_store`
   - Method: POST
   - Headers: `Content-Type: application/json`
   - Request Body:
     ```json
     {"content": "YOUR_INPUT", "tags": ["personal"]}
     ```
3. Show confirmation

---

## Shortcut 6: Memory Recall

**Purpose**: Recall stored memories

### Steps:
1. Add **Ask for Input**: "What do you want to recall?"
2. Add **Get Contents of URL**:
   - URL: `https://zeroclaw-gateway.monmonbolbol85.workers.dev/tools/memory_recall`
   - Method: POST
   - Headers: `Content-Type: application/json`
   - Request Body:
     ```json
     {"query": "YOUR_INPUT", "limit": 5}
     ```
3. Display memories

---

## Shortcut 7: Weather Check

### Steps:
1. Add **Ask for Input**: "Location?"
2. Add **Get Contents of URL**:
   - URL: `https://zeroclaw-gateway.monmonbolbol85.workers.dev/tools/weather`
   - Method: POST
   - Request Body:
     ```json
     {"location": "YOUR_INPUT", "units": "celsius"}
     ```
3. Display weather data

---

## Shortcut 8: Quick Note to ZeroClaw

### Widget-Friendly Shortcut:
1. Add **Text** action with your default note
2. Add **Get Contents of URL**:
   - URL: `https://zeroclaw-gateway.monmonbolbol85.workers.dev/chat`
   - Method: POST
   - Request Body: `{"message": "Remember: YOUR_NOTE"}`
3. Add notification or haptic feedback

---

## API Endpoints Reference

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/chat` | POST | Main conversation |
| `/chat/stream` | POST | Streaming conversation |
| `/tools/web_search` | POST | Web search |
| `/tools/image_gen` | POST | Generate images |
| `/tools/weather` | POST | Weather data |
| `/tools/memory_store` | POST | Store memory |
| `/tools/memory_recall` | POST | Recall memories |
| `/tools/summarize` | POST | Summarize text |
| `/tools/code_assist` | POST | Code help |
| `/health` | GET | Health check |
| `/doctor` | GET | System status |
| `/tools` | GET | List all tools |

---

## Widget Setup

Add shortcuts to your home screen:
1. Long press on empty space
2. Tap **+** in corner
3. Search for **Shortcuts**
4. Select widget size
5. Choose your ZeroClaw shortcut

---

## Automation Ideas

### Morning Briefing:
- Trigger: Time of day (e.g., 7:00 AM)
- Actions:
  1. Get weather
  2. Ask ZeroClaw for daily motivation
  3. Speak results

### Location-Based:
- Trigger: Arrive at location
- Action: Ask ZeroClaw for location-relevant info

### Charging Mode:
- Trigger: Connect to charger
- Action: Daily summary from ZeroClaw

---

## Troubleshooting

### "Could not connect to server"
- Check internet connection
- Verify URL is correct
- Worker may be sleeping (first request takes longer)

### Empty Response
- Check your JSON format
- Ensure Content-Type header is set

### Timeout
- Workers have 30-second limit
- Complex queries may need retry

---

## Security Notes

- Your ZeroClaw is public on `.workers.dev`
- For sensitive data, add authentication
- Consider using a custom domain with SSL

---

*ZeroClaw v7.0 - Your Personal AI Assistant*
