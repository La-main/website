# Website La Main

De site van La Main, massage in Eindhoven. Eén pagina met een afspraakplanner.
Geen framework en geen bouwstap: `index.html` openen en het werkt.

Online: https://la-main.github.io/website/ — later op https://la-main.nl

| Bestand | Wat het is |
|---|---|
| `index.html` | De hele pagina: opmaak, teksten en de planner. |
| `foto/` | Tien beelden. **Tijdelijke foto's van Unsplash**, niet de salon zelf. |
| `lettertypes/` + `lettertypes.css` | Prata, Cormorant Garamond en Montserrat, in de site zelf. Er wordt niets bij Google opgehaald. |
| `CNAME` | Komt er pas in zodra de DNS klaarstaat; staat er nu bewust niet. |

## Wijzigen en publiceren

De pagina wordt gebouwd uit de werkversie in
`C:\Users\Robbi\Projects\la-main-opzetjes\pagina-h\index.html`:

```powershell
# site opnieuw bouwen in deze map (zonder domein, nog niet vindbaar)
C:\Users\Robbi\Projects\la-main-opzetjes\bron\bouw-site.ps1 -domein ''
# live zetten
git -C C:\Users\Robbi\Projects\la-main-nl add -A
git -C C:\Users\Robbi\Projects\la-main-nl commit -m "beschrijving"
git -C C:\Users\Robbi\Projects\la-main-nl push
```

Na ongeveer een minuut staat het online. Pushen gaat met een eigen sleutel
(`~/.ssh/la-main`), die als implementatiesleutel met schrijfrechten in de
repository staat. Daardoor is er geen wachtwoord of token nodig.

## Zodra het domein aan de beurt is

1. Bij Mijndomein in het DNS-beheer zetten:
   - **A** op `@` → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - **CNAME** op `www` → `la-main.github.io`
2. Daarna hier: `bouw-site.ps1` zonder `-domein ''` (dan komt `CNAME` terug met
   `la-main.nl`), vastleggen en pushen.
3. In GitHub bij Settings → Pages het domein invullen en **Enforce HTTPS** aanzetten.
4. Pas als de site echt vindbaar mag zijn: `bouw-site.ps1 -vindbaar`. Dan gaat de
   regel `noindex` eruit die zoekmachines nu weert.

## Wat nog ontbreekt

- **Echte fotografie.** Grootste punt. De kamerfoto's bij "In de salon" en
  "Op locatie" zijn niet de salon, en in de briefing staat "geen witte handdoeken"
  terwijl er nu gestapeld wit linnen in beeld is.
- Adres van de salon, openingstijden per dag, annuleringsvoorwaarden, KvK- en
  btw-nummer, telefoon en e-mail.
- De prijzen van 90 en 120 minuten (alleen € 90 voor 60 minuten is bevestigd).
- **Boeken loopt straks via Cal.com**, gekoppeld aan de Google Agenda van
  `info@la-main.nl`. De planner in de pagina rekent de reiskosten uit en geeft
  die mee; het vastleggen doet Cal.com. Zolang dat niet is ingericht, is de
  planner een proefversie die niets opslaat.
