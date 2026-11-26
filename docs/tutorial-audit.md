# Learning Center Tutorial Audit

Reviewed on **2026-11-26** against Studio web `c4f0594`, backend `79aa382c`, Unity `1ed2ec1` (SDK [0.2.62e](../../ss-unity/Assets/SaiGame/Scripts/SaiServer.cs#L14)) and Sai Play `fe10a40`.

The Studio app registers **54 static articles** across 37 Guides, 14 Lua Guides and 3 Tips. **24 need edits**, **28 had no issue in the claims reviewed**, and **2 are editorial or external guidance**. This review uses the English text as its baseline. All three locales have article files, with localized text spot-checked for key findings. The review covers repository behavior. Screenshots and deployed behavior still need verification where relevant. [Static sections](../lib/tutorial-static-sections.ts), [Guides registry](../lib/tutorials/basic-guides.ts), [Lua registry](../lib/tutorials/lua-guides.ts)

Apply each edit to the linked English, Vietnamese and Japanese files. Keep code identifiers and values synchronized across languages. Refresh any screenshot that still shows the labels or steps being replaced.

## Correct misleading instructions

These edits fix steps, limits, prerequisites or descriptions that can lead readers to the wrong result.

### Create Gamer Progress

[EN](../public/tutorial-guides/create-gamer-progress.en.md) · [VI](../public/tutorial-guides/create-gamer-progress.vi.md) · [JA](../public/tutorial-guides/create-gamer-progress.ja.md)

- **Step 3, Clear Gamer Progress.** Show **Check 2FA** first, then enter an Authenticator code in **2FA Code** when required and click **Clear Progress**. Replace the step screenshot to show the current controls. [Inspector flow](../../ss-unity/Assets/SaiGame/Scripts/Editor/SaiGamerProgressEditor.cs#L120), [server verification](../../ss-go/internal/handler/profile_handler.go#L1250)

### What is Container?

[EN](../public/tutorial-guides/what-is-container.en.md) · [VI](../public/tutorial-guides/what-is-container.vi.md) · [JA](../public/tutorial-guides/what-is-container.ja.md)

- **The Main Inventory.** Replace the first-item trigger with Gamer Progress creation, which attempts to provision the main inventory. Keep mail claiming as a way to add an item. [Profile provisioning](../../ss-go/internal/usecase/profile_usecase.go#L263)
- **Understanding Containers.** List `inventory`, `chest`, `bag`, `vault`, `shulker_box` and `equipment`, and explain that container definitions count toward the shared Items quota. [Container types](../../ss-go/internal/domain/inventory_container_definition.go#L10), [Items usage calculation](../../ss-go/internal/handler/item_definition_handler.go#L33)

### Reposition Item in Container

[EN](../public/tutorial-guides/reposition-item-in-container.en.md) · [VI](../public/tutorial-guides/reposition-item-in-container.vi.md) · [JA](../public/tutorial-guides/reposition-item-in-container.ja.md)

- **Step 4, Moving Items via Unity Inspector.** Use the `SaiServer > Item` hierarchy and replace **Sync Item** with **Sync Items** for the item list and **Sync Containers** for the destination list. Show which control to use if either list is empty. [Prefab](../../ss-unity/Assets/SaiGame/Prefabs/SaiServer.prefab), [Inspector sync controls](../../ss-unity/Assets/SaiGame/Scripts/3_ItemContainer/Item/Editor/ItemMoveEditor.cs#L185)

### Creating Custom Containers

[EN](../public/tutorial-guides/creating-custom-containers.en.md) · [VI](../public/tutorial-guides/creating-custom-containers.vi.md) · [JA](../public/tutorial-guides/creating-custom-containers.ja.md)

- **Steps 1–2, item and grid setup.** Replace **Item Type** with **Category**, select `container`, then set the container definition's type to `chest` and link the Chest item definition. [Item categories](../../ss-go/internal/domain/inventory_item_definition.go#L14), [container types](../../ss-go/internal/domain/inventory_container_definition.go#L14)
- **Step 4, Initializing Containers in Unity.** Replace `SaiService` with `SaiServer` in the hierarchy. Keep **Get Containers** as the action to refresh the player's container list. [Prefab](../../ss-unity/Assets/SaiGame/Prefabs/SaiServer.prefab), [PlayerContainer Inspector](../../ss-unity/Assets/SaiGame/Scripts/3_ItemContainer/Container/Editor/PlayerContainerEditor.cs#L108)

### Add item to Shop

[EN](../public/tutorial-guides/add-item-to-shop.en.md) · [VI](../public/tutorial-guides/add-item-to-shop.vi.md) · [JA](../public/tutorial-guides/add-item-to-shop.ja.md)

- **Purchase Modes and Scheduling.** Rewrite the Per Player and Global bullets. **Restock Schedule** resets the purchase-count window for either mode at the selected UTC boundary. `none` counts all time. **Stock** is checked using all-time sales and can still block a purchase after the limit window resets. Include an example with a daily cap and finite stock. [Schedule definitions](../../ss-go/internal/domain/shop.go#L103), [separate stock and limit checks](../../ss-go/internal/services/implementations/shop_service_local.go#L346)
- **Item Basics & Display.** Show how an item inherits the shop currency or specifies an item or sGem override. Include localized display names and descriptions. [Shop item fields](../../ss-go/internal/domain/shop.go#L216), [currency resolution](../../ss-go/internal/domain/shop.go#L257)

### Create a Daily Quest Pool

[EN](../public/tutorial-guides/create-daily-quest-pool.en.md) · [VI](../public/tutorial-guides/create-daily-quest-pool.vi.md) · [JA](../public/tutorial-guides/create-daily-quest-pool.ja.md)

- **Intro and strategy setup.** State that Studio lets users select **Weighted Random** and **Weekly Schedule**. Label **Fixed Rotation** and **Monthly Schedule** as Coming Soon in Studio. The backend has assignment branches for both. [Strategy options](../app/games/[id]/quests/DailyTab.tsx#L274), [disabled menu options](../app/games/[id]/quests/DailyTab.tsx#L1061), [backend assignment](../../ss-go/internal/services/implementations/daily_quest_usecase.go#L356)
- **Weekly Schedule.** Fix the Sunday example. After filtering the configured quests for Sunday, the backend takes the first two entries when Slots Per Day is two. Reserve weighted selection examples for Weighted Random. [Weekly selection and cap](../../ss-go/internal/services/implementations/daily_quest_usecase.go#L356)

### Leaderboard

[EN](../public/tutorial-guides/15a-leaderboard.en.md) · [VI](../public/tutorial-guides/15a-leaderboard.vi.md) · [JA](../public/tutorial-guides/15a-leaderboard.ja.md)

- **Opening prerequisite.** Say the game needs a leaderboard-enabled plugin. List Rare, Epic, Legendary and the admin-granted Leaderboard plugin. Update the prerequisite in Leaderboard for Player at the same time. [Eligible plugin IDs](../../ss-go/internal/domain/leaderboard.go#L155)

### Leaderboard for Player

[EN](../public/tutorial-guides/leaderboard-for-player.en.md) · [VI](../public/tutorial-guides/leaderboard-for-player.vi.md) · [JA](../public/tutorial-guides/leaderboard-for-player.ja.md)

- **Before you start.** Replace the Rare-only prerequisite with a leaderboard-enabled plugin and a link to the Leaderboard overview. Keep the API default of 100 and max of 500 in the Top N section. [Eligible plugin IDs](../../ss-go/internal/domain/leaderboard.go#L155), [ranking request limit](../../ss-go/internal/handler/leaderboard_handler.go#L92)

### Execute Script

[EN](../public/tutorial-lua/execute-script.en.md) · [VI](../public/tutorial-lua/execute-script.vi.md) · [JA](../public/tutorial-lua/execute-script.ja.md)

- **Battle Start and Battle Status.** Remove the hard-coded `#1` and `#5` template references. Tell readers to choose `battle_start` and `battle_status` by name from the turn-based samples. Add a short resume step using `battle_current_session` and link to the Battle Sessions API entry. [Template list](../../ss-go/internal/handler/script/samples_turnbase.go#L17), [status sample](../../ss-go/internal/handler/script/samples_turnbase.go#L508)

### Overview

[EN](../public/tutorial-lua/overview.en.md) · [VI](../public/tutorial-lua/overview.vi.md) · [JA](../public/tutorial-lua/overview.ja.md)

- **Limits.** Replace 32 KB with **250 KiB (256,000 bytes)** and replace the blanket 200-script entry with **7 scripts per game by default**, increased by plugins. [Body limit](../../ss-go/internal/domain/script.go#L77), [default quota](../../ss-go/internal/config/resource_limits.go#L35), [quota enforcement](../../ss-go/internal/usecase/script_usecase.go#L120)
- **Global Variables and shared code.** Add numeric `ctx.script_version` to the context table. Add a minimal library and main script example with `include LibraryName`. Explain why the referenced library must be active. [Context values](../../ss-go/internal/services/implementations/lua_engine.go#L169), [include resolution](../../ss-go/internal/usecase/script_usecase.go#L448)

## Add missing coverage

### Create a Studio

[EN](../public/tutorial-guides/create-a-studio.en.md) · [VI](../public/tutorial-guides/create-a-studio.vi.md) · [JA](../public/tutorial-guides/create-a-studio.ja.md)

- **Before you start and Troubleshooting.** Add account activation when the server requires referral codes. Keep email verification and 2FA as prerequisites for the Studio dashboard flow. [Create Studio use case](../../ss-go/internal/usecase/studio_usecase.go#L88), [dashboard Create button](../app/studios/page.tsx#L166)
- **Cost table and FAQ.** Say creation is free when the owner has no non-deleted studios and costs 50 sCoin otherwise. Inactive studios still count. [Fee check](../../ss-go/internal/usecase/studio_usecase.go#L105), [ownership count](../../ss-go/internal/repository/studio_repository.go#L173)

### Import Unity Package

[EN](../public/tutorial-guides/import-unity-package.en.md) · [VI](../public/tutorial-guides/import-unity-package.vi.md) · [JA](../public/tutorial-guides/import-unity-package.ja.md)

- **Step 3, `.env` example and toggle list.** Add `SERVER_ENDPOINT` as an optional Editor-only setting and **Override server endpoint** as the switch that applies it in Play Mode. Keep `.env.build` instructions focused on Game ID. Update the environment Inspector image if it omits the endpoint toggle. [Environment controls](../../ss-unity/Assets/SaiGame/Scripts/Editor/SaiServerEditor.cs#L198)

### What is Item Definition?

[EN](../public/tutorial-guides/what-is-item-definition.en.md) · [VI](../public/tutorial-guides/what-is-item-definition.vi.md) · [JA](../public/tutorial-guides/what-is-item-definition.ja.md)

- **Key Attributes & Logic.** Add Stackable, Max Stack Size, Max Owned Quantity and Base Stats. Explain Client Writable for SDK quantity changes and show where to enable it. [Studio item form](../components/CreateItemDefinitionDialog.tsx#L581), [item model](../../ss-go/internal/domain/inventory_item_definition.go), [Unity quantity changes](../../ss-unity/Assets/SaiGame/Scripts/3_ItemContainer/Item/ItemAddDeduct.cs)
- **Category vs. Rarity.** Use the category values returned to the Studio form. List all eight rarities: `common`, `uncommon`, `rare`, `epic`, `legendary`, `set_item`, `mythic` and `Unique`. Keep the explicit casing of `Unique`. [Category list](../../ss-go/internal/domain/inventory_item_definition.go#L54), [rarity list](../../ss-go/internal/domain/inventory_item_definition.go#L116), [Studio dropdown](../components/CreateItemDefinitionDialog.tsx#L511)

### What is Gacha Pack?

[EN](../public/tutorial-guides/what-is-gacha-pack.en.md) · [VI](../public/tutorial-guides/what-is-gacha-pack.vi.md) · [JA](../public/tutorial-guides/what-is-gacha-pack.ja.md)

- **Core Components, Item Pool.** Describe one primary pool plus up to six additional drop groups, for seven groups total. Explain that the opener rolls one reward from the primary pool and independently rolls a reward from each additional group. Use a small example with a primary pool and one additional group. [Group limit](../../ss-go/internal/usecase/gacha_usecase.go#L216), [rolls per group](../../ss-go/internal/usecase/gacha_usecase.go#L254)
- **Key Requirements and Implementation Constraints.** Add the quantity consumed per key on each open, the pack's enabled setting, and the shared Items quota. [Pack and key fields](../../ss-go/internal/domain/gacha.go#L30), [Items usage](../../ss-go/internal/usecase/gacha_usecase.go#L517)

### Craft an item

[EN](../public/tutorial-guides/craft-an-item.en.md) · [VI](../public/tutorial-guides/craft-an-item.vi.md) · [JA](../public/tutorial-guides/craft-an-item.ja.md)

- **Steps 2–3, Unity Inspector.** Under **Fetch Recipe By Key**, enter the recipe key and click **Get**. Explain how **Random UUID** creates the idempotency key and that a retry of the same craft should reuse the original key. Add **Get History** to show the player's craft transactions. [Inspector controls](../../ss-unity/Assets/SaiGame/Scripts/3_ItemContainer/Crafting/Editor/ItemCraftingEditor.cs#L103)

### Group by Preset

[EN](../public/tutorial-guides/group-by-preset.en.md) · [VI](../public/tutorial-guides/group-by-preset.vi.md) · [JA](../public/tutorial-guides/group-by-preset.ja.md)

- **Limits.** Keep 500 definitions per game and add 500 active presets per player and 70 slots per definition or preset. [Preset limits](../../ss-go/internal/domain/preset.go#L22)
- **Unity steps.** Replace **Sync Player Inventory** with **Sync with PlayerItem** and add the **Update Metadata** action in the preset details. [Sync control](../../ss-unity/Assets/SaiGame/Scripts/3_ItemContainer/Preset/Editor/ItemPresetEditor.cs#L175), [metadata control](../../ss-unity/Assets/SaiGame/Scripts/3_ItemContainer/Preset/Editor/ItemPresetEditor.cs#L541)

### Create a Shop

[EN](../public/tutorial-guides/create-a-shop.en.md) · [VI](../public/tutorial-guides/create-a-shop.vi.md) · [JA](../public/tutorial-guides/create-a-shop.ja.md)

- **Usage & Shop Types.** State that games start with two shop slots and plugins can increase that quota. [Default game limits](../../ss-go/internal/config/resource_limits.go#L29)
- **Default Currency Logic and Maintenance.** Show item and sGem currency, the Mailbox and Inventory delivery choices, **Show in Sai Play**, translated names and descriptions, and where to open the activity log. [Shop fields](../../ss-go/internal/domain/shop.go#L154), [shop activity](../../ss-go/internal/domain/shop_activity.go)

### Buy an item

[EN](../public/tutorial-guides/buy-an-item.en.md) · [VI](../public/tutorial-guides/buy-an-item.vi.md) · [JA](../public/tutorial-guides/buy-an-item.ja.md)

- **Preparation and Performing a Purchase.** Distinguish inventory item currency from sGem. Check the player's sGem balance through `Shop.GetSGemWallet` for sGem purchases. In the Inspector, show **Random Key** as a button and **Purchase** as the purchase action. Reuse the same key to retry the same purchase. [Wallet method](../../ss-unity/Assets/SaiGame/Scripts/4_Shop/Shop.cs#L490), [purchase controls](../../ss-unity/Assets/SaiGame/Scripts/4_Shop/Editor/ShopEditor.cs#L305)

### Create Quest Definitions

[EN](../public/tutorial-guides/create-quest-definitions.en.md) · [VI](../public/tutorial-guides/create-quest-definitions.vi.md) · [JA](../public/tutorial-guides/create-quest-definitions.ja.md)

- **Quest Life-Cycle Types.** Add `session` quests and their shared UTC window, with a reference to Session Pools and Battle Pass. In the `one_time` entry, add Expiration in minutes and state the default quota of 30 quests per game near the creation steps. [Quest types](../../ss-go/internal/domain/quest.go#L25), [expiration settings](../../ss-go/internal/services/implementations/quest_type_config.go#L35), [default quota](../../ss-go/internal/config/resource_limits.go#L30)

### Complete a Daily Quest

[EN](../public/tutorial-guides/complete-daily-quest.en.md) · [VI](../public/tutorial-guides/complete-daily-quest.vi.md) · [JA](../public/tutorial-guides/complete-daily-quest.ja.md)

- **Assigning Quests and Player Perspective.** Start with **Load Pools**, select the pool, then show today's assignments and the streak shown on the pool response. Add **Assign Ahead** with its Days Ahead field, and a separate **DailyTimeframe** example for reading assignments by date. [Load Pools](../../ss-unity/Assets/SaiGame/Scripts/5_Quest/Daily/Editor/DailyQuestEditor.cs#L253), [Assign Ahead](../../ss-unity/Assets/SaiGame/Scripts/5_Quest/Daily/Editor/DailyQuestEditor.cs#L155), [streak display](../../ss-unity/Assets/SaiGame/Scripts/5_Quest/Daily/Editor/DailyQuestEditor.cs#L444), [timeframe component](../../ss-unity/Assets/SaiGame/Scripts/5_Quest/Daily/DailyTimeframe.cs)

### Hello World

[EN](../public/tutorial-lua/hello-world.en.md) · [VI](../public/tutorial-lua/hello-world.vi.md) · [JA](../public/tutorial-lua/hello-world.ja.md)

- **Before you start and Step 4, Unity.** Add a link to Create Gamer Progress and ask readers to create a player record before running the sample from Unity. The web editor instructions already cover creating a profile there. Use 250 KiB for the script-body limit throughout to match the server constant. [Player context lookup](../../ss-go/internal/usecase/script_usecase.go#L377), [body limit](../../ss-go/internal/domain/script.go#L77)

### Inventory

[EN](../public/tutorial-lua/inventory.en.md) · [VI](../public/tutorial-lua/inventory.vi.md) · [JA](../public/tutorial-lua/inventory.ja.md)

- **Item definition lookup.** Add `game.get_item_defs_by_ids(ids)` and `game.get_item_defs_by_codes(codes)` after the singular lookups. Include sample arrays, `(results, err)` handling, and the fact that malformed UUIDs or empty codes are skipped by the Lua bindings. [Batch lookup bindings](../../ss-go/internal/services/implementations/lua_engine_lookup_api.go#L41)

### Gacha

[EN](../public/tutorial-lua/gacha.en.md) · [VI](../public/tutorial-lua/gacha.vi.md) · [JA](../public/tutorial-lua/gacha.ja.md)

- **Opening packs.** Add `game.open_gacha_pack_by_code_name(code_name [, container_id [, idempotency_key]])`. Add the separate server-authorized reward variants `game.open_reward_gacha_pack(pack_id [, idempotency_key])` and `game.open_reward_gacha_pack_by_code_name(code_name [, idempotency_key])`, which skip key consumption. Show the `(result, err)` pattern for both families. [Lua gacha bindings](../../ss-go/internal/services/implementations/lua_engine_lookup_api.go#L334), [reward callback contract](../../ss-go/internal/domain/script.go#L351)

### Battle Sessions

[EN](../public/tutorial-lua/battle-sessions.en.md) · [VI](../public/tutorial-lua/battle-sessions.vi.md) · [JA](../public/tutorial-lua/battle-sessions.ja.md)

- **Before the session read example.** Add `local session_id, err = game.battle_session_current_id()` to explain how to look up the current player's active session. Show checking the error and passing a successful result to `battle_session_get`. [Current session binding](../../ss-go/internal/services/implementations/lua_engine_lookup_api.go#L198), [resume template](../../ss-go/internal/handler/script/samples_turnbase.go#L17)

## Articles without identified edits

### Guides

| Tutorial | Checked content |
| :--- | :--- |
| [Unity Google Login](../public/tutorial-guides/unity-google-login.en.md) | Covers browser sign-in and 2FA, session polling, passing tokens to `SaiAuth` and loading Gamer Progress afterwards. [Unity component](../../ss-unity/Assets/SaiGame/Scripts/0_Auth/Google/GoogleBackendLogin.cs#L57), [Google auth use case](../../ss-go/internal/usecase/client_google_auth.go#L257) |
| [Cross platform save](../public/tutorial-guides/cross-platform-save.en.md) | The guide now covers the default 2.5 MiB Game Data limit, `413 GAME_DATA_TOO_LARGE`, delta updates and whole-JSON replacement. [Default size](../../ss-go/internal/config/game_data.go#L10), [update errors](../../ss-go/internal/handler/profile_handler.go#L1084) |
| [Send an item to a player](../public/tutorial-guides/5b-send-an-item-to-a-player.en.md) | The guide now uses `SaiServer` and covers Load Messages, Claim All, Unread Count and Unclaimed Count. [Mailbox Inspector](../../ss-unity/Assets/SaiGame/Scripts/2_Mailbox/Editor/MailboxEditor.cs#L127), [ClaimAllMessages](../../ss-unity/Assets/SaiGame/Scripts/2_Mailbox/Mailbox.cs#L438) |
| [Item Split and Merge](../public/tutorial-guides/item-split-and-merge.en.md) | Split/merge through ItemMove; empty-slot and stack rules are correct. |
| [Item Swap](../public/tutorial-guides/item-swap.en.md) | Swapping within or across containers and the collision rules are correct. |
| [Open Gacha Pack](../public/tutorial-guides/open-gacha-pack.en.md) | Open by ID / Open by Code with `container_id`; all keys must be in the same container. |
| [Gift Codes](../public/tutorial-guides/gift-codes.en.md) | Covers linked reward packs, usage and activation limits, one redemption per player, and Unity redemption. [Redeem flow](../../ss-go/internal/usecase/game_gift_code_usecase.go#L104), [Unity component](../../ss-unity/Assets/SaiGame/Scripts/3_ItemContainer/GiftCode/GiftCodeRedeemer.cs#L24) |
| [What is Item Generator?](../public/tutorial-guides/what-is-item-generator.en.md) | Covers independent per-item **Drop Rate**, tick cap, output pool and **Collect Cap** for direct-inventory delivery. See [implementation notes](#implementation-notes) for Initial Output. [Generator use case](../../ss-go/internal/usecase/generator_usecase.go) |
| [Claim Resources from Generator](../public/tutorial-guides/claim-resources-from-generator.en.md) | Reward destination, testing with a 3-second interval, and the `ItemGenerator` class. |
| [Equipment Slots Definitions](../public/tutorial-guides/equipment-slots-definitions.en.md) | Slots count toward the Items quota; category/item restrictions; Grid View is display only. |
| [Player's Equipments](../public/tutorial-guides/player-equipments.en.md) | Get Slots / Get Equipped / Sync with Player Item / Unequip. |
| [Creating a craft recipe](../public/tutorial-guides/creating-a-craft-recipe.en.md) | Covers recipe limits, the availability window, when Burn-on inputs are deducted and when Bonus rewards roll. See [implementation notes](#implementation-notes) for Burn-off inputs. [Crafting service](../../ss-go/internal/services/implementations/local_crafting_service.go#L130), [recipe limits](../../ss-go/internal/domain/crafting.go) |
| [Group by Tag](../public/tutorial-guides/group-by-tag.en.md) | 50 tags per game, 20 tags per item, no quota cost ([item_tag.go](../../ss-go/internal/domain/item_tag.go)). |
| [Quest Reward Delivery](../public/tutorial-guides/quest-reward-delivery.en.md) | Mailbox by default, Direct delivery in Settings, per-quest override. |
| [Create a Chain Quest](../public/tutorial-guides/create-chain-quest.en.md) | Story Graph, prerequisite links, branching, List View. |
| [Complete a chain quest](../public/tutorial-guides/complete-a-chain-quest.en.md) | Quest Tree / Quest Flat with Start / Check / Claim; QuestHistory. |
| [Leaderboard Admin Page](../public/tutorial-guides/leaderboard-admin-page.en.md) | Raw/rank season data, season creation, archives. |
| [Event Type](../public/tutorial-guides/event-type.en.md) | `join_game` / `ending1`, PlayerEvent (Track Event, session id), Journey tab. |
| [Journey and Node](../public/tutorial-guides/journey-and-node.en.md) | Default Main Story journey, nodes, links, session and time-range filters. |

### Lua Guides

| Tutorial | Checked content |
| :--- | :--- |
| [Enemy Definition](../public/tutorial-lua/enemy-definition.en.md) | 10 entities by default, stats, abilities, Drop Pack IDs, the sample-script stats (hp/attack/defense/speed). |
| [Entity Pool](../public/tutorial-lua/entity-pool.en.md) | 1000 pools, 200 entries per pool, weights, gacha integration ([entity_pool.go](../../ss-go/internal/domain/entity_pool.go)). |
| [Characters Preset](../public/tutorial-lua/3a-characters-preset.en.md) | Character category, required attack/defense/hp stats, Game Presets. |
| [Quests](../public/tutorial-lua/quests.en.md) | `get_quest_def_by_id` |
| [Event Type](../public/tutorial-lua/events.en.md) | `get_event_type_by_id/by_name` |
| [Entities](../public/tutorial-lua/entities.en.md) | All 7 entity/pool functions. |
| [Presets](../public/tutorial-lua/6-presets.en.md) | All 3 preset functions. |
| [Equipment](../public/tutorial-lua/equipment.en.md) | `get_equipped_in_slot` |

### Tips

| Tutorial | Checked content |
| :--- | :--- |
| [Game Expect User](../public/tutorial-tips/game-expect-user.en.md) | Sai Play captures a valid user UUID, keeps it for the browser tab and warns when the signed-in account differs. [Parameter handling](../../play.saigame.studio/lib/expected-user.ts), [session gate](../../play.saigame.studio/components/session-gate.tsx#L20) |
| [Keep the SDK Unmodified](../public/tutorial-tips/keep-sdk-unmodified.en.md) | Maintenance guidance for keeping game scripts outside `Assets/SaiGame` and calling the SDK's public methods and events. |
| [Banner Ad Impressions](../public/tutorial-tips/banner-ad-impressions.en.md) | Ad-network counting, refresh and policy claims require provider documentation. The SDK's optional banner setup and controls are documented separately. [LevelPlay integration](../../ss-unity/Assets/SaiGame/Optional/LevelPlay/README.md) |

## Implementation notes

- **Generator Initial Output is absent in the mailbox flow.** The admin item form lets you set `initial_output` per output item, but the backend only grants it inside `AssignGenerator` ([generator_usecase.go](../../ss-go/internal/usecase/generator_usecase.go)), which no HTTP route calls. Generators sent through the Mailbox (the flow in [Claim Resources from Generator](../public/tutorial-guides/claim-resources-from-generator.en.md)) never grant Initial Output.
- **Crafting ignores Burn-off materials.** `Craft` in [local_crafting_service.go](../../ss-go/internal/services/implementations/local_crafting_service.go) skips the ownership check for inputs with Burn off (`is_consumed = false`), so a "required but not consumed" item such as a Recipe Scroll cannot lock a recipe. The [Creating a craft recipe](../public/tutorial-guides/creating-a-craft-recipe.en.md) lesson now documents this behavior. If the intent is "required but not consumed", the backend needs a presence check for these inputs.
- **Failed crafts consume Burn-on materials.** Materials are deducted before the success roll result is applied, so a failed craft still costs all burned materials. The lesson documents this behavior.

- **"Enable 2FA before creating a studio" is frontend-only.** [app/studios/page.tsx](../app/studios/page.tsx) blocks the button, but `POST /api/v1/studios` ([studio_usecase.go](../../ss-go/internal/usecase/studio_usecase.go)) does not check 2FA.

## Candidate topics for new guides

- **Battle Pass / Session Quest Pools**: [BattlePass.cs](../../ss-unity/Assets/SaiGame/Scripts/5_Quest/BattlePass/BattlePass.cs), [session_quest_pool.go](../../ss-go/internal/domain/session_quest_pool.go)
- **Generic quest progression**: [QuestProgressor.cs](../../ss-unity/Assets/SaiGame/Scripts/5_Quest/Progress/QuestProgressor.cs)
- **Client add/deduct of items**: [ItemAddDeduct.cs](../../ss-unity/Assets/SaiGame/Scripts/3_ItemContainer/Item/ItemAddDeduct.cs)
- **Item definition download**: [ItemDefinitions.cs](../../ss-unity/Assets/SaiGame/Scripts/3_ItemContainer/Item/ItemDefinitions.cs)
- **Battle history**: [BattleSessions.cs](../../ss-unity/Assets/SaiGame/Scripts/8_Battle/BattleSessions.cs)
- **Plugins / subscription tiers**: lessons only mention "Rare"; nothing explains what each tier unlocks ([plugin.go](../../ss-go/internal/domain/plugin.go))
- **Two-factor authentication**: account 2FA with recovery codes, 2FA proof for deleting games/studios and API keys, per-game **Allow player 2FA** ([game-player-two-factor.md](../../ss-go/docs/api/game-player-two-factor.md), [auth_two_factor.go](../../ss-go/internal/usecase/auth_two_factor.go)); Unity `SaiAuth.VerifyTwoFactor`
- **Game API keys and item grants**. The backend registers a key-authenticated item-grant route and a studio audit-log route. [API routes](../../ss-go/internal/handler/route_definitions/route_definitions_api_keys.go), [middleware registration](../../ss-go/cmd/gateway/bootstrap/app.go#L372)
- **Game public info and image upload** (release status, content, CDN image, main currency, is public): [game_public_info.go](../../ss-go/internal/domain/game_public_info.go), [game_media_asset.go](../../ss-go/internal/domain/game_media_asset.go)
- **Sai Play player portal and sGem** (KB note: [Sai Play player portal](../../docs/knowledge-base/topics/platform/sai-play.md)): [play.saigame.studio](../../play.saigame.studio/AGENTS.md), [sgem.go](../../ss-go/internal/domain/sgem.go)
- **Other Studio pages**. Lore, System Prompts (AI), Item Profiles, Clone Game and Users.
- **Steam sign-in, account linking, Claim Game and achievements**. [Steam setup](../../ss-unity/Assets/SaiGame/Scripts/10_Steam/Link/README.md), [achievement setup](../../ss-unity/Assets/SaiGame/Scripts/10_Steam/Achievement/README.md)
- **Unity LevelPlay integration**. Cover SDK setup, runtime controls and fallback behavior. [Setup and controls](../../ss-unity/Assets/SaiGame/Optional/LevelPlay/README.md), [banner fallback](../../ss-unity/Assets/SaiGame/Optional/LevelPlay/UnityAds.cs#L101)
