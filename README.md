# 🧠 Local Intelligence: LM Studio + MERN Workshop

Welcome to the **Local Intelligence** workshop. This repo contains a starter MERN stack application designed to interface directly with an LLM running locally on your machine.

**The Goal:** Build a private, free, and offline-capable AI application without relying on OpenAI/Anthropic API keys.

---

## 🛠 Prerequisites

Before we start the code, ensure you have the following:

1. **Node.js & npm** (Installed)
2. **[LM Studio](https://lmstudio.ai/)** (Downloaded & Installed)
3. **Hardware Check:** At least 8GB RAM (16GB recommended).

---

## 🚀 Phase 1: The Engine (LM Studio Setup)

We need to turn your laptop into an AI server.

1. **Open LM Studio** and search for a model.
* *Recommendation:* Search `Llama 3` or `Mistral Instruct`.
* *Look for the Green Bar:* Download a version that says **"Likely to run"** (usually `Q4_K_M`).


2. **Navigate to the Server Tab** (The `<->` icon on the left).
3. **Select your model** from the top dropdown to load it into RAM.
4. **Server Configuration:**
* **Port:** `1234` (Default)
* **Cross-Origin-Resource-Sharing (CORS):** ✅ **ON** (Check the box)


5. **Start Server:** Click the green **Start Server** button.

> **Verification:** You should see logs appearing in the bottom window. Your local API is now live at `http://localhost:1234/v1`.

---

## 💻 Phase 2: The Application (MERN)

### 1. Clone & Install

```bash
git clone https://github.com/sreenidhi-n/lm-studio-mern-app
cd src

```

### 2. Backend Setup

We use the official OpenAI SDK, but we "trick" it to talk to our local server instead of Sam Altman's servers.

Navigate to the server folder:

```bash
cd server
npm install

```

**Key Code Snippet (`server/index.js`):**

```javascript
const client = new OpenAI({
  baseURL: "http://localhost:1234/v1", // Points to your machine
  apiKey: "lm-studio", // Placeholder string (required by SDK)
});

```

Start the backend:

```bash
node index.js
# Server running on http://localhost:5000

```

### 3. Frontend Setup

Open a new terminal and navigate to the client folder:

```bash
cd client
npm install
npm start

```

---

## 🧪 Experimentation Guide

Now that you are connected, try these tweaks to "extract the most" out of your model:

### 1. The System Prompt

In `server/index.js`, find the `messages` array. Change the `system` role to alter the AI's personality:

```javascript
{ role: "system", content: "You are a senior cybersecurity engineer. Answer efficiently." }

```

### 2. Tuning Parameters

* **Temperature (`0.1` - `1.0`):** Low for code/logic, High for creative writing.
* **Max Tokens:** Limit the response length to ensure speed.

### 3. JSON Mode (Advanced)

If you are building an app that needs structured data, instruct the model in the System Prompt:

> *"You must strictly answer in JSON format containing a 'summary' and a 'sentiment' field."*

---

## 🔒 A Note on Security

*Why do we use a backend (Node.js) instead of calling the AI directly from React?*

Even though `localhost` is safe, in a production environment, you **never** expose your AI interaction logic to the client browser. Using a backend allows you to:

1. **Rate Limit:** Stop users from spamming your model.
2. **Sanitize Inputs:** Prevent "Prompt Injection" attacks before they reach the LLM.
3. **Hide Context:** Keep your "System Prompt" proprietary.

---

## 📚 Resources

* [LM Studio Documentation](https://lmstudio.ai/docs)
* [HuggingFace](https://huggingface.co/) (The source of all models)

**Happy Hacking.**
