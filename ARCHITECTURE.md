# Architecture

## Philosophy

The goal of this project is to create a modular Pokémon Team Planner that supports:

- Official Pokémon games
- ROM Hacks
- Fangames
- Future community expansions

The core engine should never require modifications when adding a new game.

Everything should be data-driven.

---

# Project Structure

```
pokemon-team-planner/

.github/

docs/
    index.html
    planner.html
    404.html

    assets/
        css/
        js/
        icons/
        logos/
        sprites/
            official/
            custom/
        types/

    shared/
        dex.json
        types.json
        effectiveness.json
        regions.json
        forms.json

        custom/
            pokemon-iberia.json
            pokemon-hispalis.json
            ...

    games/
        home/
        all/
        swsh/
        bdsp/
        pla/
        sv/
        za/
        luminescent/

scripts/

README.md
ARCHITECTURE.md
SCHEMA.md
ROADMAP.md
CHANGELOG.md
CONTRIBUTING.md
LICENSE
```

---

# Core Principles

## Single Source of Truth

Official Pokémon data only exists once.

```
shared/dex.json
```

Every game references those Pokémon.

---

## Modular Games

Each game contains only:

```
config.json

pokedex.json

availability.json

overrides.json
```

No duplicated Pokémon data.

---

## Custom Pokémon

Fakemon are stored separately.

```
shared/custom/
```

Each file represents one project.

Example:

```
pokemon-iberia.json

pokemon-hispalis.json
```

Games load only the custom dex packages they need.

---

# Loader

The application never loads JSON directly.

Instead it uses:

```
Loader.loadGame()

Loader.loadDex()

Loader.loadCustomDex()

Loader.loadFilters()
```

The loader is responsible for loading and combining data.

---

# HOME

HOME contains only official Pokémon.

Filters:

- Generation
- Region
- Type
- Game

---

# ALL

ALL contains:

- Official Pokémon
- Fakemon

Additional filter:

- Origin

---

# Game Pages

Each game contains:

- Regional Pokédex
- Availability
- Game logo
- Game configuration

---

# Pokémon IDs

Official Pokémon:

```
pkmn-0001
```

Custom Pokémon:

```
iberia-0001

hispalis-0001

luminescent-0001
```

Internal IDs never change.

National Dex numbers are stored as data.

---

# Data Driven

The engine should never know:

- which games exist
- which Pokémon exist
- which filters exist

Everything should be generated from JSON files.

---

# Extensibility

Adding a new game should require only:

```
games/my-game/

config.json

pokedex.json

availability.json

overrides.json

logo.png
```

No engine modifications.

---

# Future

Future versions should support:

- Multiple languages
- Damage calculator
- Team export
- Team import
- Share links
- Statistics
- Competitive mode
- Mobile improvements

The architecture should allow new features without changing existing data formats.