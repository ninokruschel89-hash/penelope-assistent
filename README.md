# Penelope Assistent

Penelope ist ein deploybarer deutschsprachiger KI-Sprachassistent fuer Telefonate und Terminverwaltung.

## Funktionen

- Railway-kompatibler Node.js/Express-Server
- Healthcheck unter `/health`
- OpenAI-Gespraechslogik
- Twilio-Outbound-Anrufe ueber `POST /api/call`
- Transparente Ansage als digitaler Assistent
- Google-Calendar-API fuer Termine auflisten, erstellen, aendern und loeschen
- Calendar-Function-Calling direkt im Telefongespraech
- Explizite Bestaetigung vor Kalenderaenderungen
- Geschuetzte private API-Endpunkte per `ADMIN_TOKEN`
- Geheimnisse nur als Environment Variables

## Railway

Start Command:

```
npm start
```

Healthcheck:

```
/health
```

Railway setzt `PORT` automatisch. Nach dem Deployment die Railway-Domain als `PUBLIC_BASE_URL` eintragen.

## Benoetigte Variablen

Mindestens fuer KI-Gespraeche:

- `OPENAI_API_KEY`
- `OPENAI_MODEL` (Standard: `gpt-5.6-luna`)

Zusaetzlich fuer Telefonate:

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
- `GOOGLE_TIMEZONE`

## Status pruefen

Mit `GET /api/status` und Bearer-`ADMIN_TOKEN` laesst sich pruefen, welche Integrationen konfiguriert sind, ohne Geheimnisse auszugeben.

## Outbound-Anruf starten

```bash
curl -X POST "https://DEINE-DOMAIN/api/call" \
  -H "Authorization: Bearer DEIN_ADMIN_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"to":"+491234567890","purpose":"Vereinbare einen Termin fuer naechste Woche."}'
```

## Sicherheit

Keine API-Keys oder OAuth-Geheimnisse in GitHub eintragen. Geheimnisse gehoeren nur in Railway Variables.
