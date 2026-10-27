# Domain `tracelight.de` anbinden — DNS-Setup

Ziel: `tracelight.de` zeigt auf die GitHub-Pages-Website **und** trägt die Zoho-Business-Mail.
Voraussetzung: Domain bei einem Registrar gekauft (z. B. INWX, Netcup, Namecheap, ~8 €/Jahr).

> ⚠️ **Reihenfolge wichtig.** Erst die DNS-Records setzen, dann die `CNAME`-Datei aktivieren
> (siehe Schritt C). Aktivierst du die Custom Domain, bevor DNS steht, ist die Seite
> vorübergehend nicht erreichbar.

---

## A) Website — DNS-Records beim Registrar eintragen

Für die nackte Domain (`tracelight.de`) vier A-Records auf die GitHub-Pages-IPs:

| Typ | Name/Host | Wert |
|-----|-----------|------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

Optional zusätzlich IPv6 (AAAA):

| Typ | Name/Host | Wert |
|-----|-----------|------|
| AAAA | @ | 2606:50c0:8000::153 |
| AAAA | @ | 2606:50c0:8001::153 |
| AAAA | @ | 2606:50c0:8002::153 |
| AAAA | @ | 2606:50c0:8003::153 |

Für `www.tracelight.de` ein CNAME auf den GitHub-Pages-Host:

| Typ | Name/Host | Wert |
|-----|-----------|------|
| CNAME | www | rrizeezz7-hub.github.io. |

---

## B) Business-Mail (Zoho Free) — Mail-Records

Die **exakten** Werte zeigt dir Zoho beim Setup (abhängig vom Datacenter EU/US).
Für das EU-Datacenter (zoho.eu) sehen sie typischerweise so aus:

| Typ | Name/Host | Wert | Priorität |
|-----|-----------|------|-----------|
| MX | @ | mx.zoho.eu | 10 |
| MX | @ | mx2.zoho.eu | 20 |
| MX | @ | mx3.zoho.eu | 50 |
| TXT (SPF) | @ | `v=spf1 include:zoho.eu ~all` | — |
| TXT (DKIM) | `<selector>._domainkey` | (Wert aus Zoho-Panel) | — |
| TXT (Verify) | @ | `zoho-verification=...` (aus Zoho) | — |

> Zoho Free: bis 5 Postfächer, 5 GB, 1 Domain. Registrierung: https://www.zoho.com/mail/ → Free Plan.
> EU-Datacenter wählen für deutsche Nutzung. Danach Postfach `kontakt@tracelight.de` anlegen.

---

## C) Custom Domain bei GitHub Pages aktivieren

Erst **nachdem** die A-Records (Schritt A) gesetzt sind und greifen (Prüfung:
`dig tracelight.de +short` → zeigt die vier GitHub-IPs):

```bash
cd ~/tracelight
git mv CNAME.txt CNAME        # Vorlage aktivieren
git add CNAME && git commit -m "chore: custom domain tracelight.de"
git push
```

Dann im Repo: **Settings → Pages → Custom domain** = `tracelight.de` eintragen,
„Enforce HTTPS" aktivieren (nach Zertifikatsausstellung, kann ~1 h dauern).

Zum Schluss in `index.html` den `og:url`-Meta-Tag auf `https://tracelight.de` prüfen (ist schon gesetzt).

---

## Schnellcheck nach Propagation (bis zu 24 h, meist Minuten)
```bash
dig tracelight.de +short          # erwartet: 4× 185.199.10x.153
dig www.tracelight.de +short      # erwartet: rrizeezz7-hub.github.io ...
dig MX tracelight.de +short       # erwartet: mx.zoho.eu etc.
curl -I https://tracelight.de     # erwartet: HTTP/2 200
```
