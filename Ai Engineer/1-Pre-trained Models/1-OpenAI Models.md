# **OpenAI Models Overview**

OpenAI offers various AI models for text, image, and speech applications:

## **1. GPT-4o**

- **Flagship model** with **text & image input** support.
- **128K context length** and **multilingual** capabilities.

## **2. GPT-4o Mini**

- **Faster & cost-effective** version of GPT-4o.
- Ideal for **lightweight** tasks.

## **3. GPT-4 Turbo**

- **Optimized** for speed & efficiency.
- Suitable for **high-performance** applications.

## **4. GPT-3.5**

- **Affordable** option for general AI tasks.
- Balances **cost, speed, and accuracy**.

## **5. DALL·E 3**

- AI-driven **image generation** from text.
- Supports **inpainting & editing**.

## **6. Whisper**

- **Speech-to-text** model with **high accuracy**.
- Handles **multiple languages**.

## **7. Embedding Models**

- Converts text into **numerical vectors** for **semantic search & recommendations**.

---

# **Knowledge Cutoff Dates & Search Capabilities**

LLMs rely on training data up to a **cutoff date**, impacting their ability to provide current information.

| **Model**                 | **Knowledge Cutoff**     | **Real-time Search** |
| ------------------------- | ------------------------ | -------------------- |
| **GPT-4o / Mini / Turbo** | **Oct 2023**             | **Yes (Bing)**       |
| **GPT-3.5**               | **Dec 2023**             | **No**               |
| **Claude (Anthropic)**    | **Aug 2023**             | **No**               |
| **Google Gemini**         | **Continuously Updated** | **No**               |
| **Meta AI**               | **Dec 2023**             | **Yes**              |
| **Microsoft Copilot**     | **2021 + Updates**       | **Yes (Bing)**       |

⚡ **Implications**:

- **Outdated Responses**: Models cannot provide post-cutoff knowledge without search access.
- **Enhanced Reliability**: Search-enabled models (e.g., GPT-4o, Copilot) can fetch real-time data.

---

# **OpenAI API Usage (JavaScript)**

## **GPT-4o Example (Text Generation)**

```js
import OpenAI from "openai";

const openai = new OpenAI({ apiKey: "YOUR_API_KEY" });

async function generateText() {
  const response = await openai.chat.completions.create({
    model: "gpt-4o",
    messages: [{ role: "user", content: "Translate 'Hello' to French." }],
    max_tokens: 60,
  });

  console.log(response.choices[0].message.content);
}

generateText();
```

## **DALL·E 3 Example (Image Generation)**

```js
async function generateImage() {
  const response = await openai.images.generate({
    model: "dall-e-3",
    prompt: "A futuristic cityscape at sunset.",
    n: 1,
    size: "1024x1024",
  });

  console.log(response.data[0].url);
}

generateImage();
```

## **Whisper Example (Speech-to-Text)**

```js
async function transcribeAudio() {
  const audioFile = new Blob(["path_to_audio.wav"]);
  const response = await openai.audio.transcriptions.create({
    model: "whisper-1",
    file: audioFile,
  });

  console.log(response.text);
}

transcribeAudio();
```
