# Monuments Watcher  

A plugin that allows other plugins to interact with players and entities in monuments via API.  

The list of all monuments can be viewed in the:  
- **Default**(Source of monument boundaries when changing the map or recreating boundaries) - ***SERVER***\oxide\data\MonumentsWatcher\DefaultBounds.json  
- **Vanilla** - ***SERVER***\oxide\data\MonumentsWatcher\MonumentsBounds.json  
- **Custom** - ***SERVER***\oxide\data\MonumentsWatcher\CustomMonumentsBounds.json  

**Note:** **MonumentsWatcher** is utilized as an **API** for other plugins. You won't obtain any functionality beyond displaying monument boundaries without an additional plugin.  

## Contacts  

- **Telegram:** [https://t.me/iiiaka](https://t.me/iiiaka)  
- **Discord:** @iiiaka  
- **GitHub:** [https://github.com/IIIaKa](https://github.com/IIIaKa)  
- **uMod:** [https://umod.org/user/IIIaKa](https://umod.org/user/IIIaKa)  
- **Codefling:** [https://codefling.com/iiiaka](https://codefling.com/iiiaka)  
- **LoneDesign:** [https://lone.design/vendor/iiiaka/](https://lone.design/vendor/iiiaka/)  
- **GitHub repository page:** [https://github.com/IIIaKa/MonumentsWatcher](https://github.com/IIIaKa/MonumentsWatcher)  

## Donations  

- **USDT TRC20:** `TLN9Tsrdmt96yFCXZTfh4NLtyzWYGkqTA3`  
- **USDT TON:** `UQDma5Ovkk7M9Qve-4P2njmrgSXZQdACU0gLCGNEgkXDlngn`  
- **TON:** `UQDma5Ovkk7M9Qve-4P2njmrgSXZQdACU0gLCGNEgkXDlngn`  

## Features  

- The ability to **automatically generate** boundaries for **vanilla** and **custom** monuments;  
- The ability to **automatically regenerate** boundaries for monuments **on wipe**;  
- The ability to **automatically adding languages** for **custom** monuments;  
- The ability to **manually configure** boundaries for monuments;  
- The ability to **track the entrance and exit** of **players**, **npcs** and **entities** in a **Monument** and **CargoShip**;  
- The ability to **display boundaries**.  

## Permissions  

- **`monumentswatcher.admin`** - Provides the capability to **recreate** or **display monument boundaries**.

## Default Configuration  

```json
{
  "Chat command": "monument",
  "Is it worth enabling GameTips for messages?": true,
  "List of language keys for creating language files": [
    "en"
  ],
  "Is it worth recreating boundaries(excluding custom monuments) upon detecting a wipe?": true,
  "List of tracked categories of monuments. Leave blank to track all": [],
  "Wipe ID": null,
  "Version": {
    "Major": 0,
    "Minor": 1,
    "Patch": 8
  }
}
```  

## Localization  

- **ENG:** [https://pastebin.com/nsjBCqZe](https://pastebin.com/nsjBCqZe)  
- **RUS:** [https://pastebin.com/ut2icv9T](https://pastebin.com/ut2icv9T)  

**Note:** After the plugin initialization, keys for custom monuments will be automatically added.  

## Commands  

- **show \*monumentID\***(optional) **\*floatValue\***(optional) - Display the boundary of the monument you are in or specified. The display will last for the specified time or 30 seconds;  
- **list** - List of available monuments;  
- **rotate \*monumentID\***(optional) **\*floatValue\***(optional) - Rotate the monument you are in or specified, either in the direction you are looking or in the specified direction;  
- **recreate custom/all**(optional) - Recreate the boundaries of vanilla/custom/all monuments.  

**Note:** Instead of a **monumentID**, you can leave it empty, but you must be inside a monument. You can also use the word '**closest**' to select the nearest monument to you.  

**Example:**
- **/monument show closest**  
- **/monument show gas_station_1**  
- **/monument show gas_station_1_4**  
- **/monument rotation**  
- **/monument rotation closest**  
- **/monument rotation gas_station_1_0 256.5**  
- **/monument recreate**  

## Developer Hooks  

### OnMonumentsWatcherLoaded  
Called after the **MonumentsWatcher** plugin is **fully loaded** and **ready**.  
No return behaviour.  

```csharp
void OnMonumentsWatcherLoaded()
{
  Puts("MonumentsWatcher plugin is ready!");
}
```  

### OnCargoWatcherCreated  
Called when a **watcher is created** for a **CargoShip**.  
No return behaviour.  

```csharp
void OnCargoWatcherCreated(string monumentID, string type)
{
  Puts($"Watcher for monument {monumentID}({type}) has been created!");
}
```  

### OnCargoWatcherDeleted  
Called when a **watcher is removed** for a **CargoShip**.  
No return behaviour.  

```csharp
void OnCargoWatcherDeleted(string monumentID)
{
  Puts($"Watcher for monument {monumentID} has been deleted!");
}
```  

### OnPlayerEnteredMonument  
Called when a **player enters** any monument.  
No return behaviour.  

```csharp
void OnPlayerEnteredMonument(string monumentID, BasePlayer player, string type, string oldMonumentID)
{
  Puts($"{player.displayName} entered to {monumentID}({type}). His previous monument was {oldMonumentID}");
}
```  

### OnNpcEnteredMonument  
Called when an **NPC player enters** any monument.  
No return behaviour.  

```csharp
void OnNpcEnteredMonument(string monumentID, BasePlayer npcPlayer, string type, string oldMonumentID)
{
  Puts($"Npc({npcPlayer.displayName}) entered to {monumentID}({type}). Previous monument was {oldMonumentID}");
}
```  

### OnEntityEnteredMonument  
Called when any other **BaseEntity enters** any monument.  
No return behaviour.  

```csharp
void OnEntityEnteredMonument(string monumentID, BaseEntity entity, string type, string oldMonumentID)
{
  Puts($"Entity({entity.net.ID}) entered to {monumentID}({type}). Previous monument was {oldMonumentID}");
}
```  

### OnPlayerExitedMonument  
Called when a **player exits** any monument.  
No return behaviour.  

```csharp
void OnPlayerExitedMonument(string monumentID, BasePlayer player, string type, string reason, string newMonumentID)
{
  Puts($"{player.displayName} left from {monumentID}({type}). Reason: {reason}. They are now at '{newMonumentID}'.");
}
```  

### OnNpcExitedMonument  
Called when an **NPC player exits** any monument.  
No return behaviour.  

```csharp
void OnNpcExitedMonument(string monumentID, BasePlayer npcPlayer, string type, string reason, string newMonumentID)
{
  Puts($"Npc({npcPlayer.displayName}) left from {monumentID}({type}). Reason: {reason}. They are now in {newMonumentID}");
}
```  

### OnEntityExitedMonument  
Called when any other **BaseEntity exits** any monument.  
No return behaviour.  

```csharp
void OnEntityExitedMonument(string monumentID, BaseEntity entity, string type, string reason, string newMonumentID)
{
  Puts($"Entity({entity.net.ID}) left from {monumentID}({type}). Reason: {reason}. They are now in {newMonumentID}");
}
```  

## Developer API  

```csharp
[PluginReference]
private Plugin MonumentsWatcher;
```  

**There are 13 types of monuments:**  
- **SafeZone**(0):  
  - **Bandit Camp**, **Outpost**, **Fishing Village**, **Ranch** and **Large Barn**.  
- **RadTown**(1):  
  - **Airfield**, **Arctic Research Base**, **Abandoned Military Base**, **Giant Excavator Pit**, **Ferry Terminal**, **Harbor**, **Junkyard**, **Launch Site**;  
  - **Military Tunnel**, **Missile Silo**, **Power Plant**, **Sewer Branch**, **Satellite Dish**, **The Dome**, **Toxic Village**(Legacy Radtown), **Train Yard** and **Water Treatment Plant**.  
- **RadTownWater**(2):  
  - **Oil Rigs**, **Underwater Labs** and **CargoShip**.  
- **RadTownSmall**(3):  
  - **Lighthouse**, **Oxum's Gas Station**, **Abandoned Supermarket** and **Mining Outpost**.  
- **TunnelStation**(4)  
- **MiningQuarry**(5):  
  - **Sulfur Quarry**, **Stone Quarry** and **HQM Quarry**.  
- **BunkerEntrance**(6)  
- **Cave**(7)  
- **Swamp**(8)  
- **IceLake**(9)  
- **PowerSubstation**(10)  
- **WaterWell**(11)  
- **Custom**(12)  

**There are 25 api methods:**  
- _General:_
  - **GetAllMonuments**  
  - **GetAllMonumentsCategories**  
  - **GetMonumentsByCategory**  
  - **GetMonumentCategory**  
  - **GetMonumentDisplayName**  
  - **GetMonumentDisplayNameByLang**  
  - **GetMonumentPosition**  
  - **GetMonumentByPos**  
  - **GetMonumentsByPos**  
  - **GetClosestMonument**  
  - **IsPosInMonument**  
  - **ShowBounds**  
- _Players:_  
  - **GetMonumentPlayers**  
  - **GetPlayerMonument**  
  - **GetPlayerMonuments**  
  - **GetPlayerClosestMonument**  
  - **IsPlayerInMonument**  
- _NPCs:_  
  - **GetMonumentNpcs**  
  - **GetNpcMonument**  
  - **GetNpcMonuments**  
  - **IsNpcInMonument**  
- _Entities:_  
  - **GetMonumentEntities**  
  - **GetEntityMonument**  
  - **GetEntityMonuments**  
  - **IsEntityInMonument**  

### GetAllMonuments  
Used to retrieve an array of IDs for all available monuments.  

```csharp
(string[])(MonumentsWatcher?.Call("GetAllMonuments") ?? Array.Empty<string>());
```  

### GetAllMonumentsCategories  
Used to retrieve a dictionary of IDs and categories for all available monuments.  

 ```csharp
(Dictionary<string, string>)(MonumentsWatcher?.Call("GetAllMonumentsCategories") ?? new Dictionary<string, string>());
```  

### GetMonumentsByCategory  
Used to retrieve all available monuments by category.  
To call the **GetMonumentsByCategory** method, you need to pass 1 parameter:  
1. **monument category** as a **string**.  

```csharp
(string[])(MonumentsWatcher?.Call("GetMonumentsByCategory", "SafeZone") ?? Array.Empty<string>());
```  

### GetMonumentCategory  
Used to retrieve the category of the specified monument.  
Returns an **empty string** on failure.  
To call the **GetMonumentCategory** method, you need to pass 1 parameter:  
1. **monumentID** as a **string**.  

```csharp
(string)(MonumentsWatcher?.Call("GetMonumentCategory", monumentID) ?? string.Empty);
```  

### GetMonumentDisplayName  
Used to retrieve the nicename of a monument in the player's language.  
Returns an **empty string** on failure.  
To call the **GetMonumentDisplayName** method, you need to pass 3 parameters:  
1. **monumentID** as a **string**;  
2. Available options:  
  **userID** as a **ulong** or a **string**;  
  **player** as a **BasePlayer** or an **IPlayer**.  
3. **displaySuffix** as a **bool**. Should the suffix be displayed in the name if there are multiple such monuments? This parameter is **optional**.  

```csharp
(string)(MonumentsWatcher?.Call("GetMonumentDisplayName", monumentID, player.userID, true) ?? string.Empty);//(ulong)userID
(string)(MonumentsWatcher?.Call("GetMonumentDisplayName", monumentID, player, true) ?? string.Empty);//(BasePlayer/IPlayer)player
(string)(MonumentsWatcher?.Call("GetMonumentDisplayName", monumentID, player.UserIDString, true) ?? string.Empty);//(string)userID ***recommended option***
```  

### GetMonumentDisplayNameByLang  
Used to retrieve the nicename of a monument in the specified language.  
Returns an **empty string** on failure.  
To call the **GetMonumentDisplayNameByLang** method, you need to pass 3 parameters:  
1. **monumentID** as a **string**;  
2. **two-char language** as a **string**;  
3. **displaySuffix** as a **bool**. Should the suffix be displayed in the name if there are multiple such monuments? This parameter is **optional**.  

```csharp
(string)(MonumentsWatcher?.Call("GetMonumentDisplayNameByLang", monumentID, "en", true) ?? string.Empty);
```  

### GetMonumentPosition  
Used to retrieve the Vector3 position of the specified monument.  
Returns **Vector3.zero** on failure.  
To call the **GetMonumentPosition** method, you need to pass 1 parameter:  
1. **monumentID** as a **string**.  

```csharp
(Vector3)(MonumentsWatcher?.Call("GetMonumentPosition", monumentID) ?? Vector3.zero);
```  

### GetMonumentByPos  
Used to retrieve the monument at the specified position.  
Returns an **empty string** on failure.  
To call the **GetMonumentByPos** method, you need to pass 1 parameter:  
1. **position** as a **Vector3**.  

```csharp
(string)(MonumentsWatcher?.Call("GetMonumentByPos", pos) ?? string.Empty);
```  
**Note:** This method returns the first encountered monument. Occasionally, there may be multiple monuments at a single point. Therefore, it is recommended to use the **GetMonumentsByPos** method.  

### GetMonumentsByPos  
Used to retrieve all monuments at the specified position.  
Returns **null** on failure.  
To call the **GetMonumentsByPos** method, you need to pass 1 parameter:  
1. **position** as a **Vector3**.  

```csharp
(string[])(MonumentsWatcher?.Call("GetMonumentsByPos", pos) ?? Array.Empty<string>());
```  

### GetClosestMonument  
Used to retrieve the nearest monument to the specified position.  
Returns an **empty string** on failure.  
To call the **GetClosestMonument** method, you need to pass 1 parameter:  
1. **position** as a **Vector3**.  

```csharp
(string)(MonumentsWatcher?.Call("GetClosestMonument", pos) ?? string.Empty);
```  

### IsPosInMonument  
Used to check whether the specified position is within the specified monument.  
Returns a **false** on failure.  
To call the **IsPosInMonument** method, you need to pass 2 parameters:  
1. **monumentID** as a **string**;  
2. **position** as a **Vector3**.  

```csharp
(bool)(MonumentsWatcher?.Call("IsPosInMonument", monumentID, pos) ?? false);
```  

### ShowBounds  
Used to display the boundaries of the specified monument to the specified player.  
No return behaviour.  
To call the **ShowBounds** method, you need to pass 3 parameters:  
1. **monumentID** as a **string**;  
2. **player** as a **BasePlayer**;  
3. **displayDuration** as a **float**. Duration of displaying the monument boundaries in seconds. This parameter is **optional**.  

```csharp
MonumentsWatcher?.Call("ShowBounds", monumentID, player, 20f);
```  
**Note:** Since an Admin flag is required for rendering, players without it will be temporarily granted an Admin flag and promptly revoked.  

### GetMonumentPlayers  
Used to retrieve an array of all players located in the specified monument.  
Returns **null** on failure.  
To call the **GetMonumentPlayers** method, you need to pass 1 parameter:  
1. **monumentID** as a **string**.  

```csharp
(BasePlayer[])(MonumentsWatcher?.Call("GetMonumentPlayers", monumentID) ?? Array.Empty<BasePlayer>());
```  

### GetPlayerMonument  
Used to retrieve the monument in which the specified player is located.  
Returns an **empty string** on failure.  
To call the **GetPlayerMonument** method, you need to pass 1 parameter:  
1. Available options:  
  **player** as a **BasePlayer**;  
  **userID** as a **ulong** or a **string**.  

```csharp
(string)(MonumentsWatcher?.Call("GetPlayerMonument", player.UserIDString) ?? string.Empty);//(string)userID
(string)(MonumentsWatcher?.Call("GetPlayerMonument", player) ?? string.Empty);//(BasePlayer)player
(string)(MonumentsWatcher?.Call("GetPlayerMonument", player.userID) ?? string.Empty);//(ulong)userID ***recommended option***
```  

### GetPlayerMonuments  
Used to retrieve all monuments in which the specified player is located.  
Returns **null** on failure.  
To call the **GetPlayerMonuments** method, you need to pass 1 parameter:  
1. Available options:  
  **player** as a **BasePlayer**;  
  **userID** as a **ulong** or a **string**.  

```csharp
(string[])(MonumentsWatcher?.Call("GetPlayerMonuments", player.UserIDString) ?? Array.Empty<string>());//(string)userID
(string[])(MonumentsWatcher?.Call("GetPlayerMonuments", player) ?? Array.Empty<string>());//(BasePlayer)player
(string[])(MonumentsWatcher?.Call("GetPlayerMonuments", player.userID) ?? Array.Empty<string>());//(ulong)userID ***recommended option***
```  

### GetPlayerClosestMonument  
Used to retrieve the nearest monument to the specified player.  
Returns an **empty string** on failure.  
To call the **GetPlayerClosestMonument** method, you need to pass 1 parameter:  
1. Available options:  
  **player** as a **BasePlayer**;  
  **userID** as a **ulong** or a **string**.  

```csharp
(string)(MonumentsWatcher?.Call("GetPlayerClosestMonument", player.UserIDString) ?? string.Empty);//(string)userID
(string)(MonumentsWatcher?.Call("GetPlayerClosestMonument", player.userID) ?? string.Empty);//(ulong)userID
(string)(MonumentsWatcher?.Call("GetPlayerClosestMonument", player) ?? string.Empty);//(BasePlayer)player ***recommended option***
```  

### IsPlayerInMonument  
Used to check whether the specified player is in the specified monument.  
Returns a **false** on failure.  
To call the **IsPlayerInMonument** method, you need to pass 1 parameter:  
1. **monumentID** as a **string**;  
2. Available options:  
  **player** as a **BasePlayer**;  
  **userID** as a **ulong** or a **string**.  

```csharp
(bool)(MonumentsWatcher?.Call("IsPlayerInMonument", monumentID, player.UserIDString) ?? false);//(string)userID
(bool)(MonumentsWatcher?.Call("IsPlayerInMonument", monumentID, player) ?? false);//(BasePlayer)player
(bool)(MonumentsWatcher?.Call("IsPlayerInMonument", monumentID, player.userID) ?? false);//(ulong)userID ***recommended option***
```  

### GetMonumentNpcs  
Used to retrieve an array of all npcs located in the specified monument.  
Returns **null** on failure.  
To call the **GetMonumentNpcs** method, you need to pass 1 parameter:  
1. **monumentID** as a **string**.  

```csharp
(BasePlayer[])(MonumentsWatcher?.Call("GetMonumentNpcs", monumentID) ?? Array.Empty<BasePlayer>());
```  

### GetNpcMonument  
Used to retrieve the monument in which the specified npc is located.  
Returns an **empty string** on failure.  
To call the **GetNpcMonument** method, you need to pass 1 parameter:  
1. Available options:  
  **npcPlayer** as a **BasePlayer**;  
  **netID** as a **NetworkableId**.  

```csharp
(string)(MonumentsWatcher?.Call("GetNpcMonument", npcPlayer) ?? string.Empty);//(BasePlayer)npcPlayer
(string)(MonumentsWatcher?.Call("GetNpcMonument", npcPlayer.net.ID) ?? string.Empty);//(NetworkableId)netID ***recommended option***
```  

### GetNpcMonuments  
Used to retrieve all monuments in which the specified npc is located.  
Returns **null** on failure.  
To call the **GetNpcMonuments** method, you need to pass 1 parameter:  
1. Available options:  
  **npcPlayer** as a **BasePlayer**;  
  **netID** as a **NetworkableId**.  

```csharp
(string[])(MonumentsWatcher?.Call("GetNpcMonuments", npcPlayer) ?? Array.Empty<string>());//(BasePlayer)npcPlayer
(string[])(MonumentsWatcher?.Call("GetNpcMonuments", npcPlayer.net.ID) ?? Array.Empty<string>());//(NetworkableId)netID ***recommended option***
```  

### IsNpcInMonument  
Used to check whether the specified npc is in the specified monument.  
Returns a **false** on failure.  
To call the **IsNpcInMonument** method, you need to pass 1 parameter:  
1. **monumentID** as a **string**;  
2. Available options:  
  **npcPlayer** as a **BasePlayer**;  
  **netID** as a **NetworkableId**.  

```csharp
(bool)(MonumentsWatcher?.Call("IsNpcInMonument", monumentID, npcPlayer.net.ID) ?? false);//(NetworkableId)netID
(bool)(MonumentsWatcher?.Call("IsNpcInMonument", monumentID, npcPlayer) ?? false);//(BasePlayer)npcPlayer ***recommended option***
```  

### GetMonumentEntities  
Used to retrieve an array of all entities located in the specified monument.  
Returns **null** on failure.  
To call the **GetMonumentEntities** method, you need to pass 1 parameter:  
1. **monumentID** as a **string**.  

```csharp
(BaseEntity[])(MonumentsWatcher?.Call("GetMonumentEntities", monumentID) ?? Array.Empty<BaseEntity>());
```  

### GetEntityMonument  
Used to retrieve the monument in which the specified entity is located.  
Returns an **empty string** on failure.  
To call the **GetEntityMonument** method, you need to pass 1 parameter:  
1. Available options:  
  **entity** as a **BaseEntity**;  
  **netID** as a **NetworkableId**.  

```csharp
(string)(MonumentsWatcher?.Call("GetEntityMonument", entity) ?? string.Empty);//(BaseEntity)entity
(string)(MonumentsWatcher?.Call("GetEntityMonument", entity.net.ID) ?? string.Empty);//(NetworkableId)netID ***recommended option***
```  

### GetEntityMonuments  
Used to retrieve all monuments in which the specified entity is located.  
Returns **null** on failure.  
To call the **GetEntityMonuments** method, you need to pass 1 parameter:  
1. Available options:  
  **entity** as a **BaseEntity**;  
  **netID** as a **NetworkableId**.  

```csharp
(string[])(MonumentsWatcher?.Call("GetEntityMonuments", entity) ?? Array.Empty<string>());//(BaseEntity)entity
(string[])(MonumentsWatcher?.Call("GetEntityMonuments", entity.net.ID) ?? Array.Empty<string>());//(NetworkableId)netID ***recommended option***
```  

### IsEntityInMonument  
Used to check whether the specified entity is in the specified monument.  
Returns a **false** on failure.  
To call the **IsEntityInMonument** method, you need to pass 1 parameter:  
1. **monumentID** as a **string**;  
2. Available options:  
  **entity** as a **BaseEntity**;  
  **netID** as a **NetworkableId**.  

```csharp
(bool)(MonumentsWatcher?.Call("IsEntityInMonument", monumentID, entity.net.ID) ?? false);//(NetworkableId)netID
(bool)(MonumentsWatcher?.Call("IsEntityInMonument", monumentID, entity) ?? false);//(BaseEntity)entity ***recommended option***
```  
