
## BattleScribe data index URL

Add this URL in BattleScribe under **Manage Data → Add data index URL**:

```text
https://raw.githubusercontent.com/kobychapmans-ship-it/Slaugth-Intendants/main/index.bsi
```

The repository is configured so future catalogue rebuilds retain this URL.

# Slaugth Intendant — Horus Heresy 1.0 BattleScribe Repository

GitHub-ready fanmade BattleScribe repository for the **Slaugth Dominion Detachment**, built from `Slaugth updated.docx` with the earlier Slaugth source used only to restore the truncated Cythor Fiend material and the Remnant Infected / Ancient Weaponology clarifications.

## Ready-to-import files

- `output/Slaugth_Intendant_Dominion_HH1.catz` — import this into BattleScribe.
- `output/(HH V1) Slaugth Intendant - Dominion Detachment.cat` — plain XML for Data Editor / inspection.
- `index.xml` and `index.bsi` — ready-to-use BattleScribe repository index files for this GitHub repository.

## Compatibility

| Field | Value |
|---|---|
| BattleScribe | 2.03 |
| Game system | `(HH V1) Warhammer 30,000 - The Horus Heresy` |
| Game-system ID | `ca571888-56a9-c58e-ddaf-54f4713538bc` |
| Game-system revision | 165 |
| Catalogue revision | 1 |

## Native Slaugth content implemented

- Slaugth Intendent
- Psyhunter Slaugth
- Herdtalon Slaugth
- Relic Hunter Slaugth
- Voidling Jumpers
- Indoctrinated Armsman
- Voidling Darklights
- Corkirya Irad Drone
- Necro Harvester Drone
- The Worm that Walks
- Barasonilash
- Baalite / Fire Scorpion
- Cythor Fiend (restored from the earlier source because the updated DOCX truncates its entry)
- Remnant Infected upgrade
- All three Slaugth relics
- Slaugth Intendent external upgrade references
- Herdtalon companion choices
- Every priced native squad-size, weapon, armour, teleport, Rad-weapon and replacement option present in the supplied material
- Discipline Collars at their printed cost, with their missing effect explicitly left unresolved rather than invented

## Borrowed-force subsets

The catalogue links the following dependencies so the detachment can draw from them under **From Diversity, We Flourish**:

1. Solar Auxilia
2. Imperialis Militia and Cults
3. Mechanicum Taghmata
4. Questoris Knights (force access; earlier Ancient Weaponology wording restricts Knight weapon borrowing)
5. Asuryani
6. Necron compatibility list
7. Agents of the Emperor / Warmaster (non-Unique legal entries only)
8. Xenos of the Great Crusade (the user-maintained Great Crusade xenos catalogue)

Astartes, Talons and Daemon catalogue dependencies are intentionally not included because the updated source excludes them. Unique units are also excluded by the army rule.

### Why external units are dependencies instead of copied XML

This keeps the repo maintainable and avoids freezing hundreds of duplicated external profiles. BattleScribe 2.03 can import linked catalogue roots, but it cannot perfectly enforce every rule that spans multiple unrelated catalogue category IDs. The compiled catalogue therefore enforces what it can safely enforce and displays the remainder as legality rules. For auditing or stricter filtering, copy installed `.cat` files into `dependencies/catalogues/` and run:

```bash
python scripts/index_dependencies.py
```

That produces `data/generated_dependency_inventory.json`, including conservative Unique/Primarch candidate flags and category IDs. Then run `python scripts/build_strict_indexed.py` to produce a second `.cat/.catz` pair that uses explicit non-Unique dependency root links instead of blanket root imports.

## Force organisation

- HQ: **1-5**
- Elites: **1+ Slaugth** (no max), **0-3 other**
- Troops: **4-10**
- Fast Attack: **0-3**
- Heavy Support: **0-3**
- Lord of War: **0-1**, max **25%** of roster points

## Rebuild

```bash
python scripts/build_catalogue.py
python scripts/validate_catalogue.py
```

Stable UUIDv5 IDs are generated from semantic keys so rebuilds do not churn roster references.

## Repository layout

```text
.github/workflows/validate.yml  CI build + validation
sources/                         frozen extracted source text
data/                            normalized units, rules, relics, dependencies
scripts/                         deterministic builder, validator, dependency indexer
docs/                            conversion ledger + Ancient Weaponology rulings
dependencies/                    optional local source catalogues for indexing
output/                          .cat, .catz, build report, checksums
index.xml / index.bsi            BattleScribe repository index
```

See `docs/conversion-ledger.md` before changing cross-faction legality or filling source gaps.
