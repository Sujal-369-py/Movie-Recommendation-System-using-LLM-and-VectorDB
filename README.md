# 🎬 Movie Recommendation System (Real World Version)

This project started as a **semantic movie recommendation system**
and ended as a **lesson in real-world engineering pain**.

Nothing here is fake.
Every decision was forced by constraints, limits, crashes, and reality.

---

## What this project DOES

- Takes a natural language movie query
- Refines it using an LLM (Groq)
- Searches movies using lightweight logic
- Returns relevant movie recommendations
- Runs on **free-tier deployment**

---

## What this project WAS SUPPOSED TO BE

Originally:
- Sentence Transformers
- 384-dim embeddings
- Cosine similarity
- Proper vector search

It worked **locally**.

It FAILED in production.

---

## Problems I Faced (Important)

### 1. Memory Limits (Biggest Issue)
- Render free tier = **512 MB RAM**
- `sentence-transformers + torch` exceeded memory
- Even lazy-loading caused **OOM crashes**

➡️ Solution:
- Disabled runtime embeddings
- Removed torch from production

---

### 2. Embedding APIs Are Not Free Forever
I tried:
- HuggingFace Inference API → **410 Gone**
- Cohere → **rate limited (1000 calls/month)**
- OpenAI → **paid**

➡️ Lesson:
Free APIs change policies.
You cannot depend on them blindly.

---

### 3. Python Version Hell
- Render default Python = **3.13**
- Torch does NOT support 3.13
- Build failed repeatedly

➡️ Solution:
- Forced Python 3.11
- Still hit memory limits later

---

### 4. Reality Check
You CANNOT:
- Generate semantic embeddings
- Without a model
- Without memory
- Without paying

This is not a tooling issue.
This is **ML reality**.

---

## Final Architecture (What Actually Works)

### Offline / Development
- Movie embeddings were generated locally
- Heavy ML only used where resources exist

### Production (Render Free Tier)
- No sentence-transformers
- No torch
- No vector generation at runtime
- Keyword-based scoring search
- LLM used only for **query refinement**

This system **DEPLOYS SUCCESSFULLY**.

---

## Current Search Logic (Production Safe)

- Break query into keywords
- Match against movie title + plot
- Score by keyword frequency
- Sort results
- Return top 10

Simple.
Fast.
Reliable.
Deployable.

---

## Tech Stack

### Backend
- Python
- FastAPI
- Groq LLM (query refinement)
- JSON + Gzip movie dataset

### Frontend
- HTML
- CSS
- JavaScript
- Served via FastAPI static files

---

## Why This Project Is Still Valuable

This project shows:
- You understand **semantic search**
- You understand **embeddings**
- You understand **deployment constraints**
- You can **adapt instead of quitting**

Most projects online skip this part.
This one doesn’t.

---

## How To Explain This In Interview

Say this:

> “I built a semantic recommendation system using embeddings,
> but optimized it to a lightweight keyword-based search for free-tier deployment.
> The architecture is scalable and embeddings can be re-enabled
> in higher-resource environments.”

That answer is **correct**.

---

## Future Improvements (If Resources Allow)

- Enable vector search with FAISS
- Move embeddings to separate service
- Upgrade deployment memory
- Add hybrid keyword + vector scoring
- Add user profiles

---

## Final Note

This project taught me more than tutorials ever could.

If you are reading this:
- Yes, things broke
- Yes, I got stuck
- Yes, I fixed it

That is engineering.

---

## License
MIT  
Do whatever you want.
Just don’t pretend this was easy.
