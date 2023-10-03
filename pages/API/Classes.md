# Classes

### vec3

See [andrewrk/node-vec3](https://github.com/andrewrk/node-vec3)

All points in mineflayer are supplied as instances of this class.

* x - south
* y - up
* z - west

Functions and methods which require a point argument accept `Vec3` instances
as well as an array with 3 values, and an object with `x`, `y`, and `z`
properties.

### mineflayer.Location

### Entity

Entities represent players, mobs, and objects. They are emitted
in many events, and you can access your own entity with `bot.entity`.
See [prismarine-entity](https://github.com/PrismarineJS/prismarine-entity)

#### Player Skin Data

The skin data is stored in the `skinData` property of the player object, if present.

```js
// player.skinData
{
  url: 'http://textures.minecraft.net/texture/...',
  model: 'slim' // or 'classic'
}
```

### Block

See [prismarine-block](https://github.com/PrismarineJS/prismarine-block)

Also `block.blockEntity` is additional field with block entity data as `Object`. The data in this varies between versions.

```js
// sign.blockEntity example from 1.19
{
  GlowingText: 0, // 0 for false, 1 for true
  Color: 'black',
  Text1: '{"text":"1"}',
  Text2: '{"text":"2"}',
  Text3: '{"text":"3"}',
  Text4: '{"text":"4"}'
}
```

Note if you want to get a sign's plain text, you can use [`block.getSignText()`](https://github.com/PrismarineJS/prismarine-block/blob/master/doc/API.md#sign) instead of unstable blockEntity data.

```java
> block = bot.blockAt(new Vec3(0, 60, 0)) // assuming a sign is here
> block.getSignText()
[ "Front text\nHello world", "Back text\nHello world" ]
```

### Biome

See [prismarine-biome](https://github.com/PrismarineJS/prismarine-biome)

### Item

See [prismarine-item](https://github.com/PrismarineJS/prismarine-item)

### windows.Window (base class)

See [prismarine-windows](https://github.com/PrismarineJS/prismarine-windows)

#### window.deposit(itemType, metadata, count, nbt)

This function returns a `Promise`, with `void` as its argument when done depositing.

* `itemType` - numerical item id
* `metadata` - numerical value. `null` means match anything.
* `count` - how many to deposit. `null` is an alias to 1.
* `nbt` - match nbt data. `null` is do not match nbt.

#### window.withdraw(itemType, metadata, count, nbt)

This function returns a `Promise`, with `void` as its argument when done withdrawing. Throws and error if the bot has no free room in its inventory.

* `itemType` - numerical item id
* `metadata` - numerical value. `null` means match anything.
* `count` - how many to withdraw. `null` is an alias to 1.
* `nbt` - match nbt data. `null` is do not match nbt.

#### window.close()

### Recipe

See [prismarine-recipe](https://github.com/PrismarineJS/prismarine-recipe)

### mineflayer.Container

Extends windows.Window for chests, dispensers, etc...
See `bot.openContainer(chestBlock or minecartchestEntity)`.

### mineflayer.Furnace

Extends windows.Window for furnace, smelter, etc...
See `bot.openFurnace(furnaceBlock)`.

#### furnace "update"

Fires when `furnace.fuel` and/or `furnace.progress` update.

#### furnace.takeInput()

This function returns a `Promise`, with `item` as its argument upon completion.

#### furnace.takeFuel()

This function returns a `Promise`, with `item` as its argument upon completion.

#### furnace.takeOutput()

This function returns a `Promise`, with `item` as its argument upon completion.

#### furnace.putInput(itemType, metadata, count)

This function returns a `Promise`, with `void` as its argument upon completion.

#### furnace.putFuel(itemType, metadata, count)

This function returns a `Promise`, with `void` as its argument upon completion.

#### furnace.inputItem()

Returns `Item` instance which is the input.

#### furnace.fuelItem()

Returns `Item` instance which is the fuel.

#### furnace.outputItem()

Returns `Item` instance which is the output.

#### furnace.fuel

How much fuel is left between 0 and 1.

#### furnace.progress

How much cooked the input is between 0 and 1.

### mineflayer.EnchantmentTable

Extends windows.Window for enchantment tables
See `bot.openEnchantmentTable(enchantmentTableBlock)`.

#### enchantmentTable "ready"

Fires when `enchantmentTable.enchantments` is fully populated and you
may make a selection by calling `enchantmentTable.enchant(choice)`.

#### enchantmentTable.targetItem()

Gets the target item. This is both the input and the output of the
enchantment table.

#### enchantmentTable.xpseed

The 16 bits xpseed sent by the server.

#### enchantmentTable.enchantments

Array of length 3 which are the 3 enchantments to choose from.
`level` can be `-1` if the server has not sent the data yet.

Looks like:

```js
[
  {
    level: 3
  },
  {
    level: 4
  },
  {
    level: 9
  }
]
```

#### enchantmentTable.enchant(choice)

This function returns a `Promise`, with `item` as its argument when the item has been enchanted.

* `choice` - [0-2], the index of the enchantment you want to pick.

#### enchantmentTable.takeTargetItem()

This function returns a `Promise`, with `item` as its argument upon completion.

#### enchantmentTable.putTargetItem(item)

This function returns a `Promise`, with `void` as its argument upon completion.

#### enchantmentTable.putLapis(item)

This function returns a `Promise`, with `void` as its argument upon completion.

### mineflayer.anvil

Extends windows.Window for anvils
See `bot.openAnvil(anvilBlock)`.

#### anvil.combine(itemOne, itemTwo[, name])

This function returns a `Promise`, with `void` as its argument upon completion.

#### anvil.combine(item[, name])

This function returns a `Promise`, with `void` as its argument upon completion.

#### villager "ready"

Fires when `villager.trades` is loaded.

#### villager.trades

Array of trades.

Looks like:

```js
[
  {
    firstInput: Item,
    output: Item,
    hasSecondItem: false,
    secondaryInput: null,
    disabled: false,
    tooluses: 0,
    maxTradeuses: 7
  },
  {
    firstInput: Item,
    output: Item,
    hasSecondItem: false,
    secondaryInput: null,
    disabled: false,
    tooluses: 0,
    maxTradeuses: 7
  },
  {
    firstInput: Item,
    output: Item,
    hasSecondItem: true,
    secondaryInput: Item,
    disabled: false,
    tooluses: 0,
    maxTradeuses: 7
  }
]
```

#### villager.trade(tradeIndex, [times])

Is the same as [bot.trade(villagerInstance, tradeIndex, [times])](#bottradevillagerinstance-tradeindex-times)

### mineflayer.ScoreBoard

#### ScoreBoard.name

Name of the scoreboard.

#### ScoreBoard.title

The title of the scoreboard (does not always equal the name)

#### ScoreBoard.itemsMap

An object with all items in the scoreboard in it

```js
{
  wvffle: { name: 'wvffle', value: 3 },
  dzikoysk: { name: 'dzikoysk', value: 6 }
}
```

#### ScoreBoard.items

An array with all sorted items in the scoreboard in it

```js
[
  { name: 'dzikoysk', value: 6 },
  { name: 'wvffle', value: 3 }
]
```

### mineflayer.Team

#### Team.name

Name of the team

#### Team.friendlyFire

#### Team.nameTagVisibility

One of `always`, `hideForOtherTeams`, `hideForOwnTeam`

#### Team.collisionRule

One of `always`, `pushOtherTeams`, `pushOwnTeam`

#### Team.color

Color (or formatting) name of team, e.g. `dark_green`, `red`, `underlined`

#### Team.prefix

A chat component containing team prefix

#### Team.suffix

A chat component containing team suffix

#### Team.members

Array of team members. Usernames for players and UUIDs for other entities.

### mineflayer.BossBar

#### BossBar.title

Title of boss bar, instance of ChatMessage

#### BossBar.health

Percent of boss health, from `0` to `1`

#### BossBar.dividers

Number of boss bar dividers, one of `0`, `6`, `10`, `12`, `20`

#### BossBar.entityUUID

Boss bar entity uuid

#### BossBar.shouldDarkenSky

Determines whether or not to darken the sky

#### BossBar.isDragonBar

Determines whether or not boss bar is dragon bar

#### BossBar.createFog

Determines whether or not boss bar creates fog

#### BossBar.color

Determines what color the boss bar color is, one of `pink`, `blue`, `red`, `green`, `yellow`, `purple`, `white`

### mineflayer.Particle

#### Particle.id

Particle ID, as defined in the [protocol](https://wiki.vg/Protocol#Particle)

#### Particle.name

Particle Name, as defined in the [protocol](https://wiki.vg/Protocol#Particle)

#### Particle.position

Vec3 instance of where the particle was created

#### Particle.offset

Vec3 instance of the particle's offset

#### Particle.longDistanceRender

Determines whether or not to force the rendering of a particle despite client particle settings and increases maximum view distance from 256 to 65536

#### Particle.count

Amount of particles created

#### Particle.movementSpeed

Particle speed in a random direction
