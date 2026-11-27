# Iron Fight Boxing Club
Fictieve oefenwebsite voor Software Developer. HTML, CSS, JavaScript en Supabase (geen PHP of React).

## Starten
1. Open de map `iron-fight-boxing` in VS Code. Installeer Live Server (Ritwick Dey) indien nodig.
2. Maak een nieuw Supabase-project aan op https://supabase.com/dashboard. Bewaar het databasewachtwoord privé.
3. Open SQL Editor > New query, plak de volledige inhoud van `supabase/schema.sql` en klik Run. Controleer in Table Editor dat `training_sessions` zes rijen bevat en `trial_requests` leeg is. Controleer dat beide tabellen via de Data API toegankelijk zijn voor de bedoelde rollen (zie SQL-grants). Laat RLS aan.
4. Open Connect / Project Settings > API Keys en kopieer de Project URL en publishable key (`sb_publishable_...`). Vul ze in `js/config.js` in. Gebruik nooit een secret of service_role key. De client accepteert alleen de moderne publishable key.
5. Rechtsklik op `index.html` > Open with Live Server. Gebruik consequent dezelfde host en poort. Bijvoorbeeld `http://127.0.0.1:5500/index.html`.
6. In Supabase Authentication > URL Configuration: stel Site URL in op `http://127.0.0.1:5500` en voeg `http://127.0.0.1:5500/dashboard.html` toe bij Redirect URLs. Pas beide aan op de echte URL die Live Server toont (inclusief eventueel pad). Zet Email provider aan, laat e-mailbevestiging aan en stel minimaal 8 wachtwoordtekens in. Voor echte bevestigingsmail naar externe testadressen is doorgaans een eigen SMTP-configuratie nodig. Voor uitsluitend lokale oefening met fictieve accounts kan e-mailbevestiging tijdelijk worden uitgezet; zet die voor publicatie weer aan.
7. Test alle functies. Zonder configuratie werkt de publieke homepagina, maar toont het lesrooster een configuratiefout en worden formulieren niet verstuurd.

## Testplan (uit te voeren)
- Home: alle navigatielinks openen de juiste pagina; trainingsknoppen openen een passend gefilterd rooster.
- Rooster: 6 rijen, filter Maandag → 1 rij, Thaiboksen → 2 rijen, Maandag + Thaiboksen → 0 rijen, reset → 6.
- Proefles: lege/ongeldige velden → fout; geldige fictieve aanvraag → bevestiging + rij in `trial_requests` (controle via beheerder).
- Registratie: afwijkend wachtwoord → fout; geldig account → bevestigingsmail of dashboard, afhankelijk van instellingen.
- Login: onjuist wachtwoord → fout; geldig bevestigd account → dashboard.
- Dashboard: directe toegang zonder sessie → login; ingelogd → eigen naam en e-mail; uitloggen → login.
- RLS: browserrollen anon/authenticated kunnen rooster lezen, alleen toegestane aanvraagvelden invoegen, geen aanvragen lezen/wijzigen/verwijderen. Beheerder controleert policies en grants. Test met publieke client, niet alleen SQL Editor (die heeft beheerrechten).
- Mobile: 390px breed; menu opent/sluit; kaarten stapelen; tabel scrollt horizontaal binnen zijn container.
- Verbreek internet of gebruik een onjuiste projectconfiguratie: duidelijke foutmelding.

## Aandachtspunten voor publicatie
Dit is een oefenproject, geen productieklare ledendienst. Gebruik fictieve gegevens. Publieke aanvragen zijn insert-only, maar kunnen door bots worden misbruikt: voeg voor publicatie server-side spambeveiliging/rate limiting toe (bijvoorbeeld een Edge Function met CAPTCHA en schakel publieke directe INSERT uit). Gebruik HTTPS, echte contact- en privacyinformatie, passende bewaartermijnen, eigen SMTP, en verifieer RLS en authenticatie in het echte project. De privacytekst is een oefentekst. Foto's zijn vervangen door grafische placeholders; trainers en lestijden zijn voorbeelddata. Er is geen wachtwoordherstelfunctie, beheerportaal of automatische proeflesmail in deze eerste versie.

## Versiebeheer en bewijs
Maak GitHub issues van user stories, ontwikkel via feature-branches en merge via pull requests. Maak zelf echte screenshots van de eigen functionaliteiten, code, tests en git-geschiedenis; zet geen echte persoonsgegevens of geheime sleutels in screenshots. De code is een leerbasis: Rayyan moet zelf de werking begrijpen, aanpassen en verantwoorden.
