[Accueil](../README.md) · [Guide](guide.md) · [Ruines](ruines.md) · [Relevé et Atlas](releve-et-atlas.md) · **Serveur** · [English](../en/server.md)

# Serveur

## Installer

Mettez le même JAR dans le dossier `mods` du serveur et de chaque client : Minecraft 1.21.1, NeoForge 21.1.265 ou plus récent, Java 21. Aucun autre mod n'est nécessaire.

## Configuration

Le fichier est `config/vanishedatlas-common.toml`, écrit par le jeu au premier lancement. Il a une section, `[densite]`, avec un réglage par ruine :

| Réglage | Ruine | Par défaut | Plage |
|---|---|---|---|
| `sealed_crypt` | Crypte Scellée | 100 | 0 à 100 |
| `watchtower` | Tour de Guet | 100 | 0 à 100 |
| `buried_temple` | Temple Enseveli | 100 | 0 à 100 |

Chaque valeur est la part des sites possibles qui sont vraiment construits, en pour cent. 100 les garde tous, 50 en garde environ un sur deux, 0 retire cette ruine. Le changement vaut pour les chunks générés ensuite ; les ruines déjà construites restent.

Retirer la Tour de Guet retire aussi les Relevés du jeu, puisque le coffre de la tour est leur seule source.

## Commandes

Le mod n'ajoute aucune commande à lui. Les commandes vanilla marchent avec ses ruines :

| Commande | Ce qu'elle fait |
|---|---|
| `/place structure vanishedatlas:watchtower` | Construit une Tour de Guet là où vous êtes |
| `/place structure vanishedatlas:sealed_crypt` | Construit une Crypte Scellée là où vous êtes |
| `/place structure vanishedatlas:buried_temple` | Construit un Temple Enseveli là où vous êtes |
| `/give @s vanishedatlas:survey` | Donne un Relevé (Crypte) |
| `/give @s vanishedatlas:atlas` | Donne un Atlas vide |

Les autres identifiants d'objets sont `vanishedatlas:vanished_key`, `vanishedatlas:crypt_plate` et `vanishedatlas:temple_plate`. Un Relevé du Temple est un Relevé dont le composant `vanishedatlas:survey_target` vaut `"temple"`.

## Données

Tout ce qui touche aux ruines est de la donnée simple qu'un datapack peut remplacer, sous `data/vanishedatlas/` :

- `worldgen/structure`, `worldgen/structure_set` et `worldgen/template_pool` : les structures, leur fréquence et leurs salles ;
- `tags/worldgen/biome/has_structure` : les biomes de chaque ruine ;
- `loot_table` : les coffres de la Tour et du Temple, le Vault, la récompense du trial spawner et le sable suspect ;
- `recipe/atlas.json` : la recette de l'Atlas.

## Performances

Le Relevé et l'Atlas ne figent jamais le serveur : la recherche tourne sur son propre fil, et le fil du serveur ne fait que charger les chunks dont elle a besoin, sans les attendre. Au plus 4 recherches tournent en même temps sur tout le serveur, et 1 par joueur.

## Problèmes connus

- De l'eau souterraine peut s'infiltrer dans une Crypte générée près d'une nappe, et inonder une partie d'une salle.
- Personne n'a encore joué une vraie partie avec cette version : l'énigme, les pièges et le combat du trial spawner n'ont pas été jugés par des joueurs, et l'équilibrage (fréquences, butin) peut changer.
- Les ruines n'apparaissent que dans les chunks neufs : sur un vieux monde, partez vers des terres inexplorées.
