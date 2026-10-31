# NadecDuelist

Yu-Gi-Oh!-deckanalyse op basis van een YDKE-string. De site is één statisch bestand (`index.html`) en heeft geen server of bouwstap nodig.

## Online zetten met GitHub Pages

1. Maak op GitHub een nieuwe **public** repository, bijvoorbeeld `nadecduelist`.
2. Kies **uploading an existing file** en sleep alle bestanden en mappen uit deze map erin. Klik op **Commit changes**.
3. Ga naar **Settings > Pages**. Kies bij **Source** de optie **Deploy from a branch**, kies de branch `main` en de map `/ (root)`, en klik op **Save**.
4. Na een paar minuten staat de site op `https://JOUW-GEBRUIKERSNAAM.github.io/nadecduelist/`.

Elke nieuwe commit op `main` zet de site automatisch opnieuw online.

## De app aanpassen

- `index.html` is het gebouwde eindresultaat. Pas dit bestand niet met de hand aan.
- `tools/template.html` bevat de opmaak, teksten en rekenregels.
- Bouw daarna opnieuw vanuit deze map, bijvoorbeeld in Git Bash:

```bash
perl tools/build.pl
```

Upload of commit daarna `index.html` en `tools/template.html`.

## Kaartdata verversen

Nieuwe kaarten komen er pas in als je de data ververst. Zet ook de datum in de voettekst van `tools/template.html` goed.

```bash
curl -o tools/data/cardinfo.json https://db.ygoprodeck.com/api/v7/cardinfo.php
```

```bash
perl tools/flatten.pl tools/data/cardinfo.json tools/data/cards.tsv
```

```bash
perl tools/classify.pl tools/data/cards.tsv tools/data/roles.tsv
```

```bash
perl tools/build.pl
```

De twee tussenbestanden (`cardinfo.json` en `cards.tsv`) staan in `.gitignore` en horen niet in de repository.
