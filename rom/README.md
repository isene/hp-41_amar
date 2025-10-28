# AMAR.ROM - HP-41 Module for Amar RPG Tools

Pluggable HP-41 ROM module providing complete Amar RPG encounter generation with stats.

## Features

- **O6 Dice Roller**: Full open-ended D6 with critical/fumble detection
- **Random Encounter Generator**: Terrain-based encounters with complete stats
- **Basic NPC Stats**: HP, AP, weapon stats (INI/Off/Def/Dam/Rng), and MD

## ROM Information

- **XROM Number**: 15
- **Module Name**: AMAR
- **Version**: 1A
- **Identity**: AR1A

## Functions

| Function | Description |
|----------|-------------|
| AMAR     | Main menu program |
| O6       | Open-ended D6 roller |
| ENC      | Encounter generator with stats |
| ENCTYP   | Encounter type determination |
| ENCNUM   | Number of opponents |
| ENCAT    | Encounter attitude |
| STATS    | NPC stats generator |
| TERRE    | Terrain/conditions setting |
| ENCDAT   | Encounter data initialization |

## Usage

### Initial Setup

1. Load the AMAR.ROM module
2. Execute `XEQ "ENCDAT"` once to initialize encounter type names

### Main Menu

Execute `XEQ "AMAR"` to access the main menu:

```
O6 ENC TERR *
```

- **A (O6)**: Roll open-ended D6
- **B (ENC)**: Generate encounter with complete stats
- **C (TERR)**: Set terrain, day/night, and level modifier
- **E (*)**: Return to menu

### Encounter Generation

Press **C** to set terrain first:
```
Terrain: 0=City, 1=Rural, 2=Road, 3=Plains
         4=Hills, 5=Mountains, 6=Woods, 7=Wilderness
Day/Night: 1=Day, 0=Night
Level Mod: -5 to +5 (adjusts difficulty)
```

Press **B** to generate encounter:
```
Shows: Number of opponents
       Attitude (Hostile/Antagonistic/Neutral/Positive/Friendly)
       Type (Small/Large Animal, Human, Dwarf, Elf, Arax, Monster, Event)

Then prompts for SIZE (typically 3-6 for humanoids)

Displays:
  HP   = Hit Points (health)
  AP   = Armor Points (damage absorption)
  INI  = Initiative (who acts first)
  OFF  = Offensive skill
  DEF  = Defensive skill
  DAM  = Damage dealt
  RNG  = Range (for ranged weapons)
  MD   = Mental Defense (vs magic/psionics)
```

## Stats Calculation

Stats are generated based on encounter level (Level Mod + base difficulty):

- **HP**: Size × 2 + (Level + d6) ÷ 3
- **AP**: Level + 1 + d3
- **INI**: Level + Skill + 2 + d3
- **OFF**: Level + Skill + d6
- **DEF**: Level + Skill + d4
- **DAM**: (Level + Size) ÷ 2 + d3
- **RNG**: Level + 3 + d3 (animals get no range)
- **MD**: Level + 1 + d4

## Registers Used

- R01-R04: O6 dice calculations
- R10-R13: Terrain/day/level settings
- R14-R16: Encounter type/number/attitude
- R20-R29: Generated stats (Size, Level, HP, AP, weapons, MD)

## Building the ROM

Requirements:
- NutStudio or HP-41 ROM development tools
- rpncomp (RPN compiler)
- asnut (assembler)
- lnnut (linker)

```bash
cd rom/src
make
```

This produces `AMAR.mod` which can be loaded into:
- HP-41CL
- DM-41X
- HP-41 emulators (V41, i41CX, etc.)

## Loading in HP-41CL

```
MMUDIS
TURBO50
"AMAR" PLUG1U
MMU
CAT 2    (should show -AMAR 1A)
```

## Loading in DM-41X

1. Copy AMAR.mod to calculator
2. Settings → Library → Load Module
3. Select AMAR.mod

## Example Session

```
XEQ "AMAR"
→ "AMAR RPG TOOLS"
→ "V 2.0 ROM"

Press C (TERR)
→ TERRAIN? 6     (Woods)
→ DAY(1)NIGHT(0)? 0
→ LEVEL MOD? 2

Press B (ENC)
→ NUM=3
→ ATTITUDE: HOSTILE
→ TYPE: LARGE ANIMAL
→ SIZE=? 5
→ HP=14
→ AP=4
→ WEAPON:
→ INI=9
→ OFF=11
→ DEF=9
→ DAM=6
→ MD=3

Press A (O6 for initiative)
→ 7
```

## Encounter Types by Terrain

See main README.md for complete probability tables by terrain and time.

## Differences from Standard Version

**ROM Module Advantages**:
- Instant loading (no program entry)
- Protected from accidental deletion
- No main memory usage
- Professional module experience

**Features**:
- Complete stats generation added
- SIZE prompt for customization
- Mental Defense (MD) calculation
- Weapon range for applicable types

## License

This software is released into the Public Domain.

## Links

- [Amar RPG](http://d6gaming.org)
- [GitHub Repository](https://github.com/isene/hp-41_amar)
