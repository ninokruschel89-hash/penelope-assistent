# Penelope Assistent

Penelope ist ein deploybarer KI-Sprachassistent fuer Telefonate und Terminverwaltung.

## Bereits enthalten

- Railway-kompatibler Node.js/Express-Server
- Healthcheck unter `/health`
- OpenAI-Gespraechslogik
- Twilio-Outbound-Anrufe ueber `POST /api/call`
- Twilio-Sprachdialog auf Deutsch
- Google-Calendar-API fuer Termine auflisten, erstellen, aendern und loeschen
- Schutz der privaten API-Endpunkte per `ADMIN_TOKEN`
- Alle Geheimnisse ausschliesslich als Environment Variables

## Railway

Start Command:

```
npm start
```

Railway setzt `PORT` automatisch.

Nach dem ersten erfolgreichen Deployment eine Railway-Domain erzeugen und diese als `PUBLIC_BASE_URL` eintragen, zum Beispiel:

```
https://penelope-production.up.railway.app
```

## Benoetigte Variablen

Siehe `.env.example`.

Mindestens fuer Telefonate:

- `OPENAI_API_KEY`
- `TWILIO_ACCOUNT_SID`
- `TWILIO_AUTH_TOKEN`
- `TWILIO_PHONE_NUMBER`
- `PUBLIC_BASE_URL`
- `ADMIN_TOKEN`

Zusaetzlich fuer Google Calendar:

- `GOOGLE_CLIENT_ID`
- `GOOGLE_CLIENT_SECRET`
- `GOOGLE_REFRESH_TOKEN`
- `GOOGLE_CALENDAR_ID`

## Outbound-Anruf starten

```bash
curl -X POST "https://DEINE-DOMAIN/api/call" \
  -H "Authorization: Bearer DEIN_ADMIN_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"to":"+491234567890","purpose":"Vereinbare einen Termin fuer naechste Woche."}'
```

## Sicherheit

Keine API-Keys in GitHub eintragen. Geheimnisse gehoeren nur in Railway Variables.
