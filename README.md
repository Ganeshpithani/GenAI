#  Day 1 - Getting Started with Google GenAI (Gemini)

##  What I Learned

* How to install Google GenAI SDK
* How to connect to Gemini API
* Why API keys are required
* Best practice to store API keys (environment variables)
* How to generate responses using Gemini model

---

## ⚙️ Installation

```bash
pip install google-genai
```

---

##  Setting Up API Key

###  Wrong Way (Not Recommended)

Directly passing API key:

```python
from google import genai

client = genai.Client(api_key="YOUR_API_KEY")
```

###  Correct Way (Recommended)

Store API key as environment variable:

```python
import os

os.environ["GEMINI_API_KEY"] = "YOUR_API_KEY"
```

 Why?

* Keeps your key safe
* Avoids exposing it in code
* Standard industry practice

---

##  Creating Client

```python
from google import genai

client = genai.Client()
```

 If API key is set correctly, client works without error.

---

##  Generating Response

```python
response = client.models.generate_content(
    model="gemini-2.5-flash",
    contents="What are advantages of Gemini LLM?"
)

print(response.text)
```

---

##  Common Error

```bash
ValueError: No API key was provided
```

 Reason:

* You didn’t set API key

 Fix:

* Set environment variable before creating client

---

##  Key Concept (Simple Understanding)

* **Client** → connects your code to Gemini server
* **API Key** → acts like password
* **Model** → brain (Gemini-2.5-flash)
* **Prompt (contents)** → your question

---

##  What is Special About Gemini?

* Works with text, image, audio (multimodal)
* Strong reasoning + coding ability
* Integrated with Google ecosystem
* Different models (Ultra, Pro, Flash, Nano)

---

## 📅 Progress

✔️ Day 1 Completed
➡️ Next: Learn prompt engineering

---

## 🧑‍💻 Author

Ganesh
