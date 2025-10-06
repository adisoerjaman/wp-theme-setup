# wp-theme-setup

## Inleiding
Voordat je een eigen thema kunt bouwen, moet je WordPress correct installeren en een lokale omgeving opzetten. Daarna maak je een eerste thema-map aan in wp-content/themes met de minimale bestanden. Dit geeft je een basis waarop je verder kunt bouwen.

## Wat is het WordPress-dashboard?
Het WordPress-dashboard (ook wel wp-admin) is het beheergedeelte van je website. Je bereikt het door in je browser naar /wp-admin te gaan, bijvoorbeeld:

http://nieuwstheme.local/wp-admin


Hier log je in met de gebruikersnaam en het wachtwoord die je tijdens de installatie hebt gekozen.

In het dashboard kun je:
- pagina’s en berichten beheren;
- thema’s en plugins installeren of activeren;
- menu’s, widgets en instellingen aanpassen;
- gebruikers toevoegen;
- en de algemene instellingen van je website beheren.

Je kunt het zien als de achterkant van je site, waar je werkt aan structuur en inhoud, terwijl de voorkant is wat bezoekers zien.

---

1. Installeer LocalWP vanaf https://localwp.com/ en open de applicatie.
2. Maak een nieuwe WordPress-site aan, bijvoorbeeld met de naam “NieuwsTheme”.
3. Log in op het WordPress-dashboard via `/wp-admin` om te controleren dat de installatie werkt.
4. Ga naar de map `wp-content/themes` in je lokale WordPress-installatie.
5. Maak een nieuwe map aan voor je thema, bijvoorbeeld `nieuws-theme`.
6. Maak in deze map de volgende bestanden:
   - `style.css` met de minimale themakop:
     ```css
     /*
     Theme Name: Nieuws Theme
     Author: [Jouw naam]
     Description: Eerste versie van mijn eigen nieuws-theme
     Version: 1.0
     */
     ```
   - `index.php` met minimale content, bijvoorbeeld:
     ```php
     <?php
     get_header();
     ?>
     <h1>Hello Nieuws Theme!</h1>
     <?php
     get_footer();
     ?>
     ```
   - Optioneel: `functions.php` voor later gebruik.
7. Activeer het thema via het WordPress-dashboard onder **Weergave → Thema’s**.
8. Open de homepage en controleer dat je eerste thema actief is en de tekst zichtbaar is.

## Auto-update
Nu je thema actief is in WordPress, wil je direct kunnen zien wat er verandert als je code aanpast.
Met VS Code, LocalWP en een kleine npm-configuratie kun je je bestanden bewerken en de browser automatisch laten verversen zodra je opslaat.

Dit werkt net als Live Server, maar dan geïntegreerd in je WordPress-omgeving.
Zo ervaar je direct het effect van je HTML, PHP en CSS-wijzigingen zonder handmatig te vernieuwen.

---

### npm

1. Open je thema-map (`nieuws-theme`) in VS Code.
2. Open de terminal in VS Code en controleer of je Node.js hebt geïnstalleerd:
```bash
   node -v
   ```

Als dit geen versie toont, installeer dan Node.js vanaf https://nodejs.org/.
3. Initialiseer npm in je thema-map:

```bash
  npm init -y
Dit maakt een package.json-bestand aan.
```

---

### BrowserSync
4. Installeer BrowserSync als ontwikkeltool:

```bash
npm install browser-sync --save-dev
```

5. Maak in de hoofdmap van je thema een nieuw bestand: bs-config.js
Voeg daarin de volgende configuratie toe:

```js
module.exports = {
  proxy: "http://nieuwstheme.local", // jouw lokale domeinnaam
  files: ["**/*.php", "**/*.css"],
  injectChanges: true,
  open: false,
  notify: false
};
```

6. Voeg in je package.json een nieuw script toe:
```json
"scripts": {
  "watch": "browser-sync start --config bs-config.js"
}
```

7. Start nu BrowserSync:

```bash
npm run watch
```

8. De browser opent automatisch of vernieuwt zodra je bestanden opslaat.
Test of het werkt.

Open index.php en voeg onder de bestaande code een paragraaf toe:
```php
<h1>Hello Nieuws Theme!</h1>
<p>Dit is mijn eerste automatische live wijziging!</p>
Sla op en kijk hoe de browser automatisch ververst.
```

9. Probeer ook style.css te bewerken, bijvoorbeeld:

```css
body {
  background-color: #f8fafc;
  color: #333;
}
```

---

Zodra je opslaat, zie je direct de verandering in de browser.

> Succes! - Adi