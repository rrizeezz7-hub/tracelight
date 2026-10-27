# Tracelight — Firma online bringen (kostenlos)

Stand: 2026-10-27. Marke: **Tracelight** · Feld: OSINT- & Attack-Surface-Beratung.

Diese Datei ist die Checkliste. Reihenfolge ist egal, außer: Domain **vor** Business-Mail.

---

## Was schon fertig ist
- **Name + Logo:** Tracelight, Wortmarke + Scope-Icon (inline SVG in `index.html`, auch als Favicon).
- **Website:** `index.html` — fertige, responsive Landingpage (Hell/Dunkel), noch lokal.
- **Platzhalter:** Kontakt-Mail `kontakt@tracelight.de`, Impressum/Datenschutz-Links → noch leer.

---

## 1. Website öffentlich schalten (0 €, ~3 Min)

### Weg A — Netlify Drop (am schnellsten, keine Anmeldung nötig)
1. https://app.netlify.com/drop öffnen.
2. Den **Ordner `~/tracelight`** ins Fenster ziehen.
3. Fertig → du bekommst sofort eine echte URL wie `random-name.netlify.app`.
4. Kostenloses Konto anlegen, um die URL zu behalten + Namen zu ändern (`tracelight.netlify.app`).

### Weg B — GitHub Pages (versioniert, gut wenn du eh GitHub nutzt)
```bash
cd ~/tracelight
git init && git add . && git commit -m "Tracelight site"
gh repo create tracelight --public --source=. --push
```
Dann im Repo: **Settings → Pages → Branch `main` / root** → URL `deinuser.github.io/tracelight`.

### Weg C — Cloudflare Pages
Konto → Pages → Ordner hochladen. URL `tracelight.pages.dev`. (Bonus: gleicher Anbieter kann später Domain + DNS.)

> Alle drei: HTTPS inklusive, 0 €, unbegrenzt für eine statische Seite.

---

## 2. Business-Mail `name@tracelight.de` (0 € Mailhosting)

Eine echte `@firma`-Adresse braucht eine eigene Domain (siehe Schritt 3). Das **Mailhosting selbst** ist gratis:

### Zoho Mail — Free Forever
1. https://www.zoho.com/mail/ → **Free Plan** (bis 5 Postfächer, 5 GB, 1 Domain).
2. Domain `tracelight.de` angeben → Zoho zeigt dir **MX-, TXT- (SPF), DKIM-Records**.
3. Diese Records beim Domain-Anbieter (Schritt 3) in die DNS eintragen.
4. Postfach anlegen: `kontakt@tracelight.de`. Webmail + IMAP/SMTP für Mail-App.

**Alternativen:** Infomaniak (kostenlos, EU/CH, datenschutzfreundlich) · Proton Mail (eigene Domain erst ab Bezahlplan; kostenlos nur `@proton.me`).

> **Komplett ohne Domain / 0 €:** vorerst `tracelight.osint@proton.me` o. ä. nutzen und später auf die eigene Domain umziehen. Wirkt weniger professionell, kostet aber nichts.

---

## 3. Domain (optional, ~1 €/Monat — der einzige kleine Posten)

Frei geprüft am 2026-10-27:
- `tracelight.de` ✅ frei — ~5–10 €/Jahr (INWX, Netcup, Namecheap)
- `tracelight.io` ✅ frei — ~35–45 €/Jahr (teurer, „Tech"-Image)
- `tracelight.com` ❌ vergeben

Empfehlung: **tracelight.de** (günstig + trägt die Zoho-Mail). Nach Kauf:
- A-/CNAME-Record auf dein Hosting (Netlify/Pages) zeigen → Seite läuft unter `tracelight.de`.
- MX/TXT-Records von Zoho → Mail läuft.

**Echt-kostenlos-Variante:** `nic.eu.org` vergibt kostenlose Domains, aber Freigabe dauert Wochen und wirkt weniger seriös. Für den Start reicht die Gratis-Subdomain aus Schritt 1.

---

## 4. Social-Handles sichern (0 €)
Einheitlich `@tracelight` bzw. `tracelightsec` reservieren, bevor es jemand anderes tut:
- LinkedIn **Unternehmensseite** (wichtigster Kanal für B2B-Security)
- GitHub-Org `tracelight` (Code/Tools = Glaubwürdigkeit)
- X / Mastodon (infosec.exchange) optional
Verfügbarkeit vorher prüfen: https://namechk.com

---

## 5. Rechtliches — ehrlich (DE)
Kostenlos baubar ist die **Präsenz**. Sobald du geschäftlich (gegen Geld) tätig wirst, gilt:
- **Impressumspflicht** (§ 5 DDG): Name, Anschrift, Kontakt. Generator: e-recht24.de (kostenlos). → `impressum.html` füllen.
- **Datenschutzerklärung** (DSGVO), sobald die Seite Daten verarbeitet (z. B. Kontaktformular, Hosting-Logs). → `datenschutz.html`.
- **Gewerbeanmeldung** (~20–60 € einmalig) ODER Einstufung als Freiberufler (Beratung kann freiberuflich sein — Finanzamt/Steuerberater klärt das). Das ist die **einzige** nicht-kostenlose Pflicht, falls du echt abrechnest.
- **Markenrecherche** vor ernster Nutzung: DPMA (register.dpma.de) und EUIPO auf „Tracelight" prüfen — der Name darf keine bestehende Marke verletzen.

> Für reinen Marken-/Portfolioaufbau ohne Rechnungen brauchst du Gewerbe/Impressum noch nicht. Für echte Kundenaufträge schon.

---

## Reihenfolge, wenn du es „richtig" willst
1. Domain `tracelight.de` kaufen (~8 €/Jahr)
2. Netlify/Pages-Site mit der Domain verbinden
3. Zoho-Mail einrichten (`kontakt@tracelight.de`)
4. LinkedIn + GitHub-Org anlegen
5. Impressum + Datenschutz füllen
6. Markenrecherche DPMA/EUIPO
→ Laufende Kosten: nur die Domain. Alles andere 0 €.
