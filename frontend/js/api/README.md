# API-Schicht

Zentrale Schnittstelle zwischen UI und Backend. Nur Dateien in diesem Ordner sprechen mit Supabase
(Auth, Datenbank, Storage, Edge Functions). Seiten und Komponenten rufen ausschließlich Funktionen
aus diesem Ordner auf und kennen keine Supabase-Details.

Mögliche Aufteilung (Vorschlag):

- `client.js` – Initialisierung des Supabase-Clients (URL + Anon-Key)
- `auth.js` – Registrierung, Login, Logout
- `personen.js`, `anlaesse.js`, `geschenke.js`, `aufgaben.js` – CRUD je Entität
