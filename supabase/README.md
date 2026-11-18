# Supabase

- `migrations/` – SQL-Migrationen in zeitlicher Reihenfolge (`supabase migration new <name>`):
  Tabellen (Benutzer, Personen, Anlässe, Geschenkideen, Geschenke, Aufgaben, Versandprotokolle),
  RLS-Policies, Storage-Bucket für Geschenkbilder, Cron-Jobs.
- `functions/` – Edge Functions, z. B. Erinnerungsversand über die Brevo API.

Secrets für Edge Functions (z. B. `BREVO_API_KEY`) werden mit `supabase secrets set` hinterlegt,
lokal in `supabase/functions/.env` (nicht eingecheckt).
