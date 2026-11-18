# Geschenke-Manager

Webanwendung zur Verwaltung von Personen, Anlässen, Geschenkideen und Geschenken inkl. automatischer E-Mail-Erinnerungen.
Projekt im Kurs „Projekt: Software Engineering“ (IU), Aufgabenstellung E.

## Architektur

| Bereich | Technologie |
|---|---|
| Frontend | HTML5, CSS3, Vanilla JavaScript (kein Framework), modular aufgebaut |
| Backend / DB | Supabase (PostgreSQL, Auth, Row Level Security, Storage, Edge Functions) |
| E-Mail | Brevo Free, angebunden über Edge Functions (API-Key nur serverseitig) |
| Erinnerungen | Supabase Cron → Edge Function → Brevo, Versandprotokolle gegen Doppelversand |
| Hosting | GitHub Pages (Deployment per GitHub Actions) |
| Keepalive | GitHub Actions, regelmäßiger DB-Zugriff gegen Inaktivitätspausierung |

## Ordnerstruktur

```
geschenke-manager/
├── frontend/                 # Wird 1:1 auf GitHub Pages veröffentlicht
│   ├── index.html            # Einstieg / Übersicht
│   ├── pages/                # Weitere Seiten (Personen, Profil, Geschenke, …)
│   ├── css/                  # Stylesheets
│   ├── js/
│   │   ├── api/              # Zentrale API-Schicht (einziger Ort mit Supabase-Zugriff)
│   │   ├── components/       # Wiederverwendbare UI-Bausteine
│   │   └── pages/            # Seitenlogik je HTML-Seite
│   └── assets/img/           # Statische Bilder/Icons
├── supabase/
│   ├── migrations/           # SQL-Migrationen (Schema, RLS-Policies, Storage, Cron)
│   └── functions/            # Edge Functions (Deno/TypeScript)
├── docs/                     # Projektdokumentation, Diagramme
└── .github/workflows/        # Pages-Deployment und Supabase-Keepalive
```

## Lokal starten

Die Seiten in `frontend/` mit einem lokalen Webserver öffnen, z. B. VS Code „Live Server“ oder:

```
cd frontend
python -m http.server 8000
```

## Deployment (GitHub Pages)

Der Workflow `.github/workflows/pages.yml` veröffentlicht bei jedem Push auf `main` den Ordner `frontend/`.
Einmalig nötig: im Repository unter **Settings → Pages → Build and deployment → Source** „GitHub Actions“ auswählen.

## Secrets

Zugangsdaten gehören **nie** ins Repository. `.env`-Dateien sind per `.gitignore` ausgeschlossen.
Benötigte GitHub-Secrets (Settings → Secrets and variables → Actions):

- `SUPABASE_URL` – Projekt-URL
- `SUPABASE_ANON_KEY` – öffentlicher Anon-Key (für den Keepalive)

Der Brevo-API-Key wird ausschließlich als Supabase-Secret für die Edge Functions hinterlegt.

## Zusammenarbeit

Änderungen laufen über Feature-Branches und Pull Requests auf `main`.
