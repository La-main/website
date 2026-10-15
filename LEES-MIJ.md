# Website La Main

De site van La Main, massage in Eindhoven en Nuenen. Eén pagina met een
afspraakplanner. Geen framework en geen bouwstap: `index.html` openen en het
werkt.

Online: **https://la-main.nl** (www stuurt door naar het hoofdadres, HTTPS staat
aan, zoekmachines mogen erin sinds 09-10-2026).

| Bestand | Wat het is |
|---|---|
| `index.html` | De hele pagina: opmaak, teksten en de planner. |
| `foto/` | Veertien beelden uit de eigen fotoshoot van 15-10-2026. |
| `video/` | De film van 40 seconden (720x1280, 6,9 MB) en het stilstaande beeld ervoor. |
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

De pagina rekent zelf niets vast. Hij bepaalt de behandeling en, bij op locatie,
de reistijd en reiskosten op postcode, en stuurt de klant daarna door naar
Cal.com. Daar kiest de klant dag en tijd, en de afspraak komt in de agenda van
La Main. Zij beheert haar agenda dus zelf.

**Het inrichten van Cal.com staat stap voor stap in
`C:\Users\Robbi\Projects\la-main-opzetjes\CAL-COM-INRICHTEN.md`.** Kort:

| Afspraaktype | URL | Dagen | Tijd | Marge vooraf | Marge erna |
|---|---|---|---|---|---|
| Salon Eindhoven | `salon-eindhoven` | maandag, woensdag | 09:00 – 18:00 | — | 15 min |
| Salon Nuenen | `salon-nuenen` | dinsdag | 09:00 – 18:00 | — | 15 min |
| Op locatie | `op-locatie` | nog te bevestigen | nog te bevestigen | 30 min | 30 min |

- Eén afspraaktype per plek, met 60, 90 en 120 minuten in één lijstje. De site
  geeft de gekozen duur mee als `?duration=`, de berekening als `?notes=` en bij
  op locatie het adres van de klant als `?location=`.
- Gratis abonnement volstaat: één persoon, onbeperkt afspraken en afspraaktypen.
  Het logo van Cal.com blijft onderaan de boekingspagina staan.
- Cal.com rekent **niets** met reisafstand. De marges hierboven zijn vast.
- Vraag bij het boeken om naam, telefoon en (op locatie) het adres. **Geen
  vragen over gezondheid, blessures of zwangerschap in Cal.com**: dat zijn
  gezondheidsgegevens en die horen bij de intake, niet in een boekingssysteem.

Zodra de drie links bestaan, hoeft er in de werkversie één woord in:

```js
cal: { basis:'https://cal.com/', gebruiker:'la-main', locatie:'op-locatie' },
```

Daarna opnieuw bouwen en pushen. Zolang `gebruiker` leeg is, staat op de site
"Agenda volgt" en komt niemand op een dood adres uit. Bij op locatie buiten het
werkgebied of boven 35 minuten reistijd kan er nooit direct geboekt worden;
daar staat dat de klant contact opneemt.

## Beeld

Sinds 15-10-2026 staat er eigen werk op de site. De bron ligt in `Shoot/`;
het uitsnijden gaat met `la-main-opzetjes` (zie het geheugen voor de scripts).
De film komt uit `Tezza-7745.MOV`; er is ook een zwart-witte versie van
dezelfde montage (`Tezza-5116.MOV`) die nu niet gebruikt wordt.

De film staat met `preload="none"` op de pagina: er wordt niets geladen tot
iemand op afspelen drukt. Alleen het stilstaande beeld (64 kB) komt mee.

## Wat nog ontbreekt

- **Haar verhaal.** Er staat geen naam, geen gezicht en geen opleiding op de
  site. De vragen daarvoor staan in
  `C:\Users\Robbi\Projects\la-main-opzetjes\VRAGEN-VOOR-LA-MAIN.md`.
- De prijzen van 90 en 120 minuten (alleen € 90 voor 60 minuten is bevestigd).
- Annuleringsvoorwaarden, KvK- en btw-nummer, privacyverklaring.
- Op welke dagen en tijden ze op locatie werkt.
