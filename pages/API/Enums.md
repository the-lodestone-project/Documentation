# Enums

These enums are stored in the language independent [minecraft-data](https://github.com/PrismarineJS/minecraft-data) project,

 and accessed through [node-minecraft-data](https://github.com/PrismarineJS/node-minecraft-data).

### minecraft-data

The data is available in [node-minecraft-data](https://github.com/PrismarineJS/node-minecraft-data) module

`require('minecraft-data')(bot.version)` gives you access to it.

### mcdata.blocks

blocks indexed by id

### mcdata.items

items indexed by id

### mcdata.materials

The key is the material. The value is an object with the key as the item id

of the tool and the value as the efficiency multiplier.

### mcdata.recipes

recipes indexed by id

### mcdata.instruments

instruments indexed by id

### mcdata.biomes

biomes indexed by id

### mcdata.entities

entities indexed by id
