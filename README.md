# GenAI Learning Journey

Daily progress tracking my journey with Generative AI models and APIs.

---

## Day 1 - Getting Started with Google GenAI (Gemini)

### What I Learned

- Install Google GenAI SDK
- Connect to Gemini API
- Why API keys are required
- Best practice: Store API keys in environment variables
- Generate responses using Gemini model

---

### Installation

```bash
pip install google-genai
```

---

### Setting Up API Key

#### Wrong Way (Not Recommended)

```python
from google import genai
client = genai.Client(api_key="YOUR_API_KEY")
```

#### Correct Way (Recommended)

```python
import os
os.environ["GEMINI_API_KEY"] = "YOUR_API_KEY"
```

**Why?**

- Keeps your key safe
- Avoids exposing it in code
- Standard industry practice

---

### Creating Client

```python
from google import genai
client = genai.Client()  # Works if API key is set correctly
```

---

### Generating Response

```python
response = client.models.generate_content(
    model="gemini-2.5-flash",
    contents="What are advantages of Gemini LLM?"
)
print(response.text)
```

---

### Common Error

```text
ValueError: No API key was provided
```

**Fix:** Set the environment variable before creating the client.

---

### Key Concepts

| Concept | Simple Explanation |
|---|---|
| Client | Connects your code to Gemini server |
| API Key | Acts like a password |
| Model | Brain (gemini-2.5-flash) |
| Prompt | Your question |

---

### Why Gemini?

- Supports text, image, audio (multimodal)
- Strong reasoning and coding ability
- Integrated with Google ecosystem
- Multiple models (Ultra, Pro, Flash, Nano)

---

**Progress: Day 1 Completed**

**Next: Prompt Engineering**

---

## Day 2 - Groq LLM Practice

### What I Did

- Switched from Gemini to Groq LLM models
- Used `openai/gpt-oss-120b` model
- Implemented chat-based API (`chat.completions`)
- Used system prompt to control response length
- Extracted clean output from response object
- Displayed output using Markdown in Colab

---

### Generating Response (Groq)

```python
response = client.chat.completions.create(
    messages=[
        {
            "role": "user",
            "content": "What are the advantages of generative AI?"
        },
        {
            "role": "system",
            "content": "Respond to user queries concisely"
        }
    ],
    model="openai/gpt-oss-120b"
)
```

---

### Extracting Clean Output

```python
print(response.choices[0].message.content)
```

**Why?** Removes unnecessary metadata, gives only the actual model response.

---

### Displaying Output (Formatted)

```python
from IPython.display import Markdown
Markdown(response.choices[0].message.content)
```

**Why?** Shows clean Markdown format and improves readability.

---

### Key Learning

- Large models = better reasoning but longer responses
- System prompt = controls output length and style
- Response object contains metadata (extract the useful part)
- Markdown improves output readability

---

### Observation

- Model initially returned very large responses
- After adding system prompt, output became concise
- Output was structured with bullet points and headings
- Better prompts = better control

---

## Progress Tracker

| Day | Topic | Status |
|---|---|---|
| 1 | Google GenAI (Gemini) | Completed |
| 2 | Groq LLM Practice | Completed |
