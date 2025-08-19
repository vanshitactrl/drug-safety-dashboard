# Drug & Beauty Safety Explorer (North America)

**Goal (simple words):** Show people the **ingredients** in medicines and beauty products and the **common side effects** reported in the US & Canada — so they can compare before buying.

> This is **not medical advice**. It’s an information tool. Always talk to a professional for health decisions.

## What we will build (very short)
- A small website/app to **search a product or ingredient**.
- It shows **ingredients**, **top side effects** (from labels + official reports), and **rule flags** (e.g., restricted ingredients).
- Clear badges: 🟢 OK • 🟡 Be careful • 🔴 Maybe avoid.

---

## Step 0 – Set up (you are here)

### 1) Things to install (once)
- **Python 3.11+**
- (Optional) **Git** (to track changes)
- (Optional) **Docker Desktop** (we’ll add containers later)

### 2) Make a Python environment (simple)
Windows:
```bat
python -m venv .venv
.venv\Scripts\activate
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Mac/Linux:
```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 3) Copy settings file
Make your .env file:
```bash
cp .env.example .env   # on Windows: copy .env.example .env
```

### 4) Test everything works
Run the tiny demo pages:

**Streamlit UI**
```bash
streamlit run src/ui/streamlit_app.py
```
Open the link it prints (usually http://localhost:8501). You should see “Setup complete”.

**FastAPI (backend)**
```bash
uvicorn src.api.main:app --reload --port 8000
```
Open http://localhost:8000/health – it should say `{"status":"ok"}`.

If these work, **Step 0 is done** ✅

---

## Folder map (simple)
```
drug-safety-explorer/
├─ .env.example      # sample secrets/settings (copy to .env)
├─ requirements.txt  # Python packages
├─ README.md         # this guide
├─ PRIVACY.md        # what we do with data
├─ SECURITY.md       # safety rules for data
├─ LICENSE           # MIT license
├─ .gitignore        # files Git should ignore
├─ config/
│  └─ settings.example.yaml
├─ data/             # data lives here (not in Git)
│  ├─ raw/.gitkeep
│  ├─ external/.gitkeep
│  └─ processed/.gitkeep
├─ docs/
│  ├─ 01-overview.md
│  └─ data-sources.md
├─ scripts/
│  └─ check_env.py
└─ src/
   ├─ api/main.py
   ├─ common/config.py
   ├─ ingest/README.md
   ├─ normalize/README.md
   ├─ scoring/README.md
   └─ ui/streamlit_app.py
```

## Naming rules (plain)
- Files/folders: **lowercase**, words with `-` or `_` (e.g., `side-effects.csv`).
- Python code: snake_case for files and functions, PascalCase for classes.
- Commits: start with a tag like `setup:`, `data:`, `fix:`, `feat:`, e.g., `feat: add CAERS loader skeleton`.

## Next steps
- **Step 1:** Pull the official catalogs (RxNorm + DPD) and prepare the product/ingredient tables.
- **Step 2:** Read drug labels (DailyMed) and store the side-effect sections.
- **Step 3:** Load adverse event reports (FAERS, Canada Vigilance, CAERS).
- **Step 4:** Add scoring & flags, then make the product cards.
- **Step 5:** Polish the UI (search, compare, filters).
