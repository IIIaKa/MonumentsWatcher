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

- **USDT TRC20:** `TGd19rg8amSDvspnMLyAcGiquNGMoC73SH`  
- **USDT TON:** `UQAcBjQGjTNXCmrOAm5fJDL0fBgnASsnni7_jSIAix2METXp`  
- **TON:** `UQAcBjQGjTNXCmrOAm5fJDL0fBgnASsnni7_jSIAix2METXp`  

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
    "Patch": 11
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
void OnCargoWatcherCreated(string monumentID, string category, CargoShip cargoShip)
{
  Puts($"Watcher for monument '{monumentID}'({category}) has been created!");
}
```  

### OnCargoWatcherDeleted  
Called when a **watcher is removed** for a **CargoShip**.  
No return behaviour.  

```csharp
void OnCargoWatcherDeleted(string monumentID)
{
  Puts($"Watcher for monument '{monumentID}' has been deleted!");
}
```  

### OnSpawnableWatcherCreated  
Called when a **watcher is created** for a **Spawnable monument**.  
No return behaviour.  

```csharp
void OnSpawnableWatcherCreated(string monumentID, string category, BaseEntity entity)
{
  Puts($"Watcher for monument '{monumentID}'({category}) has been created!");
}
```  

### OnSpawnableWatcherDeleted  
Called when a **watcher is removed** for a **Spawnable monument**.  
No return behaviour.  

```csharp
void OnSpawnableWatcherDeleted(string monumentID)
{
  Puts($"Watcher for monument '{monumentID}' has been deleted!");
}
```  

### OnPlayerEnteredMonument  
Called when a **player enters** any monument.  
No return behaviour.  

```csharp
void OnPlayerEnteredMonument(string monumentID, BasePlayer player, string category, string oldMonumentID)
{
  Puts($"Player '{player.displayName}' entered to '{monumentID}'({category}). His previous monument was '{oldMonumentID}'.");
}
```  

### OnNpcEnteredMonument  
Called when an **NPC player enters** any monument.  
No return behaviour.  

```csharp
void OnNpcEnteredMonument(string monumentID, BaseNPC2 npcPlayer, string category, string oldMonumentID)
{
  Puts($"Npc '{npcPlayer.displayName}'({npcPlayer.GetType()}) entered to '{monumentID}'({category}). Previous monument was '{oldMonumentID}'.");
}

void OnNpcEnteredMonument(string monumentID, BasePlayer npcPlayer, string category, string oldMonumentID)
{
  Puts($"Npc '{npcPlayer.displayName}'({npcPlayer.GetType()}) entered to '{monumentID}'({category}). Previous monument was '{oldMonumentID}'.");
}
```  

### OnAnimalEnteredMonument  
Called when an **Animal enters** any monument.  
No return behaviour.  

```csharp
void OnAnimalEnteredMonument(string monumentID, BaseNPC2 animal, string category, string oldMonumentID)
{
  Puts($"Animal '{animal.displayName}'({animal.GetType()}) entered to '{monumentID}'({category}). Previous monument was '{oldMonumentID}'.");
}

void OnAnimalEnteredMonument(string monumentID, BaseAnimalNPC animal, string category, string oldMonumentID)
{
  Puts($"Animal '{animal.net.ID.Value}'({animal.GetType()}) entered to '{monumentID}'({category}). Previous monument was '{oldMonumentID}'.");
}
```  

### OnEntityEnteredMonument  
Called when any other **BaseEntity enters** any monument.  
No return behaviour.  

```csharp
void OnEntityEnteredMonument(string monumentID, BaseEntity entity, string category, string oldMonumentID)
{
  Puts($"Entity '{entity.net.ID.Value}'({entity.GetType()}) entered to '{monumentID}'({category}). Previous monument was '{oldMonumentID}'.");
}
```  

### OnPlayerExitedMonument  
Called when a **player exits** any monument.  
No return behaviour.  

```csharp
void OnPlayerExitedMonument(string monumentID, BasePlayer player, string category, string reason, string newMonumentID)
{
  Puts($"Player '{player.displayName}' left from '{monumentID}'({category}). Reason: '{reason}'. New monument is: '{newMonumentID}'.");
}
```  

### OnNpcExitedMonument  
Called when an **NPC player exits** any monument.  
No return behaviour.  

```csharp
void OnNpcExitedMonument(string monumentID, BaseNPC2 npcPlayer, string category, string reason, string newMonumentID)
{
  Puts($"Npc '{npcPlayer.displayName}'({npcPlayer.GetType()}) left from '{monumentID}'({category}). Reason: '{reason}'. New monument is: '{newMonumentID}'.");
}

void OnNpcExitedMonument(string monumentID, BasePlayer npcPlayer, string category, string reason, string newMonumentID)
{
  Puts($"Npc '{npcPlayer.displayName}'({npcPlayer.GetType()}) left from '{monumentID}'({category}). Reason: '{reason}'. New monument is: '{newMonumentID}'.");
}
```  

### OnAnimalExitedMonument  
Called when an **Animal exits** any monument.  
No return behaviour.  

```csharp
void OnAnimalExitedMonument(string monumentID, BaseNPC2 animal, string category, string reason, string newMonumentID)
{
  Puts($"Animal '{animal.displayName}'({animal.GetType()}) left from '{monumentID}'({category}). Reason: '{reason}'. New monument is: '{newMonumentID}'.");
}

void OnAnimalExitedMonument(string monumentID, BaseAnimalNPC animal, string category, string reason, string newMonumentID)
{
  Puts($"Animal '{animal.net.ID.Value}'({animal.GetType()}) left from '{monumentID}'({category}). Reason: '{reason}'. New monument is: '{newMonumentID}'.");
}
```  

### OnEntityExitedMonument  
Called when any other **BaseEntity exits** any monument.  
No return behaviour.  

```csharp
void OnEntityExitedMonument(string monumentID, BaseEntity entity, string category, string reason, string newMonumentID)
{
  Puts($"Entity '{entity.net.ID.Value}'({entity.GetType()}) left from '{monumentID}'({category}). Reason: '{reason}'. New monument is: '{newMonumentID}'.");
}
```  

## Developer API  

```csharp
[PluginReference]
private Plugin MonumentsWatcher;
```  

**There are 15 categories of monuments:**  
- **SafeZone**(0):  
  - **Bandit Camp**, **Outpost**, **Floating City**, **Fishing Village**, **Ranch** and **Large Barn**.  
- **RadTown**(1):  
  - **Airfield**, **Arctic Research Base**, **Abandoned Military Base**, **Giant Excavator Pit**, **Ferry Terminal**, **Harbor**, **Junkyard**, **Launch Site**;  
  - **Military Tunnel**, **Missile Silo**, **Power Plant**, **Sewer Branch**, **Satellite Dish**, **The Dome**, **Toxic Village**(Legacy Radtown), **Train Yard** and **Water Treatment Plant**.  
- **RadTownWater**(2):  
  - **Oil Rigs**, **Underwater Labs**, **Cargo Ships** and **Ghost Ships**.  
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
- **Ruins**(11):  
  - **Jungle Ruins** and **Tropical Ruins**.  
- **WaterWell**(12)  
- **DeepSeaIsland**(13)  
- **Custom**(14)  

**There are 42 api methods:**  
- _General:_
  - **IsReady**  
  - **GetAllMonuments**  
  - **GetAllMonumentsNoAlloc**  
  - **GetAllMonumentsWithCategories**  
  - **GetAllMonumentsWithCategoriesNoAlloc**  
  - **GetMonumentsByCategory**  
  - **GetMonumentsByCategoryNoAlloc**  
  - **GetMonumentCategory**  
  - **GetMonumentDisplayName**  
  - **GetMonumentDisplayNameByLang**  
  - **GetMonumentPosition**  
  - **GetMonumentByPos**  
  - **GetMonumentsByPos**  
  - **GetMonumentsByPosNoAlloc**  
  - **GetClosestMonument**  
  - **IsPosInMonument**  
  - **ShowBounds**  
- _Players:_  
  - **GetMonumentPlayers**  
  - **GetMonumentPlayersNoAlloc**  
  - **GetPlayerMonument**  
  - **GetPlayerMonuments**  
  - **GetPlayeronumentsNoAlloc**  
  - **GetPlayerClosestMonument**  
  - **IsPlayerInMonument**  
- _NPCs:_  
  - **GetMonumentNpcs**  
  - **GetMonumentNpcsNoAlloc**  
  - **GetNpcMonument**  
  - **GetNpcMonuments**  
  - **GetNpcMonumentsNoAlloc**  
  - **IsNpcInMonument**  
- _Animals:_  
  - **GetMonumentAnimals**  
  - **GetMonumentAnimalsNoAlloc**  
  - **GetAnimalMonument**  
  - **GetAnimalMonuments**  
  - **GetAnimalMonumentsNoAlloc**  
  - **IsAnimalInMonument**  
- _Entities:_  
  - **GetMonumentEntities**  
  - **GetMonumentEntitiesNoAlloc**  
  - **GetEntityMonument**  
  - **GetEntityMonuments**  
  - **GetEntityMonumentsNoAlloc**  
  - **IsEntityInMonument**  

### IsReady  
Used to check if the **MonumentsWatcher** plugin is **loaded** and **ready** to work.
Returns **true** if plugin is ready, otherwise **null**.

```csharp
(bool)(MonumentsWatcher?.Call("IsReady") ?? false);
```  

### GetAllMonuments  
Used to retrieve an array of IDs for all available monuments.  

```csharp
(string[])(MonumentsWatcher?.Call("GetAllMonuments") ?? Array.Empty<string>());
```  

### GetAllMonumentsNoAlloc  
Used to fill your existing list with monument IDs.  
Returns **true** if at least one monument is added, otherwise **null**.  
To call the **GetAllMonumentsNoAlloc** method, you need to pass 1 parameter:  
1. **list** as **List\<string>**.  

```csharp
(bool)(MonumentsWatcher?.Call("GetAllMonumentsNoAlloc", yourList) ?? false);
MonumentsWatcher?.Call("GetAllMonumentsNoAlloc", yourList);
```  

### GetAllMonumentsWithCategories  
Used to retrieve a dictionary of IDs and categories for all available monuments.  

 ```csharp
(Dictionary<string, string>)(MonumentsWatcher?.Call("GetAllMonumentsWithCategories") ?? new Dictionary<string, string>());
```  

### GetAllMonumentsWithCategoriesNoAlloc  
Used to fill your existing dictionary with monument IDs(key) and their category(value).  
Returns **true** if at least one monument is added, otherwise **null**.  
To call the **GetAllMonumentsWithCategoriesNoAlloc** method, you need to pass 1 parameter:  
1. **dictionary** as **Dictionary\<string, string>**.  

```csharp
(bool)(MonumentsWatcher?.Call("GetAllMonumentsWithCategoriesNoAlloc", yourDictionary) ?? false);
MonumentsWatcher?.Call("GetAllMonumentsWithCategoriesNoAlloc", yourDictionary);
```  

### GetMonumentsByCategory  
Used to retrieve all available monuments by category.  
To call the **GetMonumentsByCategory** method, you need to pass 1 parameter:  
1. **monument category** as a **string**.  

```csharp
(string[])(MonumentsWatcher?.Call("GetMonumentsByCategory", "SafeZone") ?? Array.Empty<string>());
```  

### GetMonumentsByCategoryNoAlloc  
Used to fill your existing list with monument IDs by specified category.  
Returns **true** if at least one monument is added, otherwise **null**.  
To call the **GetMonumentsByCategoryNoAlloc** method, you need to pass 2 parameters:  
1. **list** as **List\<string>**;  
2. **monument category** as a **string**.  

```csharp
(bool)(MonumentsWatcher?.Call("GetMonumentsByCategoryNoAlloc", yourList, "SafeZone") ?? false);
MonumentsWatcher?.Call("GetMonumentsByCategoryNoAlloc", yourList, "SafeZone");
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
2. **Player**, available options:  
  **userID** as a **ulong** or a **string**(recommended);  
  **player** as a **BasePlayer** or an **IPlayer**.  
3. **displaySuffix** as a **bool**. Should the suffix be displayed in the name if there are multiple such monuments? This parameter is **optional**.  

```csharp
(string)(MonumentsWatcher?.Call("GetMonumentDisplayName", monumentID, player.userID, true) ?? string.Empty);//(ulong)userID
(string)(MonumentsWatcher?.Call("GetMonumentDisplayName", monumentID, player, true) ?? string.Empty);//(BasePlayer/IPlayer)player
(string)(MonumentsWatcher?.Call("GetMonumentDisplayName", monumentID, player.UserIDString, true) ?? string.Empty);//(string)userID
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

### GetMonumentsByPosNoAlloc  
Used to fill your existing list with monument IDs by specified position.  
Returns **true** if at least one monument is added, otherwise **null**.  
To call the **GetMonumentsByPosNoAlloc** method, you need to pass 2 parameters:  
1. **list** as **List\<string>**;  
2. **position** as a **Vector3**.  

```csharp
(bool)(MonumentsWatcher?.Call("GetMonumentsByPosNoAlloc", yourList, pos) ?? false);
MonumentsWatcher?.Call("GetMonumentsByPosNoAlloc", yourList, pos);
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

### GetMonumentPlayersNoAlloc  
Used to fill your existing list with players located in the specified monument.  
Returns **true** if at least one player is added, otherwise **null**.  
To call the **GetMonumentPlayersNoAlloc** method, you need to pass 2 parameters:  
1. **list** as **List\<BasePlayer>**;  
2. **monumentID** as a **string**.  

```csharp
(bool)(MonumentsWatcher?.Call("GetMonumentPlayersNoAlloc", yourList, monumentID) ?? false);
MonumentsWatcher?.Call("GetMonumentPlayersNoAlloc", yourList, monumentID);
```  

### GetPlayerMonument  
Used to retrieve the monument in which the specified player is located.  
Returns an **empty string** on failure.  
To call the **GetPlayerMonument** method, you need to pass 1 parameter:  
1. **Player**, available options:  
  **player** as a **BasePlayer**;  
  **userID** as a **ulong**(recommended) or a **string**.  

```csharp
(string)(MonumentsWatcher?.Call("GetPlayerMonument", player.UserIDString) ?? string.Empty);//(string)userID
(string)(MonumentsWatcher?.Call("GetPlayerMonument", player) ?? string.Empty);//(BasePlayer)player
(string)(MonumentsWatcher?.Call("GetPlayerMonument", player.userID) ?? string.Empty);//(ulong)userID
```  

### GetPlayerMonuments  
Used to retrieve all monuments in which the specified player is located.  
Returns **null** on failure.  
To call the **GetPlayerMonuments** method, you need to pass 1 parameter:  
1. **Player**, available options:  
  **player** as a **BasePlayer**;  
  **userID** as a **ulong**(recommended) or a **string**.  

```csharp
(string[])(MonumentsWatcher?.Call("GetPlayerMonuments", player.UserIDString) ?? Array.Empty<string>());//(string)userID
(string[])(MonumentsWatcher?.Call("GetPlayerMonuments", player) ?? Array.Empty<string>());//(BasePlayer)player
(string[])(MonumentsWatcher?.Call("GetPlayerMonuments", player.userID) ?? Array.Empty<string>());//(ulong)userID
```  

### GetPlayerMonumentsNoAlloc  
Used to fill your existing list with players located in the specified monument.  
Returns **true** if at least one player is added, otherwise **null**.  
To call the **GetPlayerMonumentsNoAlloc** method, you need to pass 2 parameters:  
1. **list** as **List\<string>**;  
2. **Player**, available options:  
  **player** as a **BasePlayer**;  
  **userID** as a **ulong**(recommended) or a **string**.  

```csharp
(bool)(MonumentsWatcher?.Call("GetPlayerMonumentsNoAlloc", yourList, player.userID) ?? false);
MonumentsWatcher?.Call("GetPlayerMonumentsNoAlloc", yourList, player.userID);
```  

### GetPlayerClosestMonument  
Used to retrieve the nearest monument to the specified player.  
Returns an **empty string** on failure.  
To call the **GetPlayerClosestMonument** method, you need to pass 1 parameter:  
1. **Player**, available options:  
  **player** as a **BasePlayer**(recommended);  
  **userID** as a **ulong** or a **string**.  

```csharp
(string)(MonumentsWatcher?.Call("GetPlayerClosestMonument", player.UserIDString) ?? string.Empty);//(string)userID
(string)(MonumentsWatcher?.Call("GetPlayerClosestMonument", player.userID) ?? string.Empty);//(ulong)userID
(string)(MonumentsWatcher?.Call("GetPlayerClosestMonument", player) ?? string.Empty);//(BasePlayer)player
```  

### IsPlayerInMonument  
Used to check whether the specified player is in the specified monument.  
Returns a **false** on failure.  
To call the **IsPlayerInMonument** method, you need to pass 1 parameter:  
1. **monumentID** as a **string**;  
2. **Player**, available options:  
  **player** as a **BasePlayer**;  
  **userID** as a **ulong**(recommended) or a **string**.  

```csharp
(bool)(MonumentsWatcher?.Call("IsPlayerInMonument", monumentID, player.UserIDString) ?? false);//(string)userID
(bool)(MonumentsWatcher?.Call("IsPlayerInMonument", monumentID, player) ?? false);//(BasePlayer)player
(bool)(MonumentsWatcher?.Call("IsPlayerInMonument", monumentID, player.userID) ?? false);//(ulong)userID
```  

### GetMonumentNpcs  
Used to retrieve an array of all npcs located in the specified monument.  
Returns **null** on failure.  
To call the **GetMonumentNpcs** method, you need to pass 1 parameter:  
1. **monumentID** as a **string**.  

```csharp
(BaseNPC2[])(MonumentsWatcher?.Call("GetMonumentNpcs", monumentID) ?? Array.Empty<BaseNPC2>());
(BasePlayer[])(MonumentsWatcher?.Call("GetMonumentNpcs_Old", monumentID) ?? Array.Empty<BasePlayer>());
```  

### GetMonumentNpcsNoAlloc  
Used to fill your existing list with npcs located in the specified monument.  
Returns **true** if at least one npc is added, otherwise **null**.  
To call the **GetMonumentNpcsNoAlloc** method, you need to pass 2 parameters:  
1. **list** as **List\<BaseNPC2>**, **List\<BasePlayer>** or **List\<BaseEntity>**;  
2. **monumentID** as a **string**.  

```csharp
(bool)(MonumentsWatcher?.Call("GetMonumentNpcsNoAlloc", yourList, monumentID) ?? false);
MonumentsWatcher?.Call("GetMonumentNpcsNoAlloc", yourList, monumentID);
```  

### GetNpcMonument  
Used to retrieve the monument in which the specified npc is located.  
Returns an **empty string** on failure.  
To call the **GetNpcMonument** method, you need to pass 1 parameter:  
1. **Npc**, available options:  
  **npcPlayer** as a **BaseNPC2** or **BasePlayer**;  
  **netID** as a **NetworkableId**;  
  **netID** as a **ulong**(recommended).  

```csharp
(string)(MonumentsWatcher?.Call("GetNpcMonument", npcPlayer) ?? string.Empty);//(BaseNPC2 or BasePlayer)npcPlayer
(string)(MonumentsWatcher?.Call("GetNpcMonument", npcPlayer.net.ID) ?? string.Empty);//(NetworkableId)netID
(string)(MonumentsWatcher?.Call("GetNpcMonument", npcPlayer.net.ID.Value) ?? string.Empty);//(ulong)netID
```  

### GetNpcMonuments  
Used to retrieve all monuments in which the specified npc is located.  
Returns **null** on failure.  
To call the **GetNpcMonuments** method, you need to pass 1 parameter:  
1. **Npc**, available options:  
  **npcPlayer** as a **BaseNPC2** or **BasePlayer**;  
  **netID** as a **NetworkableId**;  
  **netID** as a **ulong**(recommended).  

```csharp
(string[])(MonumentsWatcher?.Call("GetNpcMonuments", npcPlayer) ?? Array.Empty<string>());//(BaseNPC2 or BasePlayer)npcPlayer
(string[])(MonumentsWatcher?.Call("GetNpcMonuments", npcPlayer.net.ID) ?? Array.Empty<string>());//(NetworkableId)netID
(string[])(MonumentsWatcher?.Call("GetNpcMonuments", npcPlayer.net.ID.Value) ?? Array.Empty<string>());//(ulong)netID
```  

### GetNpcMonumentsNoAlloc  
Used to fill your existing list with npcs located in the specified monument.  
Returns **true** if at least one npc is added, otherwise **null**.  
To call the **GetNpcMonumentsNoAlloc** method, you need to pass 2 parameters:  
1. **list** as **List\<string>**;  
2. **Npc**, available options:  
  **npcPlayer** as a **BaseNPC2** or **BasePlayer**;  
  **netID** as a **NetworkableId**;  
  **netID** as a **ulong**(recommended).  

```csharp
(bool)(MonumentsWatcher?.Call("GetNpcMonumentsNoAlloc", yourList, npcPlayer.net.ID.Value) ?? false);
MonumentsWatcher?.Call("GetNpcMonumentsNoAlloc", yourList, npcPlayer.net.ID.Value);
```  

### IsNpcInMonument  
Used to check whether the specified npc is in the specified monument.  
Returns a **false** on failure.  
To call the **IsNpcInMonument** method, you need to pass 1 parameter:  
1. **monumentID** as a **string**;  
2. **Npc**, available options:  
  **npcPlayer** as a **BaseNPC2** or **BasePlayer**;  
  **netID** as a **NetworkableId**;  
  **netID** as a **ulong**(recommended).  

```csharp
(bool)(MonumentsWatcher?.Call("IsNpcInMonument", monumentID, npcPlayer) ?? false);//(BaseNPC2)npcPlayer
(bool)(MonumentsWatcher?.Call("IsNpcInMonument", monumentID, npcPlayer.net.ID) ?? false);//(NetworkableId)netID
(bool)(MonumentsWatcher?.Call("IsNpcInMonument", monumentID, npcPlayer.net.ID.Value) ?? false);//(ulong)netID
```  

### GetMonumentAnimals  
Used to retrieve an array of all animals located in the specified monument.  
Returns **null** on failure.  
To call the **GetMonumentAnimals** method, you need to pass 1 parameter:  
1. **monumentID** as a **string**.  

```csharp
(BaseNPC2[])(MonumentsWatcher?.Call("GetMonumentAnimals", monumentID) ?? Array.Empty<BaseNPC2>());
(BaseAnimalNPC[])(MonumentsWatcher?.Call("GetMonumentAnimals_Old", monumentID) ?? Array.Empty<BaseAnimalNPC>());
```  

### GetMonumentAnimalsNoAlloc  
Used to fill your existing list with animals located in the specified monument.  
Returns **true** if at least one animal is added, otherwise **null**.  
To call the **GetMonumentAnimalsNoAlloc** method, you need to pass 2 parameters:  
1. **list** as **List\<BaseNPC2>**, **List\<BaseAnimalNPC>** or **List\<BaseEntity>**;  
2. **monumentID** as a **string**.  

```csharp
(bool)(MonumentsWatcher?.Call("GetMonumentAnimalsNoAlloc", yourList, monumentID) ?? false);
MonumentsWatcher?.Call("GetMonumentAnimalsNoAlloc", yourList, monumentID);
```  

### GetAnimalMonument  
Used to retrieve the monument in which the specified animal is located.  
Returns an **empty string** on failure.  
To call the **GetAnimalMonument** method, you need to pass 1 parameter:  
1. **Animal**, available options:  
  **animal** as a **BaseNPC2** or **BaseAnimalNPC**;  
  **netID** as a **NetworkableId**;  
  **netID** as a **ulong**(recommended).  

```csharp
(string)(MonumentsWatcher?.Call("GetAnimalMonument", animal) ?? string.Empty);//(BaseNPC2 or BaseAnimalNPC)animal
(string)(MonumentsWatcher?.Call("GetAnimalMonument", animal.net.ID) ?? string.Empty);//(NetworkableId)netID
(string)(MonumentsWatcher?.Call("GetAnimalMonument", animal.net.ID.Value) ?? string.Empty);//(ulong)netID
```  

### GetAnimalMonuments  
Used to retrieve all monuments in which the specified animal is located.  
Returns **null** on failure.  
To call the **GetAnimalMonuments** method, you need to pass 1 parameter:  
1. **Animal**, available options:  
  **animal** as a **BaseNPC2** or **BaseAnimalNPC**;  
  **netID** as a **NetworkableId**;  
  **netID** as a **ulong**(recommended).  

```csharp
(string[])(MonumentsWatcher?.Call("GetAnimalMonuments", animal) ?? Array.Empty<string>());//(BaseNPC2 or BaseAnimalNPC)animal
(string[])(MonumentsWatcher?.Call("GetAnimalMonuments", animal.net.ID) ?? Array.Empty<string>());//(NetworkableId)netID
(string[])(MonumentsWatcher?.Call("GetAnimalMonuments", animal.net.ID.Value) ?? Array.Empty<string>());//(ulong)netID
```  

### GetAnimalMonumentsNoAlloc  
Used to fill your existing list with animals located in the specified monument.  
Returns **true** if at least one animal is added, otherwise **null**.  
To call the **GetAnimalMonumentsNoAlloc** method, you need to pass 2 parameters:  
1. **list** as **List\<string>**;  
2. **Animal**, available options:  
  **animal** as a **BaseNPC2** or **BaseAnimalNPC**;  
  **netID** as a **NetworkableId**;  
  **netID** as a **ulong**(recommended).  

```csharp
(bool)(MonumentsWatcher?.Call("GetAnimalMonumentsNoAlloc", yourList, animal.net.ID.Value) ?? false);
MonumentsWatcher?.Call("GetAnimalMonumentsNoAlloc", yourList, animal.net.ID.Value);
```  

### IsAnimalInMonument  
Used to check whether the specified animal is in the specified monument.  
Returns a **false** on failure.  
To call the **IsAnimalInMonument** method, you need to pass 1 parameter:  
1. **monumentID** as a **string**;  
2. **Animal**, available options:  
  **animal** as a **BaseNPC2** or **BaseAnimalNPC**;  
  **netID** as a **NetworkableId**;  
  **netID** as a **ulong**(recommended).  

```csharp
(bool)(MonumentsWatcher?.Call("IsAnimalInMonument", monumentID, animal) ?? false);//(BaseNPC2)animal
(bool)(MonumentsWatcher?.Call("IsAnimalInMonument", monumentID, animal.net.ID) ?? false);//(NetworkableId)netID
(bool)(MonumentsWatcher?.Call("IsAnimalInMonument", monumentID, animal.net.ID.Value) ?? false);//(ulong)netID
```  

### GetMonumentEntities  
Used to retrieve an array of all entities located in the specified monument.  
Returns **null** on failure.  
To call the **GetMonumentEntities** method, you need to pass 1 parameter:  
1. **monumentID** as a **string**.  

```csharp
(BaseEntity[])(MonumentsWatcher?.Call("GetMonumentEntities", monumentID) ?? Array.Empty<BaseEntity>());
```  

### GetMonumentEntitiesNoAlloc  
Used to fill your existing list with entities located in the specified monument.  
Returns **true** if at least one entity is added, otherwise **null**.  
To call the **GetMonumentEntitiesNoAlloc** method, you need to pass 2 parameters:  
1. **list** as **List\<BaseEntity>**;  
2. **monumentID** as a **string**.  

```csharp
(bool)(MonumentsWatcher?.Call("GetMonumentEntitiesNoAlloc", yourList, monumentID) ?? false);
MonumentsWatcher?.Call("GetMonumentEntitiesNoAlloc", yourList, monumentID);
```  

### GetEntityMonument  
Used to retrieve the monument in which the specified entity is located.  
Returns an **empty string** on failure.  
To call the **GetEntityMonument** method, you need to pass 1 parameter:  
1. **Entity**, available options:  
  **entity** as a **BaseEntity**;  
  **netID** as a **NetworkableId**;  
  **netID** as a **ulong**(recommended).  

```csharp
(string)(MonumentsWatcher?.Call("GetEntityMonument", entity) ?? string.Empty);//(BaseEntity)entity
(string)(MonumentsWatcher?.Call("GetEntityMonument", entity.net.ID) ?? string.Empty);//(NetworkableId)netID
(string)(MonumentsWatcher?.Call("GetEntityMonument", entity.net.ID.Value) ?? string.Empty);//(ulong)netID
```  

### GetEntityMonuments  
Used to retrieve all monuments in which the specified entity is located.  
Returns **null** on failure.  
To call the **GetEntityMonuments** method, you need to pass 1 parameter:  
1. **Entity**, available options:  
  **entity** as a **BaseEntity**;  
  **netID** as a **NetworkableId**;  
  **netID** as a **ulong**(recommended).  

```csharp
(string[])(MonumentsWatcher?.Call("GetEntityMonuments", entity) ?? Array.Empty<string>());//(BaseEntity)entity
(string[])(MonumentsWatcher?.Call("GetEntityMonuments", entity.net.ID) ?? Array.Empty<string>());//(NetworkableId)netID
(string[])(MonumentsWatcher?.Call("GetEntityMonuments", entity.net.ID.Value) ?? Array.Empty<string>());//(ulong)netID
```  

### GetEntityMonumentsNoAlloc  
Used to fill your existing list with entities located in the specified monument.  
Returns **true** if at least one entity is added, otherwise **null**.  
To call the **GetEntityMonumentsNoAlloc** method, you need to pass 2 parameters:  
1. **list** as **List\<string>**;  
2. **Entity**, available options:  
  **entity** as a **BaseNPC2** or **BaseEntity**;  
  **netID** as a **NetworkableId**;  
  **netID** as a **ulong**(recommended).  

```csharp
(bool)(MonumentsWatcher?.Call("GetEntityMonumentsNoAlloc", yourList, entity.net.ID.Value) ?? false);
MonumentsWatcher?.Call("GetEntityMonumentsNoAlloc", yourList, entity.net.ID.Value);
```  

### IsEntityInMonument  
Used to check whether the specified entity is in the specified monument.  
Returns a **false** on failure.  
To call the **IsEntityInMonument** method, you need to pass 1 parameter:  
1. **monumentID** as a **string**;  
2. **Entity**, available options:  
  **entity** as a **BaseEntity**;  
  **netID** as a **NetworkableId**;  
  **netID** as a **ulong**(recommended).  

```csharp
(bool)(MonumentsWatcher?.Call("IsEntityInMonument", monumentID, entity) ?? false);//(BaseEntity)entity
(bool)(MonumentsWatcher?.Call("IsEntityInMonument", monumentID, entity.net.ID) ?? false);//(NetworkableId)netID
(bool)(MonumentsWatcher?.Call("IsEntityInMonument", monumentID, entity.net.ID.Value) ?? false);//(ulong)netID
```  