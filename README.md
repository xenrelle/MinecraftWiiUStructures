# Data Types Table

| Type   | Usual Size | Description       |
| ------ | ---------- | ----------------- |
| bool   | 0x1        | Literally just bytes that only contain 0 or 1 |
| byte   | 0x1        | Normal Byte (0-255) |
| short  | 0x2        | Normal Signed Short (-32768 - 32767) |
| int    | 0x4        | Normal Signed Integer (-2147483648 - 2147483647) |
| long   | 0x8        | Normal Signed Long (-9223372036854775808 - 9223372036854775807) |
| d-long | 0x10       | Double Long (`you get the idea`) |
| float  | 0x4        | Floating Point Number (`varies`) |
| struct | 0x??       | Structures, varies in size |
| ptr    | 0x4        | Pointer Address |

# Structs
> NOTE: This is HIGHLY unfinished and rushed.

> Descriptions suffixed with "(?)" means that I am unsure if that is the actual meaning or I haven't really looked into it. If that is the case then the descriptions may be a little weird since I pull them straight from the disassembly.

> Hint: Add the offset 0x502500 to pointers in IDA to get the actual addresses

## ItemInstance
> (Max Size: ???)

| Type | Offset | Description           | Size |
| ---- | ------ | --------------------- | ---- |
| int  | 0x8    | Item Amount           | 0x4  |
| int  | 0xC    | "Pop Time"?           | 0x4  |
| int  | 0x10   | [Item](#item) Pointer | 0x4  |
| int? | 0x14   | Item Tag*             | 0x4  |
| byte | 0x18   | ???                   | 0x1  |
| int  | 0x1C   | Damage/Data Value     | 0x4  |
  
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

## Inventory
> (Max Size: ???)

| Type | Offset | Description      | Size |
| ---- | ------ | ---------------- | ---- |
| int  | 0x38    | ???             | 0x4  |
| int  | 0x3C    | Max Slots Count | 0x4  |
| int  | 0x40    | ???             | 0x4  |
| int  | 0x44    | ???             | 0x4  |


## Level
> (Max Size: ???)

| Type | Offset | Description          | Size |
| ---- | ------ | -------------------- | ---- |
| int  | 0x14C  | LevelStorage Pointer | 0x4  |
| int  | 0x154  | LevelData Pointer    | 0x4  |


## LevelChunk
> (Max Size: ???)

| Type | Offset | Description | Size |
| ---- | ------ | ----------- | ---- |
| int  | 0x1B8  | Chunk Pos X | 0x4  |
| int  | 0x1BC  | Chunk Pos Z | 0x4  |


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
| bool | 0xA9   | Has been in Creative previously | 0x1  |
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


## Player
> (Max Size: 0x868)

| Type      | Offset | Description                                                                          | Size |
| --------- | ------ | ------------------------------------------------------------------------------------ | ---- |
| struct    | 0x48   | Duplicate of 0x54(?)                                                                 | 0xC  |
| struct    | 0x54   | Current Position ([BlockPos](#blockpos))                                             | 0xC  |
| ptr       | 0xF8   | Current [Level](#level) Pointer                                                      | 0x4  |
| int       | 0x1F8  | ???                                                                                  | 0x4  |
| ptr?      | 0x26C  | Display Name Pointer (i think)                                                       | 0x4  |
| ptr?      | 0x348  | LivingEntity Pointer(?)                                                              | 0x4  |
| int       | 0x3BC  | Attack Strength Ticker(?)                                                            | 0x4  |
| int       | 0x3E0  | Body Rotation?                                                                       | 0x4  |
| int       | 0x4A8  | ???                                                                                  | 0x4  |
| ptr       | 0x5F0  | '[Inventory](#inventory)' Pointer                                                    | 0x4  |
| int       | 0x600  | No Container Interaction Value (game copies this value to 0x604 to close containers) | 0x4  |
| ptr?      | 0x604  | Current Container Interacting With                                                   | 0x4  |
| struct    | 0x608  | ([FoodData](#fooddata))                                                              | 0xC+ |
| bool      | 0x6C0  | Is Sleeping                                                                          | 0x1  |
| int       | 0x6C8  | Sleeping Timer (max 0x64)                                                            | 0x4  |
| int       | 0x6CC  | Death Fade Timer                                                                     | 0x4  |
| (idk)     | 0x6E0  | Respawn Position                                                                     | 0x?  |
| bool      | 0x6E4  | Is Respawn Forced                                                                    | 0x1  |
| byte      | 0x70C  | Portal Wait Time                                                                     | 0x1  |
| bool      | 0x70D  | Is Currently Flying                                                                  | 0x1  |
| byte/bool | 0x70E  | ???                                                                                  | 0x1  |
| bool      | 0x70F  | Is allowed to use Command Blocks                                                     | 0x1  |
| bool      | 0x710  | Is allowed to build                                                                  | 0x1  |
| int       | 0x71C  | Current XP Level                                                                     | 0x4  |
| int       | 0x720  | Current Raw XP Amount                                                                | 0x4  |
| int       | 0x730  | Enchantment Seed                                                                     | 0x4  |
| d-long    | 0x784  | UUID                                                                                 | 0x10 |
| d-long    | 0x798  | UUID (Duplicate? I'd rely on the previous one though)                                | 0x10 |
| int       | 0x7D8  | Skin ID from Default Skin Pack (1 = steve, 2 = tennis steve, etc.) (Max 0x12)        | 0x4  |
| int       | 0x7DC  | Current Equipped Skin ID (custom skins are in hex and ORed with 0x80000000)          | 0x4  |
| int       | 0x7E0  | Current Equipped Cape ID (same format as skin id)                                    | 0x4  |
| int       | 0x7E4  | Player Colour Index (Max 0x7, idk why it isn't just a byte lmao)                     | 0x4  |
| int       | 0x7E8  | ???                                                                                  | 0x4  |
| byte      | 0x7EC  | ???                                                                                  | 0x1  |
| int       | 0x7FC  | ???                                                                                  | 0x4  |
| int       | 0x808  | ???                                                                                  | 0x4  |
| ptr(?)    | 0x80C  | Current Entity Spectating                                                            | 0x4  |
| bool      | 0x814  | Is Position Locked                                                                   | 0x1  |
| float     | 0x854  | Underwater Light Level                                                               | 0x4  |
| float     | 0x858  | Underwater Vision Scale                                                              | 0x4  |
| bool      | 0x85C  | Has Eaten Dried Kelp Before (used for Castaway achievement)                          | 0x1  |
| byte/bool | 0x85D  | Something to do with "Sleep with the Fishies" achievement                            | 0x1  |
| byte      | 0x85E  | ???                                                                                  | 0x1  |
| byte      | 0x85F  | ???                                                                                  | 0x1  |
| int       | 0x860  | ???                                                                                  | 0x4  |
| int       | 0x864  | ???                                                                                  | 0x4  |


## FoodData
> (Max Size: ???)

| Type  | Offset | Description            | Size |
| ----- | ------ | ---------------------- | ---- |
| int   | 0x0    | Current Hunger Amount  | 0x4  |
| float | 0x4    | Current Saturation     | 0x4  |
| int   | 0x8    | Current Exhaustion     | 0x4  |


## BlockPos
> (Max Size: 0xC)

| Type  | Offset | Description | Size |
| ----- | ------ | ----------- | ---- |
| int   | 0x0    | X Position  | 0x4  |
| int   | 0x4    | Y Position  | 0x4  |
| int   | 0x8    | Z Position  | 0x4  |
