# Timatch — Website

Produktseite zur Timatch-App, live unter **https://app.timatch.de** — gehostet auf GitHub Pages.

Statisches HTML ohne Build-Schritt, zweisprachig DE/EN. Keine externen Skripte, Styles oder Fonts.

## ⚠️ In App Store Connect umzustellen

Bis August 2026 lief die Seite unter `timatch.jaimetaboada.com`. Diese Adresse wurde aufgegeben. Folgende Felder müssen auf die neue Domain gezogen werden — **auch bei der tvOS-Version**:

| Feld | Sprache | Neue URL |
|---|---|---|
| Marketing URL | EN + DE | `https://app.timatch.de/` |
| Support URL | English (U.S.) | `https://app.timatch.de/support.html` |
| Support URL | Deutsch | `https://app.timatch.de/hilfe.html` |
| Privacy Policy URL | English (U.S.) | `https://app.timatch.de/privacy.html` |
| Privacy Policy URL | Deutsch | `https://app.timatch.de/datenschutz.html` |

Der Apple-TV-Datenschutztext (Volltext, da tvOS keine URLs öffnen kann) nennt die Domain ebenfalls.

## Deployment

Ein Push genügt — GitHub Pages baut selbstständig, rund 30 Sekunden:

```bash
git add -A && git commit -m "..." && git push
```

HTTPS stellt GitHub kostenlos bereit, auch für die eigene Domain, und erneuert das Let's-Encrypt-Zertifikat automatisch.

Die Datei `CNAME` im Root ist Pflicht — Pages liest daraus die Custom Domain. Nicht löschen und nicht umbenennen.

## Struktur

```
index.html        Startseite
hilfe.html        Hilfe (DE)
support.html      Support (EN)
datenschutz.html  Datenschutzerklärung (DE)
privacy.html      Privacy Policy (EN)
style.css         Styles
robots.txt        Crawler-Regeln, KI-Crawler ausgeschlossen
CNAME             Custom Domain für GitHub Pages
```

## DNS

`app.timatch.de` ist ein CNAME auf `jaimetabo.github.io.`, verwaltet im STRATO-Kundenlogin unter dem Paket **TIMATCH** (Auftrag 7070811) → Domains → `timatch.de` → DNS.

Die Domain `timatch.de` selbst bleibt unangetastet und zeigt weiterhin nach Hause.

Alternativ zum CNAME gehen auch vier A-Records auf dieselbe Subdomain — die offiziellen GitHub-Pages-Adressen `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`. Funktional gleichwertig, nur ohne automatische Anpassung, falls GitHub die IPs je ändert. CNAME und A-Record schließen sich gegenseitig aus.

## Warum nicht auf dem STRATO-Webspace?

Das TIMATCH-Paket ist ein reines Domain-Produkt ohne Webspace. Im Webhosting-Paket wäre `app.timatch.de` eine Subdomain — und STRATOs inklusives Zertifikat deckt nur die Hauptdomain plus `www` ab. Für Subdomains verlangt STRATO ein Wildcard-Zertifikat zu 30 €/Monat plus 100 € Einrichtung. GitHub Pages liefert dasselbe kostenlos.

## Vor der App-Store-Einreichung prüfen

1. Alle fünf URLs im Browser öffnen — Apple ruft Support- und Privacy-URL im Review auf und lehnt bei 404 ab.
2. `https://app.timatch.de` muss per HTTPS ohne Zertifikatswarnung laden.

Die Anschrift ist **erledigt**: `privacy.html` und `datenschutz.html` nennen unter „Verantwortlicher" Name und E-Mail und verlinken für die vollständige Anschrift auf `jaimetaboada.com/impressum.html`, wo sie hinterlegt ist. Eine frühere Fassung dieses README behauptete, dort stünden noch Platzhalter in eckigen Klammern — das stimmte nicht.

## Sichtbarkeit

Alle Seiten tragen `<meta name="robots" content="noindex, nofollow">`. Sie sind über den Direktlink erreichbar, landen aber nicht im Google-Index.

Bewusst **kein** `Disallow` in der `robots.txt`: Ein gesperrter Crawler kann die Seite nicht laden und das `noindex` deshalb nie lesen — die URL könnte trotzdem im Index auftauchen. Die `robots.txt` sperrt nur KI-Crawler, analog zur Hauptdomain.

Wenn Timatch später auffindbar sein soll: die fünf `noindex`-Zeilen entfernen, pushen, fertig.

## Kontakt

Alle Kontaktadressen auf der Seite lauten `timatch@jaimetaboada.com`.

## Hinweis

Die Rechtstexte sind am tatsächlichen Codeverhalten der App ausgerichtet, ersetzen aber keine Rechtsberatung.
