# Meewerken aan koezeg

Leuk dat je wil meewerken! Hieronder staat stap voor stap hoe je een
wijziging naar dit project stuurt via een **fork** en een **pull request**
(afgekort: PR).

Even de begrippen op een rij:

- **Upstream**: het originele project van de docent.
- **Fork**: jouw eigen kopie van het project op GitHub.
- **Origin**: de naam die git geeft aan jouw fork.
- **Branch**: een aparte "tak" waarop je jouw wijziging maakt.
- **Pull request**: een verzoek aan het originele project om jouw wijziging
  over te nemen.

## Het stappenplan

### 1. Fork het project

Klik rechtsboven op de GitHub-pagina van dit project op **Fork**. Je krijgt
nu een eigen kopie onder je eigen account.

### 2. Clone je fork

Let op: clone **jouw fork**, niet het originele project.

```bash
git clone https://github.com/<jouw-gebruikersnaam>/koezeg.git
cd koezeg
```

### 3. Voeg het originele project toe als `upstream`

Zo kan je later wijzigingen van het originele project binnenhalen.

```bash
git remote add upstream https://github.com/dvx76/koezeg.git
git remote -v
```

Je ziet nu twee remotes: `origin` (jouw fork) en `upstream` (het origineel).

### 4. Maak een branch

```bash
git switch -c mijn-nieuwe-koe
```

Werk nooit rechtstreeks op `main`. Geef je branch een korte, duidelijke naam,
bijvoorbeeld `koe-draak` of `fix-tired-mode`.

### 5. Maak je wijziging en test ze

Pas de code of de bestanden aan en probeer het uit:

```bash
uv run koezeg "Test"
uv run koezeg -f draak -d "Test"
```

### 6. Commit je wijziging

```bash
git status
git add koezeg/cows/draak.cow
git commit -m "Voeg draak toe"
```

Schrijf een korte boodschap die zegt wat je gedaan hebt. Het mag in het
Nederlands of in het Engels.

### 7. Push je branch naar je fork

```bash
git push -u origin mijn-nieuwe-koe
```

### 8. Open een pull request

Ga naar je fork op GitHub. Je ziet een gele balk met **Compare & pull
request**. Klik erop en controleer:

- **base repository**: het originele project (upstream)
- **base**: `main`
- **head repository**: jouw fork, met jouw branch

Vul de vragen in het sjabloon in. Los je een issue op? Schrijf dan in de
beschrijving `Fixes #12` (met het juiste nummer). GitHub sluit het issue
automatisch zodra je PR gemerged wordt.

### 9. Reageer op feedback

Misschien krijg je opmerkingen op je PR. Pas je code aan op **dezelfde
branch**, maak een nieuwe commit en push opnieuw. Je PR wordt automatisch
bijgewerkt. Je hoeft geen nieuwe PR te openen.

### 10. Werk je fork bij na de merge

Is je PR gemerged? Haal dan de nieuwste versie van het originele project
binnen, zodat je fork weer gelijk loopt:

```bash
git switch main
git fetch upstream
git merge upstream/main
git push origin main
```

Je mag je oude branch nu opruimen:

```bash
git branch -d mijn-nieuwe-koe
```

Wil je nog een wijziging maken? Begin dan opnieuw bij stap 4, **na** het
bijwerken van je `main`.

## Welke wijziging kan ik maken?

- Kijk bij de **Issues** van het originele project. Issues met het label
  `good first issue` zijn bedoeld om mee te beginnen.
- Laat in een reactie op het issue weten dat je eraan werkt
  ("Ik pak dit op"), zodat niet twee mensen hetzelfde doen.
- Heb je een eigen idee? Open eerst een issue om het te bespreken.

## Een nieuwe koe toevoegen

Een koe is gewoon een tekstbestand in de map `koezeg/cows/`. Kijk eens naar
`koezeg/cows/kat.cow` als voorbeeld.

1. Maak een nieuw bestand, bijvoorbeeld `koezeg/cows/draak.cow`. De naam
   bestaat uit kleine letters, zonder spaties. Het bestand moet op `.cow`
   eindigen.
2. Teken je koe met gewone ASCII-tekens (dus geen emoji of speciale tekens).
3. Gebruik deze drie plaatshouders:

   | Plaatshouder | Wordt vervangen door                                        |
   | ------------ | ----------------------------------------------------------- |
   | `$thoughts`  | het streepje dat de tekstballon met de koe verbindt (`\`)   |
   | `$eyes`      | de ogen (2 tekens, bv. `oo` of `xx`)                        |
   | `$tongue`    | de tong (2 tekens, bv. `U ` of twee spaties)                |

4. Test je koe met `uv run koezeg -f draak "Test"`. Probeer ook eens `-d` en
   `-g`.

Let op: `$thoughts` wordt maar 1 teken, `$eyes` en `$tongue` worden 2 tekens.
Je tekening schuift dus een beetje op zodra de plaatshouders vervangen zijn.
Kijk daarom altijd naar de echte uitvoer van `koezeg`, en niet alleen naar
het bestand.

## Afspraken

- **Eén onderwerp per PR.** Een nieuwe koe en een bugfix horen in twee aparte
  PR's.
- **Test je wijziging** voor je een PR opent.
- **Verander niets wat niet nodig is.** Formatteer dus geen hele bestanden om.
- **Blijf vriendelijk** in reacties, zowel als je feedback krijgt als wanneer
  je ze geeft.
- Krijg je een **merge conflict**? Geen paniek. Het betekent dat iemand
  anders hetzelfde stuk van een bestand heeft aangepast. Vraag hulp, dan
  lossen we het samen op.
