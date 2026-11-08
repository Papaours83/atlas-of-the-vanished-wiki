[Home](../README.md) · [Guide](guide.md) · [Ruins](ruins.md) · [Survey and Atlas](survey-and-atlas.md) · **Server** · [Français](../fr/serveur.md)

# Server

## Installing

Put the same JAR in the `mods` folder of the server and of every client: Minecraft 1.21.1, NeoForge 21.1.265 or newer, Java 21. No other mod is needed.

## Configuration

The file is `config/vanishedatlas-common.toml`, written by the game on first launch. It has one section, `[densite]`, with one setting per ruin:

| Setting | Ruin | Default | Range |
|---|---|---|---|
| `sealed_crypt` | Sealed Crypt | 100 | 0 to 100 |
| `watchtower` | Watchtower | 100 | 0 to 100 |
| `buried_temple` | Buried Temple | 100 | 0 to 100 |

Each value is the share of possible sites that are actually built, in percent. 100 keeps them all, 50 keeps about one in two, 0 turns that ruin off. The change applies to chunks generated afterwards; ruins already built stay.

Turning off the Watchtower also removes the Surveys from the game, since the tower chest is their only source.

## Commands

The mod adds no command of its own. Vanilla commands work with its ruins:

| Command | What it does |
|---|---|
| `/place structure vanishedatlas:watchtower` | Builds a Watchtower where you stand |
| `/place structure vanishedatlas:sealed_crypt` | Builds a Sealed Crypt where you stand |
| `/place structure vanishedatlas:buried_temple` | Builds a Buried Temple where you stand |
| `/give @s vanishedatlas:survey` | Gives a Survey (Crypt) |
| `/give @s vanishedatlas:atlas` | Gives an empty Atlas |

The other item ids are `vanishedatlas:vanished_key`, `vanishedatlas:crypt_plate` and `vanishedatlas:temple_plate`. A Temple Survey is a Survey with the component `vanishedatlas:survey_target` set to `"temple"`.

## Data

Everything about the ruins is plain data that a datapack can replace, under `data/vanishedatlas/`:

- `worldgen/structure`, `worldgen/structure_set` and `worldgen/template_pool`: the structures, how often they appear, and their rooms;
- `tags/worldgen/biome/has_structure`: the biomes of each ruin;
- `loot_table`: the Watchtower and Temple chests, the Vault, the trial spawner reward and the suspicious sand;
- `recipe/atlas.json`: the Atlas recipe.

## Performance

Surveys and the Atlas never freeze the server: the search runs on its own thread, and the server thread only loads the chunks it needs without waiting for them. At most 4 searches run at once on the whole server and 1 per player.

## Known issues

- Groundwater can seep into a Crypt generated next to an underground aquifer, flooding part of a room.
- Nobody has played a full game with this version yet: the puzzle, the traps and the trial spawner fight have not been judged by players, and the balance (frequencies, loot) may change.
- The ruins only appear in new chunks: on an old world, travel to unexplored land.
