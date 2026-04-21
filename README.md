# MyAesirNeighbourCapstoneTFS
Technical Design Document
Overview
My Aesir Neighbour is a life-simulation game built in Unreal Engine using Blueprints. The player gathers fish through minigames, crafts items, completes quests, and helps grow a Norse-inspired village populated by charming characters.
Naming Conventions
Consistent naming makes Blueprints, assets, and references much easier to navigate, especially as systems scale.
General Rules
Use PascalCase for all asset names (e.g., BP_PlayerCharacter)
Use prefixes to indicate asset type
Be descriptive but concise
Avoid spaces and special characters
Keep names consistent across systems
Blueprint Prefixes
Asset Type
Prefix
Example
Blueprint Actor
BP_
BP_NPC, BP_CraftingStation
Widget Blueprint
WBP_
WBP_Inventory
Actor Component
AC_
AC_InventoryComponent
Interface
BPI_
BPI_Interactable
Struct
ST_
ST_ItemData
Enum
EN_
EN_ItemType
Data Table
DT_
DT_Items, DT_Quests
Function Library
FL_
FL_Utility


Variable Naming
Use camelCase
Boolean variables should start with b
bIsInteractable
bHasQuest
Examples:
currentQuest
inventoryItems
interactionDistance

Function Naming
Use Verb + Noun
AddItem
StartMinigame
CompleteQuest
Event Naming
Prefix with On or Handle
OnQuestCompleted
HandleInteraction
Asset-Specific Naming Examples
Materials: M_WaterSurface
Material Instances: MI_WaterSurface_Deep
Textures: T_Fish_Scales_D
Static Meshes: SM_Boat
Skeletal Meshes: SK_Player
Anim Blueprints: ABP_Player
Folder Structure
A clean folder structure is critical for scalability and team collaboration.
Root Structure
Content
│
├── Core
├── Characters
├── Systems
├── World
├── UI
├── Data
├── Audio
├── Art
└── Dev

Core
Global systems and framework
Core
├── GameMode
├── GameInstance
├── SaveSystem
├── Input

Characters
Characters
├── Player
│   ├── Blueprints
│   ├── Animations
│   └── Meshes
│
├── NPCs
│   ├── Base
│   ├── Villagers
│   └── Mythic

Systems
Organized by feature (very important for Blueprint projects)
Systems/
├── Interaction
├── Inventory
├── Minigames
├── Crafting
├── Quests
├── Dialogue
├── Town
└── Fish
Each system:
Inventory
├── Blueprints
├── Components
├── UI
└── Data

World
World
├── Maps
├── LevelStreaming
├── Environment
├── Buildings
└── Props
UI
UI
├── HUD
├── Menus
├── Widgets
└── Styles

Data
Centralized data-driven design
Data
├── Items
├── Fish
├── Quests
├── Dialogue
└── Recipes

Audio
Audio
├── Music
├── SFX
└── Ambience
Art
Art/
├── Materials
├── Textures
├── VFX
└── Concept

Dev
For testing and prototyping
Dev
├── TestMaps
├── DebugTools
└── Experimental

Core Systems Architecture
Game Framework
Engine: Unreal Engine (Blueprints primarily, optional C++ for optimization)
Game Mode (BP_GameMode)
Handles overall game rules
Initializes player, world state, and progression systems
Game Instance (BP_GameInstance)
Persistent data across levels (inventory, quest progress, town state)
Save System (BP_SaveGame)
Stores:
Player inventory
Quest progress
Built structures
NPC relationship states
Player System
Player Controller (BP_PlayerController)
Handles:
Input (movement, interaction, minigames)
UI triggers
Camera control
Player Character (BP_PlayerCharacter)
Components:
Skeletal Mesh
Camera
Interaction Component
Features:
Movement (walk/run)
Interaction trace (line trace or sphere overlap)
Animation Blueprint integration
Interaction System
Base Interactable (BP_Interactable)
Parent Blueprint for all interactable objects
Variables:
InteractionName
bIsInteractable
Functions:
Interact(Player)
Derived Interactables
NPCs (BP_NPC)
Minigame triggers (BP_MinigameNode)
Crafting stations (BP_CraftingStation)
Resource nodes (fishing spots, etc.)
Minigame System
Minigame Manager (BP_MinigameManager)
Responsible for:
Launching minigames
Tracking results
Reward distribution
Minigame Types
Each minigame is a separate Blueprint:
BP_FishingMinigame
BP_SpearMinigame
BP_StackingMinigame
Flow
Player interacts with node
Minigame loads (UI or level instance)
Player completes challenge
Output:
Score
Fish rarity
Rewards sent to Inventory System
Inventory & Item System
Item Data Structure
Use Data Tables (DT_Items):
Item ID
Name
Type (Fish, Material, Crafted)
Rarity
Icon
Description
\Inventory Component (BP_InventoryComponent)
Attached to Player
Functions:
AddItem(ItemID, Quantity)
RemoveItem(ItemID, Quantity)
HasItem(ItemID)
Fish System
Fish Data
Stored in Data Table (DT_Fish):
Name
Rarity tier
Minigame source
Crafting value
Crafting System
Crafting Recipes (DT_Recipes)
Required Items
Output Item
Crafting Station (BP_CraftingStation)
UI-based interaction
Validates:
Required materials
Calls:
Inventory removal
Item creation
Quest System
Quest Structure (DT_Quests)
Quest ID
Description
Objectives
Rewards
NPC giver
Quest Manager (BP_QuestManager)
Tracks:
Active quests
Completed quests
Updates objectives dynamically
NPC System
NPC Base (BP_NPC)
Variables:
Name
Dialogue Data
Relationship Level
Dialogue System
Simple dialogue trees via Data Tables
Branching choices
Quest integration
Town Building System
Structure System (BP_Building)
Types:
Houses
Shops
Utility/Story structures (e.g hot springs)
Town Manager (BP_TownManager)
Tracks:
Built structures
Town level
Unlocks:
New NPCs
New quests
New minigames
UI System
Widgets
Inventory UI (WBP_Inventory)
Quest Log (WBP_QuestLog)
Dialogue UI (WBP_Dialogue)
Minigame UI (WBP_Minigame)
Map UI (WBP_Map)
UI Manager
Handles switching between gameplay and UI states
Progression System
Player Progression
Metrics:
Completed quests
Town level
Rare fish collected
Unlocks
New areas
New minigames
Higher rarity fish
World Design
Structure
Hub-based village
Surrounding explorable zones:
Shores
Hot Springs
Other hidden realms
Norse Inspiration
Visual themes inspired by:
Thor
Loki
Skadi
Audio System
Ambient Norse-inspired soundtrack
SFX:
Water
Fish capture
Crafting
Performance Considerations
Use Blueprint Interfaces to reduce casting
Use Object Pooling for repeated minigame actors
Optimize tick usage (avoid heavy per-frame logic)
Future Extensions
Multiplayer co-op
Seasonal events
Expanded mythology (other pantheons)
Additional Best Practices
Avoid “God Blueprints”
Don’t put everything into one Blueprint (e.g., Player). Use:
Components
Interfaces
Managers
Use Blueprint Interfaces
Example:
BPI_Interactable
BPI_Minigame
This avoids heavy casting and keeps systems modular.
Data-Driven Design
Use Data Tables for:
Items
Fish
Quests
Recipes
This makes balancing and iteration much faster.
Consistency Over Perfection
A simple, consistently followed structure is far better than a “perfect” one that no one sticks to.

