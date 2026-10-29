# Website La Main

> ## ⚠️ DE SITE STAAT NIET ONLINE (29-10-2026)
>
> Op `la-main.nl` staat een "binnenkort online"-pagina met alleen het logo en
> `noindex`. De mappen `foto/` en `video/` zijn uit deze map gehaald, zodat er
> geen beeldmateriaal meer publiek staat.
>
> **`index.html` in deze map is dus NIET de site** — het is die ene pagina. De
> echte site staat ongewijzigd in `la-main-opzetjes\pagina-h\index.html` en in
> de geschiedenis op commit `4dfb1d1`.
>
> **Weer online, één commando:**
>
> ```powershell
> powershell C:\Users\Robbi\Projects\la-main-opzetjes\bron\weer-online.ps1
> ```
>
> Dat bouwt, controleert en pusht. Met `-droog` bouwt hij alleen.
> Terug naar de binnenkort-pagina gaat met `bron\offline.ps1`.
>
> **Alleen doen als Robbie er uitdrukkelijk om vraagt.**
>
> Domein, HTTPS en de mail op `info@la-main.nl` zijn niet geraakt.
> **Let op: `cal.com/la-main` staat nog wél publiek** — daar kan nog geboekt
> worden. Wil je dat ook stil, verberg dan de drie afspraaktypen in Cal.com.

De site van La Main, massage in Eindhoven en Nuenen. Eén pagina met een
afspraakplanner. Geen framework en geen bouwstap: `index.html` openen en het
werkt.

Online: **https://la-main.nl** (www stuurt door naar het hoofdadres, HTTPS staat
aan, zoekmachines mogen erin sinds 09-10-2026).

| Bestand | Wat het is |
|---|---|
| `index.html` | De hele pagina: opmaak, teksten en de planner. |
| `foto/` | Veertien beelden uit de eigen fotoshoot van 15-10-2026. |
| `video/` | `la-main.mp4`: de film van 40 seconden met geluid (720x1280, 6,9 MB) plus het stilstaande beeld ervoor. `kop-telefoon.mp4`: de eerste 10 seconden zonder geluid (0,9 MB) voor de kop op de telefoon. |
| `Shoot/` | De onbewerkte bestanden van de shoot: 111 foto's en twee films, samen 2,7 GB. Staat in `.gitignore` en gaat dus **niet** mee naar GitHub. |
| `lettertypes/` + `lettertypes.css` | Prata, Cormorant Garamond en Montserrat, in de site zelf. Er wordt niets bij Google opgehaald. |
| `CNAME` | `la-main.nl`, zodat GitHub Pages het eigen adres gebruikt. |

## Wijzigen en publiceren

De pagina wordt gebouwd uit de werkversie in
`C:\Users\Robbi\Projects\la-main-opzetjes\pagina-h\index.html`. Daar wijzig je,
nooit rechtstreeks in deze map:

```powershell
C:\Users\Robbi\Projects\la-main-opzetjes\bron\bouw-site.ps1 -vindbaar
git -C C:\Users\Robbi\Projects\la-main-nl add -A
git -C C:\Users\Robbi\Projects\la-main-nl commit -m "beschrijving"
git -C C:\Users\Robbi\Projects\la-main-nl push
```

`-vindbaar` hoort er altijd bij; zonder die vlag komt de regel `noindex` terug
en valt de site uit Google. Na ongeveer een minuut staat het online. Pushen gaat
met een eigen sleutel (`~/.ssh/la-main`), die als implementatiesleutel met
schrijfrechten in de repository staat. Daardoor is er geen wachtwoord of token
nodig.

## Mail

`info@la-main.nl` loopt via **iCloud+ met een eigen domein**, op het Apple-ID van
Danny. MX, SPF, DKIM en de controlecode staan bij Mijndomein in de DNS. DMARC
staat op `p=none`: meekijken, nog niets weigeren.

## Boeken: de planner en Cal.com

**Werkt sinds 26-10-2026.** De pagina rekent zelf niets vast. Hij bepaalt de
massage, de duur en, bij op locatie, de reistijd en reiskosten op postcode, en
stuurt de klant daarna door naar Cal.com. Daar kiest de klant dag en tijd, en de
afspraak komt in de agenda **Werk** van Danny (iCloud). Zij beheert haar agenda
dus zelf.

| Afspraaktype | URL | Dagen en tijden | Marge vooraf | Marge erna |
|---|---|---|---|---|
| Salon Eindhoven | `salon-eindhoven` | ma, wo 09:00 – 17:00 | — | 15 min |
| Salon Nuenen | `salon-nuenen` | di 09:00 – 17:00 | — | 15 min |
| Op locatie | `op-locatie` | ma, di, wo 19:00 – 22:00 · do 09:00 – 17:00 én 19:00 – 22:00 · vr 09:00 – 17:00 | 30 min | 30 min |

Weekenden dicht. Minimaal 12 uur van tevoren boeken. Alle drie vragen om naam,
e-mail, **telefoonnummer (verplicht)** en **welke massage**. Op locatie vraagt
daarnaast **voor wie** en moet Danny elke aanvraag zelf goedkeuren
(*Vereist bevestiging* staat aan).

- Eén afspraaktype per plek. De site geeft de gekozen duur mee als
  `?duration=`, de berekening als `?notes=` en bij op locatie het adres van de
  klant als `?location=`.
- Op locatie kan 60 tot 240 minuten, zodat een **stel** twee behandelingen na
  elkaar kan nemen zonder dat ze twee keer rijdt.
- Gratis abonnement volstaat. Het logo van Cal.com blijft onderaan staan.
- Cal.com rekent **niets** met reisafstand. De marges hierboven zijn vast.
- **Geen vragen over gezondheid, blessures of zwangerschap in Cal.com**: dat
  zijn gezondheidsgegevens en die horen bij de intake, niet in een
  boekingssysteem. De zwangerschapsmassage is alleen een keuze, geen vragenlijst.

### Wat de planner op de site doet

Zes stappen: waar → welke massage → hoe lang → (op locatie) voor wie → (op
locatie) adres → overzicht.

- **Vier massages**, alle vier dezelfde prijs: ontspanningsmassage, ontspanning
  met cuppen, alleen cuppen, zwangerschapsmassage. De prijs hangt alleen af van
  de duur: 60 min € 90 · 90 min € 130 · 120 min € 170.
- **Een stel** betaalt twee keer de behandeling en één keer reiskosten, en krijgt
  de dubbele tijd mee naar Cal.com (2 × 90 min = `duration=180`).
- **Op locatie werkt La Main alleen bij vrouwen en bij stellen.** Kiest iemand
  "een man", dan blokkeert de planner met een uitleg en een verwijzing naar de
  salon. Besluit van Robbie en Danny, 26-10-2026.
- Buiten het werkgebied of boven 35 minuten reistijd kan er nooit direct geboekt
  worden; daar staat dat de klant contact opneemt.

De reiskosten: € 0,39 per kilometer heen én terug vanaf Helmond (hemelsbreed ×
1,35), plus een reistijdtoeslag van € 0 tot 10 minuten, € 15 tot 20 minuten en
€ 30 tot 35 minuten.

Alles wat je wilt wijzigen staat in `CONFIG` bovenin het laatste script van
`la-main-opzetjes\pagina-h\index.html`. Het inrichtblad van Cal.com staat in
`la-main-opzetjes\CAL-COM-INRICHTEN.md`.

## Beeld

Sinds 15-10-2026 staat er eigen werk op de site. De bron ligt in `Shoot/`;
het uitsnijden gaat met `la-main-opzetjes` (zie het geheugen voor de scripts).
De film komt uit `Tezza-7745.MOV`; er is ook een zwart-witte versie van
dezelfde montage (`Tezza-5116.MOV`) die nu niet gebruikt wordt.

De film staat met `preload="none"` op de pagina: er wordt niets geladen tot
iemand op afspelen drukt. Alleen het stilstaande beeld (64 kB) komt mee.

**De kop.** De film is staand geschoten en past alleen beeldvullend op een
telefoon. Daarom draait op een smal scherm (tot 900 px) de korte lus in de kop,
en blijft op een breed scherm de foto staan. Een breed scherm haalt die film
**niet** op: hij staat op `preload="none"` en wordt pas door een klein stukje
JavaScript geladen als het scherm smal genoeg is. Wie "minder beweging" heeft
ingesteld, krijgt de foto. Nagemeten: op 1440 px wordt er geen enkele mp4
opgehaald, op 390 px 901 kB.

Het scrolleffect gebruikt bewust alleen close-ups; de opnames van veraf staan
bij "In de salon" en "Op locatie".

## Wat nog ontbreekt

- De prijzen van **90 en 120 minuten**. Alleen € 90 voor 60 minuten is door
  Danny bevestigd; € 130 en € 170 zijn nog een aanname.
- **De productfoto van de olie.** Zolang die er niet is, staat de olietekst in
  één kolom in het midden; met foto wordt het weer twee kolommen.
- **Haar verhaal.** Naam en portret staan er sinds 15-10, maar opleiding,
  ervaring en waarom ze dit doet nog niet. De vragen staan in
  `C:\Users\Robbi\Projects\la-main-opzetjes\VRAGEN-VOOR-LA-MAIN.md`.
- Annuleringsvoorwaarden, KvK- en btw-nummer, privacyverklaring.
