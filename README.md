# Data Types Table

| Type   | Usual Size | Description                                                     |
| ------ | ---------- | --------------------------------------------------------------- |
| bool   | 0x1        | Literally just bytes that only contain 0 or 1                   |
| byte   | 0x1        | Normal Byte (0-255)                                             |
| short  | 0x2        | Normal Signed Short (-32768 - 32767)                            |
| int    | 0x4        | Normal Signed Integer (-2147483648 - 2147483647)                |
| long   | 0x8        | Normal Signed Long (-9223372036854775808 - 9223372036854775807) |
| d-long | 0x10       | Double Long (`you get the idea`)                                |
| float  | 0x4        | Floating Point Number (`varies`)                                |
| struct | 0x??       | Structures, varies in size                                      |
| ptr    | 0x4        | Pointer Address                                                 |

# Structs

> NOTE: This is HIGHLY unfinished and rushed.

> Descriptions suffixed with "(?)" means that I am unsure if that is the actual meaning or I haven't really looked into it. If that is the case then the descriptions may be a little weird since I pull them straight from the disassembly. :P

> Hint: Add the offset 0x502500 to pointers in IDA to get the actual addresses

## ItemInstance

> (Max Size: ???)

| Type | Offset | Description                     | Size |
| ---- | ------ | ------------------------------- | ---- |
| int  | 0x8    | Item Amount                     | 0x4  |
| int  | 0xC    | "Pop Time"?                     | 0x4  |
| int  | 0x10   | [Item](#item) Pointer           | 0x4  |
| int? | 0x14   | CompoundTag containing NBT data | 0x4  |
| byte | 0x18   | Is Item Empty                   | 0x1  |
| int  | 0x1C   | Damage/Data Value               | 0x4  |

*from reading the disassembly, it seems like this is probably a string

## Item

> (Max Size: ???)

| Type | Offset | Description                | Size |
| ---- | ------ | -------------------------- | ---- |
| int  | 0x8    | Item Amount                | 0x4  |
| int  | 0xC    | Max Stack Count            | 0x4  |
| int  | 0x10   | Max Damage Count           | 0x4  |
| int? | 0x14   | Item Icon(?)               | 0x4  |
| int? | 0x18   | Base Item Type(?)          | 0x4  |
| byte | 0x21   | Is Stacked via Data Value  | 0x1  |
| byte | 0x22   | Can Place in Offhand       | 0x1  |
| int? | 0x24   | Crafting Remaining Item(?) | 0x4  |
| int? | 0x48   | Description ID(?)          | 0x4  |
| int? | 0x4C   | Use Description ID(?)      | 0x4  |

## InsomniaComponent

> (Max Size: 0x10)

| Type  | Offset | Description                                         | Size |
| ----- | ------ | --------------------------------------------------- | ---- |
| ptr   | 0x0    | Pointer to the LivingEntity this is related to      | 0x4  |
| int   | 0x4    | Ticks Since Last Sleep                              | 0x4  |
| float | 0x8    | ??? (seems to always be 3.0, MAYBE amount of days?) | 0x4  |
| int   | 0xC    | Ticks For Insomnia To Occur                         | 0x4  |

## Inventory

> (Max Size: ???)

| Type | Offset | Description                   | Size |
| ---- | ------ | ----------------------------- | ---- |
| int  | 0x8    | Items Vector Start Address(?) | 0x4  |
| int  | 0x38   | ???                           | 0x4  |
| int  | 0x3C   | Max Slots Count               | 0x4  |
| int  | 0x40   | ???                           | 0x4  |
| int  | 0x44   | ???                           | 0x4  |
| int  | 0x6C   | Selected Slot Index           | 0x4  |

## Level

> (Max Size: ???)

| Type | Offset | Description                                   | Size |
| ---- | ------ | --------------------------------------------- | ---- |
| ptr  | 0x148  | [ClientChunkCache](#clientchunkcache) Pointer | 0x4  |
| ptr  | 0x14C  | LevelStorage Pointer                          | 0x4  |
| ptr  | 0x154  | LevelData Pointer                             | 0x4  |

## ClientChunkCache

> (Max Size: ???)

| Type | Offset | Description | Size |
| ---- | ------ | ----------- | ---- |

## LevelChunk

> (Max Size: ???)

| Type | Offset | Description                     | Size |
| ---- | ------ | ------------------------------- | ---- |
| ptr  | 0x0    | Biomes Pointer                  | 0x4  |
| ptr  | 0xC    | ElementStorage Pointer          | 0x4  |
| ptr  | 0x194  | Current [Level](#level) Pointer | 0x4  |
| ptr  | 0x1A8  | HeightMap Pointer               | 0x4  |
| int  | 0x1B8  | Chunk Pos X                     | 0x4  |
| int  | 0x1BC  | Chunk Pos Z                     | 0x4  |
| bool | 0x1C0  | Has Gaps To Check(?)            | 0x1  |
| int  | 0x1C4  | Biome Present Flag(?)           | 0x4  |
| int  | 0x1C8  | Block Entities (pointer??? idk) | 0x4  |
| byte | 0x1ED  | Is Ready(???)                   | 0x1  |
| byte | 0x1EE  | Is Unsaved                      | 0x1  |
| byte | 0x1EF  | ???                             | 0x1  |
| byte | 0x1F0  | Last Save Had Entities(?)       | 0x1  |
| long | 0x200  | Last Save Time                  | 0x8  |
| int  | 0x20C  | Lowest Heightmap                | 0x4  |
| long | 0x210  | Inhabited Time                  | 0x8  |
| int  | 0x228  | Chunk Version                   | 0x4  |
| bool | 0x241  | Has Lighting Been Dropped(?)    | 0x1  |

## LevelData

> (Max Size: ???)

| Type | Offset | Description                     | Size |
| ---- | ------ | ------------------------------- | ---- |
| long | 0x0    | World Seed                      | 0x8  |
| bool | 0x81   | Hardcore Mode                   | 0x1  |
| bool | 0x82   | Commands Allowed                | 0x1  |
| bool | 0x83   | Initialized                     | 0x1  |
| int  | 0x84   | Difficulty                      | 0x4  |
| bool | 0x88   | Difficulty Locked               | 0x1  |
| int  | 0xA4   | Cloud Height                    | 0x4  |
| bool | 0xA8   | Using New Sea Level             | 0x1  |
| bool | 0xA9   | Has been in Creative Previously | 0x1  |
| bool | 0xAA   | Has Bonus Chest                 | 0x1  |
| int  | 0xAC   | XZ Size                         | 0x4  |
| int  | 0xB0   | Nether Scale                    | 0x4  |

## CMinecraftApp

> (Max Size: 0x690)

Address: `0x10A2AFC0`
| Type | Offset | Description                        | Size |
| ---- | ------ | ---------------------------------- | ---- |
| bool | 0x184  | Is Game Started                    | 0x1  |
| byte | 0x185  | === Unused ===                     | 0x1  |
| bool | 0x186  | Is App Paused                      | 0x1  |
| int  | 0x1C0  | Gamemode(?)                        | 0x4  |
| bool | 0x1C4  | Load Saves from Folder             | 0x1  |
| int  | 0x1CC  | Disconnection Reason               | 0x4  |
| bool | 0x268  | Live Link Required(?)              | 0x1  |
| byte | 0x42D  | Player Colour 1(?)                 | 0x1  |
| byte | 0x42E  | Player Colour 2(?)                 | 0x1  |
| byte | 0x42F  | Player Colour 3(?)                 | 0x1  |
| byte | 0x430  | Player Colour 4(?)                 | 0x1  |
| byte | 0x431  | Player Colour 5(?)                 | 0x1  |
| byte | 0x432  | Player Colour 6(?)                 | 0x1  |
| byte | 0x433  | Player Colour 7(?)                 | 0x1  |
| byte | 0x434  | Player Colour 8(?)                 | 0x1  |
| bool | 0x62C  | Reset The Nether(?)                | 0x1  |
| bool | 0x62D  | Reset The End(?)                   | 0x1  |
| int  | 0x630  | Current Texture Pack ID            | 0x4  |
| int  | 0x68C  | Previously-Played Minigame ID      | 0x4  |

## Minecraft

> (Max Size: ???)

Pointer: `0x109CD8E4`
| Type | Offset | Description                        | Size |
| ---- | ------ | ---------------------------------- | ---- |
| ptr? | 0x104  | ??? (Something to do with fonts)   | 0x4  |
| ptr  | 0x144  | '`Gui`' Pointer                    | 0x4  |
| ptr  | 0x160  | '`TexturePackRepository`' Pointer  | 0x4  |
| ptr  | 0x24C  | '`Minigame`' Pointer               | 0x4  |
| ptr  | 0x250  | '`ClientMasterGameMode`' Pointer   | 0x4  |

## Entity

> (Max Size: 0x350)

| Type   | Offset | Description                               | Size |
| ------ | ------ | ----------------------------------------- | ---- |
| int    | 0xC    | Entity ID                                 | 0x4  |
| struct | 0x48   | Duplicate of 0x54(?)                      | 0xC  |
| struct | 0x54   | Current Position ([BlockPos](#blockpos))  | 0xC  |
| ptr    | 0xF0   | Current Entity Riding Pointer             | 0x4  |
| ptr    | 0xF8   | Current [Level](#level) Pointer           | 0x4  |
| float  | 0x1D8  | Step Height                               | 0x4  |
| bool   | 0x1EC  | Is in Water                               | 0x1  |
| bool   | 0x1ED  | Is Head in Water                          | 0x1  |
| int    | 0x1F0  | Invulnerability Frames in Ticks           | 0x4  |
| bool   | 0x1F5  | Is Immune to Fire                         | 0x1  |
| int    | 0x1F8  | ???                                       | 0x4  |
| ptr?   | 0x26C  | Display Name Pointer (i think)            | 0x4  |
| ptr?   | 0x348  | LivingEntity Pointer(???, could be wrong) | 0x4  |

## LivingEntity

> Inherits **Entity**
> (Max Size: 0x5F0)

| Type | Offset | Description                                       | Size |
| ---- | ------ | ------------------------------------------------- | ---- |
| int  | 0x3BC  | Attack Strength Ticker(?)                         | 0x4  |
| int  | 0x3E0  | Body Rotation                                     | 0x4  |
| int  | 0x3E4  | Duplicate of 0x3E0(?)                             | 0x4  |
| int  | 0x3E8  | Head Rotation                                     | 0x4  |
| int  | 0x3EC  | Duplicate of 0x3E8(?)                             | 0x4  |
| bool | 0x4A4  | Currently Jumping                                 | 0x1  |
| ptr  | 0x4A8  | '[InsomniaComponent](#insomniacomponent)' Pointer | 0x4  |

## Player

> Inherits **LivingEntity**  
> (Max Size: 0x868)

| Type      | Offset | Description                                                                         | Size |
| --------- | ------ | ----------------------------------------------------------------------------------- | ---- |
| ptr       | 0x5F0  | '[Inventory](#inventory)' Pointer                                                   | 0x4  |
| ptr       | 0x600  | InventoryMenu Pointer                                                               | 0x4  |
| ptr?      | 0x604  | Current Container Interacting With                                                  | 0x4  |
| struct    | 0x608  | '[FoodData](#fooddata)' Structure                                                   | 0x14 |
| bool      | 0x6C0  | Is Sleeping                                                                         | 0x1  |
| int       | 0x6C8  | Sleeping Timer (max 0x64)                                                           | 0x4  |
| int       | 0x6CC  | Death Fade Timer                                                                    | 0x4  |
| int?      | 0x6E0  | Respawn Position                                                                    | 0x4? |
| bool      | 0x6E4  | Is Respawn Forced                                                                   | 0x1  |
| struct    | 0x70C  | '[Abilities](#abilities)' Structure                                                 | 0x10 |
| int       | 0x71C  | Current XP Level                                                                    | 0x4  |
| int       | 0x720  | Current Raw XP Amount                                                               | 0x4  |
| float     | 0x724  | Current XP Bar Fullness                                                             | 0x4  |
| int?      | 0x728  | ???                                                                                 | 0x4  |
| int?      | 0x72C  | ???                                                                                 | 0x4  |
| int       | 0x730  | Enchantment Seed                                                                    | 0x4  |
| float     | 0x734  | Air Speed (can be modified, default is usually 0.02)                                | 0x4  |
| ptr       | 0x738  | 'ItemCooldowns' Pointer                                                             | 0x4  |
| int?      | 0x73C  | ???                                                                                 | 0x4  |
| bool      | 0x760  | IsReducedDebugInfo(???)                                                             | 0x1  |
| byte[]    | 0x761  | ???                                                                                 | 0x3  |
| ptr?      | 0x764  | Current Held Item                                                                   | 0x4  |
| ptr?      | 0x768  | Current Held Item 2(?)                                                              | 0x4  |
| int?      | 0x76C  | Something to do with "hand slots"                                                   | 0x4  |
| int?      | 0x770  | Something to do with "hand slots"                                                   | 0x4  |
| byte      | 0x781  | ???                                                                                 | 0x1  |
| byte[]    | 0x782  | ???                                                                                 | 0x2  |
| d-long    | 0x784  | UUID                                                                                | 0x10 |
| d-long    | 0x798  | UUID (Duplicate? I'd rely on the previous one though)                               | 0x10 |
| int       | 0x7D8  | Skin ID from Default Skin Pack (1 = steve, 2 = tennis steve, etc.) (Max 0x12)       | 0x4  |
| int       | 0x7DC  | Current Equipped Skin ID (custom skins are in hex and ORed with 0x80000000)         | 0x4  |
| int       | 0x7E0  | Current Equipped Cape ID (same format as skin id)                                   | 0x4  |
| int       | 0x7E4  | Player Colour Index (Max 0x7, idk why it isn't just a byte lmao)                    | 0x4  |
| int       | 0x7E8  | Unused(?)                                                                           | 0x4  |
| byte      | 0x7EC  | Something about Minigames? look into 0x0270F0BC                                     | 0x1  |
| int       | 0x7F0  | Something about Minigame Points? look into 0x027112DC                               | 0x4  |
| int       | 0x7F4  | Something about Minigame Checkpoints (glide?)? look into 0x02711638                 | 0x4  |
| byte      | 0x7F8  | ???                                                                                 | 0x1  |
| byte[]    | 0x7F9  | ???                                                                                 | 0x3  |
| int       | 0x7FC  | '[Player Privileges](#player-privileges)'                                           | 0x4  |
| int       | 0x800  | AdditionalModelParts(?) see 0x02728EC8                                              | 0x4  |
| byte      | 0x804  | Related to 0x800, see 0x0272B9D0                                                    | 0x1  |
| byte      | 0x805  | Related to 0x800, see 0x0272B9D8                                                    | 0x1  |
| byte[]    | 0x806  | ???                                                                                 | 0x2  |
| int       | 0x808  | Something related to round ending/camera??? look into 0x0270F76C                    | 0x4  |
| ptr(?)    | 0x80C  | Current Entity Spectating                                                           | 0x4  |
| int       | 0x810  | Something related to 0x80C and camera? look into 0x0272BDE0                         | 0x4  |
| bool      | 0x814  | Is Position Locked                                                                  | 0x1  |
| bool      | 0x815  | Able to take Collision Damage from Gliding                                          | 0x1  |
| byte[]    | 0x816  | Unused(?)                                                                           | 0x2  |
| float     | 0x818  | Lift Force Modifier(?)                                                              | 0x4  |
| int       | 0x81C  | Unused(?)                                                                           | 0x4  |
| float     | 0x820  | dupe of 0x120(?????) **HIGHLY** unsure, only ever mentioned here: 0x0270F1A0        | 0x4  |
| int       | 0x824  | Unused(?)                                                                           | 0x4  |
| int       | 0x828  | Collision Box Shape (0 is default, 1 is small (for spectators), 2 is none (buggy!)) | 0x4  |
| byte      | 0x82C  | Unused(?)                                                                           | 0x1  |
| byte[]    | 0x82D  | Unused(?)                                                                           | 0x3  |
| byte[]    | 0x830  | Unused(?)                                                                           | 0xC  |
| byte      | 0x83C  | Glide Ring Score Sound Variation (only 0 and 1 seem to be used)                     | 0x1  |
| byte[]    | 0x83D  | Unused(?)                                                                           | 0x3  |
| float     | 0x840  | Used for Calculating "Flapping" (like when running while jumping in the air)        | 0x4  |
| float     | 0x844  | Also used for Calculating "Flapping"                                                | 0x4  |
| float     | 0x848  | Duplicate of 0x844                                                                  | 0x4  |
| float     | 0x84C  | Duplicate of 0x840                                                                  | 0x4  |
| float     | 0x850  | Again, used for "flapping"                                                          | 0x4  |
| float     | 0x854  | Underwater Light Level                                                              | 0x4  |
| float     | 0x858  | Underwater Vision Scale                                                             | 0x4  |
| bool      | 0x85C  | Has Eaten Dried Kelp Before (used for Castaway achievement)                         | 0x1  |
| byte/bool | 0x85D  | Something to do with "Sleep with the Fishies" achievement                           | 0x1  |
| byte      | 0x85E  | ???                                                                                 | 0x1  |
| byte      | 0x85F  | ???                                                                                 | 0x1  |
| int       | 0x860  | ???                                                                                 | 0x4  |
| int       | 0x864  | ???                                                                                 | 0x4  |

## FoodData

> (Max Size: 0x14)

| Type  | Offset | Description           | Size |
| ----- | ------ | --------------------- | ---- |
| int   | 0x0    | Current Hunger Amount | 0x4  |
| float | 0x4    | Current Saturation    | 0x4  |
| int   | 0x8    | Current Exhaustion    | 0x4  |
| int   | 0xC    | ???                   | 0x4  |
| int   | 0x10   | Last Hunger Amount    | 0x4  |

## FoodItem

> (Max Size: 0x8C)

| Type | Offset | Description                           | Size |
| ---- | ------ | ------------------------------------- | ---- |
| bool | 0x80   | Is Meat (used for feeding wolves)     | 0x1  |
| bool | 0x81   | Can Eat Even If Full?                 | 0x1  |
| bool | 0x82   | Faster Eat Duration (dried kelp only) | 0x1  |
| byte | 0x83   | Unused                                | 0x1  |

## Player Privileges

> (Max Size: 0x4)

| Bit Position | Description          |
| ------------ | -------------------- |
| 3            | Can attack players   |
| 4            | "Moderator"          |
| 5            | "Can Fly"            |
| 6            | "Disable Exhaustion" |
| 7            | "Invisible"          |
| 8            | "Invulnerable"       |
| 10           | Can attack animals   |

## Abilities

> (Max Size: 0x10)

| Type   | Offset | Description                                  | Size |
| ------ | ------ | -------------------------------------------- | ---- |
| bool   | 0x0    | Is Invulnerable (doesn't seem to work)       | 0x1  |
| bool   | 0x1    | Currently Flying                             | 0x1  |
| bool   | 0x2    | Can Fly (not related to the host permission) | 0x1  |
| bool   | 0x3    | Can Use Command Blocks                       | 0x1  |
| bool   | 0x4    | ??? (seems to always be set to `1`)          | 0x1  |
| byte[] | 0x5    | Unused                                       | 0x3  |
| float  | 0x8    | Current Flying Speed (doesn't seem to work)  | 0x4  |
| float  | 0xC    | Current Walking Speed (only changes FOV)     | 0x4  |

## BlockPos

> (Max Size: 0xC)

| Type | Offset | Description | Size |
| ---- | ------ | ----------- | ---- |
| int  | 0x0    | X Position  | 0x4  |
| int  | 0x4    | Y Position  | 0x4  |
| int  | 0x8    | Z Position  | 0x4  |
