# ComicCraft – AI Comic Story Creator

ComicCraft is a FastAPI web application that turns a user's story idea into a five-panel comic.

## Project flow

1. User enters story prompt, character, setting, tone and art style.
2. Gemini Flash generates a structured five-panel outline.
3. Gemini Pro expands the outline into narration and dialogue.
4. Stable Diffusion generates an illustration for each panel.
5. The layout builder combines text and images.
6. FPDF creates a downloadable PDF.
7. Jinja2 displays the comic preview.

## Folder structure

```text
ComicCraft/
│
├── app/
│   ├── __init__.py
│   ├── main.py
│   ├── config.py
│   ├── schemas.py
│   ├── gemini_client.py
│   ├── gemini_flash.py
│   ├── gemini_pro.py
│   ├── image_generator.py
│   ├── layout_builder.py
│   ├── exporters.py
│   └── routes.py
│
├── templates/
│   ├── base.html
│   ├── index.html
│   ├── comic_preview.html
│   └── export_success.html
│
├── static/
│   ├── css/
│   │   └── style.css
│   └── panels/
│
├── exports/
├── .env.example
├── .gitignore
├── requirements.txt
└── README.md
```

## Windows setup

```powershell
python -m venv comiccraft-env
comiccraft-env\Scripts\activate
pip install -r requirements.txt
copy .env.example .env
```

Edit `.env` and add your Gemini API key.

Then start the server:

```powershell
uvicorn app.main:app --reload
```

Open:

```text
http://127.0.0.1:8000
```

API documentation:

```text
http://127.0.0.1:8000/docs
```

## If your computer cannot run Stable Diffusion locally

Set:

```text
IMAGE_PROVIDER=placeholder
```

The application will still demonstrate the complete workflow using generated placeholder panel images. Later, change it back to `local` when your environment is ready for Diffusers.

## JSON API example

POST to `/generate-comic/json`:

```json
{
  "prompt": "A brave fox exploring an enchanted forest.",
  "character_name": "Finn",
  "setting": "An enchanted forest",
  "tone": "adventure",
  "art_style": "comic book"
}
```
