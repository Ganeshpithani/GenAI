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

## Day 3 - LLM Generation Control & Prompt Engineering

### What I Learned

- How LLMs generate text token by token
- Parameters to control output behavior
- Writing effective prompts
- Advanced prompting techniques

---

### How LLMs Generate Text

- LLMs generate text one word at a time
- Each word is chosen based on probability

**Two methods:**

- **Greedy** — Picks the highest probability word (safe, repetitive)
- **Sampling** — Picks randomly from probable words (creative, varied)

---

### Temperature (Creativity Control)

Controls how random the output is:

| Temperature | Behavior |
|---|---|
| 0.0 | Same output every time (no creativity) |
| 0.1 – 0.5 | Focused, accurate |
| 0.7 – 1.0 | Balanced |
| 1.0+ | Very creative (can be unpredictable) |

**Rule:** Lower = Safe, Higher = Creative

---

### Top-K Sampling

- Limits choices to the top K most likely words
- Example: `k = 50`

**Problem:** Fixed limit, does not adapt to context.

---

### Top-P (Nucleus Sampling)

- Chooses the smallest set of words whose total probability equals P
- Example: `p = 0.8`

**Why it is better:**

- Adapts to context
- Produces more natural output

---

### Template + Low Temperature

Structured prompts give better results:

```python
Q: {question}
A:
```

Use low temperature (0.1 – 0.3) for clean and repeatable output.

---

### My Experiment

- Default temperature → Output changes each time
- Low temperature (0.1) → Same output repeated

**Conclusion:**

- Low temperature = consistent output
- High temperature = creative output

---

### Key Idea

Temperature + Top-K + Top-P = Full control over AI output

---

### Prompt Engineering

#### Writing Better Prompts

**Bad:**

```
"Tell me about cars"
```

**Good:**

```
"List 3 benefits of electric cars in city driving in bullet points"
```

Clear prompts produce better answers.

---

#### 5 Key Parts of a Good Prompt

- Clear wording
- Short but detailed
- Assign a role
- Define the goal
- Use positive and negative instructions

**Example:**

```
"Act as a friendly teacher. Explain gravity to a 10-year-old. Do NOT use hard words."
```

---

### Advanced Prompting Techniques

#### Zero-Shot Prompting

No examples given:

```
"Translate to Hindi: How are you?"
```

#### Few-Shot Prompting

Provide examples before asking:

```
"happy → positive
sad → negative
excited → ?"
```

#### Chain of Thought (CoT)

Ask the model to think step by step:

```
"Solve 25 + (18 / 3) - 7 step by step"
```

#### Self-Consistency CoT

- Solve the same problem multiple times
- Pick the most common answer

Improves accuracy on reasoning tasks.

#### Tree of Thoughts (ToT)

- Explore multiple solution paths
- Compare and choose the best

```
"Give 3 plans (A, B, C), compare them, and pick the best one"
```

---

### Final Takeaways

- Prompt controls what the AI does
- Temperature controls creativity
- Top-K and Top-P control word selection
- Advanced prompting improves reasoning and accuracy

---

### Summary

Today I learned how to control LLM outputs using temperature, Top-K, Top-P, better prompt writing, and advanced prompting techniques.

**Progress: Day 3 Completed**

**Next: Practical Implementations**

---

## Progress Tracker

| Day | Topic | Status |
|---|---|---|
| 1 | Google GenAI (Gemini) | Completed |
| 2 | Groq LLM Practice | Completed |
| 3 | LLM Generation Control & Prompt Engineering | Completed |
