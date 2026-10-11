# koezeg 🐄

Een koe die dingen zegt.

`koezeg` is een kleine Python-versie van het klassieke programma [`cowsay`](https://en.wikipedia.org/wiki/Cowsay).
Het is bedoeld als **oefenproject voor git en GitHub**: je maakt een fork,
past iets aan (een bug, een nieuwe koe, een extra optie) en stuurt een
pull request naar dit project.

## Aan de slag

Je hebt [git](https://git-scm.com/) en [uv](https://docs.astral.sh/uv/)
nodig. Daarna:

```bash
git clone https://github.com/dvx76/koezeg.git
cd koezeg
uv run koezeg "Hallo wereld"
```

> Wil je meewerken aan het project? Lees dan eerst
> [CONTRIBUTING.md](CONTRIBUTING.md). Daar staat stap voor stap hoe je een
> fork maakt en een pull request opent.

Het eerste `uv run` duurt even, want uv maakt dan een virtuele omgeving voor
je aan. Daarna gaat het meteen.

## Gebruik

```bash
uv run koezeg "Hallo wereld"
```

```text
 _____________
< Hallo wereld >
 -------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

Je kan opties combineren. Bijvoorbeeld een dode kat:

```bash
uv run koezeg -d -f kat "Au!"
```

```text
 _____
< Au! >
 -----
        \
         \
          /\_/\
         ( xx  )
          =\U /=
          /     \      _
         /  | |  \    / )
        (__/   \__)__/ /
                  \___/
```

## Opties

| Optie       | Wat doet het?                                                  |
| ----------- | -------------------------------------------------------------- |
| `-f <koe>`  | Kies een koe (de naam van een bestand in `koezeg/cows/`)       |
| `-r`        | Kies een willekeurige koe                                      |
| `-b`        | Borg-modus (ogen `==`)                                         |
| `-d`        | Dood (ogen `xx` en een tong)                                   |
| `-g`        | Gierig (ogen `$$`)                                             |
| `-s`        | Stoned (ogen `**` en een tong)                                 |
| `-t`        | Moe (ogen `--`)                                                |
| `-w`        | Wired (wijd open ogen `OO`)                                    |
| `-y`        | Jeugdig (kleine ogen `..`)                                     |
| `-h`        | Toon de hulptekst                                              |

Zonder tekst zegt de koe gewoon `Boe!`.
Alle koeien staan in de map `koezeg/cows/`.

## Hoe zit het project in elkaar?

```text
koezeg/
├── README.md          <- dit bestand
├── CONTRIBUTING.md    <- hoe werk je mee? Lees dit!
├── pyproject.toml     <- instellingen van het project (voor uv)
├── .github/           <- sjabloon voor pull requests
└── koezeg/            <- de Python-code
    ├── __main__.py    <- startpunt voor `python -m koezeg`
    ├── cli.py         <- leest de opties en print de koe
    ├── bubble.py      <- tekent de tekstballon
    ├── cowfile.py     <- zoekt en tekent de koeien
    ├── modes.py       <- de gezichten (-d, -g, ...)
    └── cows/          <- één bestand per koe
```

Tip: begin met lezen in `cli.py`. Dat is de plek waar alles samenkomt.
