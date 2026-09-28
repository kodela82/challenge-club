# Challenge Club

Een spel met AI-challenges voor kinderen. De website bewaart namen, leeftijden, rondes en scores alleen in de browser (`localStorage`). De Cloudflare Pages Function gebruikt een OpenAI API-key als Cloudflare Secret.

## Publiceren via GitHub en Cloudflare Pages

1. Maak een nieuwe GitHub-repository en voeg de inhoud van deze map toe op het hoogste niveau.
2. Maak in Cloudflare **Workers & Pages → Create → Pages → Connect to Git** een Pages-project met die repository.
3. Kies **Build command:** leeg / geen; **Build output directory:** `.`. De map `functions/api` moet op het hoogste niveau van de repository staan.
4. Voeg in **Settings → Variables and Secrets** de naam `OPENAI_API_KEY` toe, plak je key, kies **Encrypt** en sla op. Herdeploy daarna het project. Eventueel kun je de gewone variabele `OPENAI_MODEL` instellen; standaard is `gpt-4.1-mini`.
5. Test een challenge op de Pages-URL. GitHub mag nooit je API-key of `.dev.vars` bevatten.

## Lokaal testen

Gebruik `npx wrangler pages dev .` vanuit deze map en zet voor lokale tests een `.dev.vars` met `OPENAI_API_KEY=...`. Dit bestand staat in `.gitignore`.

## Grenzen

De app doet per generatie één betaalde OpenAI-aanvraag; een andere challenge vraagt opnieuw een generatie. Punten voor de afgeronde ronde worden geboekt bij **Volgende ronde**. De spelstand is per browser en synchroniseert niet tussen apparaten. De server valideert invoer en controleert enkele risicowoorden in de uitvoer; AI-uitvoer kan alsnog ongepast zijn. Een volwassene blijft bij fysieke challenges toezicht houden. Voor publieke inzet is een limiet per bezoeker via Cloudflare WAF/rate limiting en eventueel een dagbudget op het OpenAI-project verstandig.
