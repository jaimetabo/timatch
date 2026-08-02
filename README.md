# Timatch — Website

Läuft unter **https://timatch.jaimetaboada.com** — Subdomain bei STRATO, gehostet auf GitHub Pages.

## Eingetragene URLs in App Store Connect

| Feld | Sprache | URL |
|---|---|---|
| Marketing URL | EN + DE | `https://timatch.jaimetaboada.com/` |
| Support URL | English (U.S.) | `https://timatch.jaimetaboada.com/support.html` |
| Support URL | Deutsch | `https://timatch.jaimetaboada.com/hilfe.html` |
| Privacy Policy URL | English (U.S.) | `https://timatch.jaimetaboada.com/privacy.html` |
| Privacy Policy URL | Deutsch | `https://timatch.jaimetaboada.com/datenschutz.html` |

Dieselben URLs sind auch bei der tvOS-Version hinterlegt. Der Apple-TV-Datenschutztext (Volltext, da tvOS keine URLs öffnen kann) verweist ebenfalls auf diese Domain.

---

## Einrichtung — drei Schritte

### 1. Repository anlegen und pushen

```bash
cd timatch-website
git init
git add .
git commit -m "Timatch website"
git branch -M main
git remote add origin https://github.com/jaimetabo/timatch.git
git push -u origin main
```

Die Datei `CNAME` im Root ist Pflicht — GitHub Pages liest daraus die Custom Domain. Nicht löschen und nicht umbenennen.

### 2. DNS bei STRATO

STRATO-Kundenlogin → **Domains** → **Domainverwaltung** → `jaimetaboada.com` → **Verwaltung / DNS-Einstellungen**.

Neuen Eintrag anlegen:

| Typ | Name | Ziel |
|---|---|---|
| CNAME | `timatch` | `jaimetabo.github.io.` |

Der Punkt am Ende gehört dazu, falls STRATO ihn verlangt.

**Falls STRATO für diese Subdomain kein CNAME zulässt** (kommt vor, wenn die Subdomain zuvor als Webspace-Subdomain angelegt wurde): stattdessen vier A-Records auf dieselbe Subdomain:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

Das sind die offiziellen GitHub-Pages-Adressen. Funktional gleichwertig, nur ohne automatische Anpassung, falls GitHub die IPs je ändert.

Wichtig: Für `timatch` darf **kein** paralleler A-/AAAA-Eintrag auf `81.169.145.92` (STRATO-Webspace) stehen. CNAME und A-Record schließen sich gegenseitig aus.

### 3. GitHub Pages aktivieren

Repository → **Settings** → **Pages**

- Source: *Deploy from a branch* → Branch `main`, Ordner `/ (root)`
- Custom domain: `timatch.jaimetaboada.com` → **Save**
- Warten, bis der DNS-Check grün ist (kann bis zu einer Stunde dauern), dann **Enforce HTTPS** aktivieren

GitHub stellt automatisch ein Let's-Encrypt-Zertifikat aus und erneuert es selbstständig.

---

## Vor der App-Store-Einreichung prüfen

1. Alle fünf URLs im Browser öffnen — Apple ruft Support- und Privacy-URL im Review auf und lehnt bei 404 ab.
2. `https://timatch.jaimetaboada.com` muss per **HTTPS** ohne Zertifikatswarnung laden.
3. **Postanschrift eintragen:** In `privacy.html` und `datenschutz.html` steht die Adresse noch in eckigen Klammern. Ladungsfähige Anschrift nach Art. 13 DSGVO, bei kostenpflichtigem Angebot zusätzlich § 5 DDG.

## Sichtbarkeit

Alle Seiten tragen `<meta name="robots" content="noindex, nofollow">`. Sie sind über den Direktlink erreichbar, landen aber nicht im Google-Index, und von `jaimetaboada.com` führt kein Link hierher.

Bewusst **kein** `Disallow` in der `robots.txt`: Ein gesperrter Crawler kann die Seite nicht laden und das `noindex` deshalb nie lesen — die URL könnte trotzdem im Index auftauchen. Die `robots.txt` sperrt nur KI-Crawler, analog zu deiner Hauptdomain.

Wenn Timatch später auffindbar sein soll: die fünf `noindex`-Zeilen entfernen, pushen, fertig.

## Hinweis

Die Rechtstexte sind am tatsächlichen Codeverhalten der App ausgerichtet, ersetzen aber keine Rechtsberatung.
