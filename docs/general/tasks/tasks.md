# Tasks

*Written by: Kramb*

---

This page lists unit task types, the object and task attributes they use, and XS examples where available. If a task or description is incomplete or incorrect, please let the authors of this guide know!

Attributes without an available XS constant are marked **Unavailable**.

## 1. Move to

- ID: 1

- Unknown.

## 2. Follow

- ID: 2

- Unknown.

## 3. Garrison

- ID: 3

- Ability to garrison a unit into another unit or building.

<h3>Object attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cGarrisonCapacity | Target object must have some capacity for the current unit to garrison to. |
| cGarrisonType | If target object is a building, it must have a garrison type that matches current unit's type. |
| cTraits | If target object is a unit, it must have this bitfield 1st bit (1) set for garrison unit. |

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkRange | Range at which a unit can garrison. |
| cTaskAttrOwnerType | Controls which objects the task can target based on ownership. Values: **0** — All objects; **1** — Your objects only; **2** — Neutral and enemy objects only; **3** — Gaia only; **4** — Gaia, your and ally objects only; **5** — Gaia, neutral and enemy objects only; **6** — All but your objects. |
| cTaskAttrObjectId | Object in which a unit can garrison. |
| cTaskAttrObjectClass | Object in which a unit can garrison. |

<h3>XS example</h3>

```xs
/* This code gives player 1 scorpion an ability to garrison into friendly castles at a range of 5 */

const int player = 1;
const int scorpion = 279;
const int castle = 82;
const float range = 5.0;
const int garrisonSiegeType = 32;
const int gaiaYouAndAlly = 4;

int currentGarrisonType = xsGetObjectAttribute(player, castle, cGarrisonType);
xsEffectAmount(cSetAttribute, castle, cGarrisonType, currentGarrisonType + garrisonSiegeType, player);

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkRange, range);
xsTaskAmount(cTaskAttrOwnerType, gaiaYouAndAlly);
xsTaskAmount(cTaskAttrTaskType, cTaskTypeGarrison);
xsTaskAmount(cTaskAttrObjectClass, cBuildingClass);

xsModifyObjectTasks(scorpion, player);
```

## 4. Explore

- ID: 4

- Unknown.

## 5. Gather/rebuild

- ID: 5

- Unknown.

## 6. Graze

- ID: 6

- Unknown.

## 7. Combat

- ID: 7

- Unknown.

## 8. Shoot

- ID: 8

- Unknown.

## 9. Attack

- ID: 9

- Unknown.

## 10. Fly

- ID: 10

- Unknown.

<h3>Object attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cStanding2Graphic | Used instead of the task's **Working graphic (14)**. Graphic while moving, if not set uses moving graphic. |
| cWalkingGraphic | Used if **[Standing Graphic 2 (72)](../../attributes/attributes/#72-standing-graphic-2)** or the task's **Working graphic (14)** is not set. |

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Unit speed multiplier while roaming. |
| cTaskAttrWorkValue2 | Unit ID to avoid. |
| cTaskAttrWorkRange | Minimum distance to the unit to avoid that will be maintained while roaming. |
| cTaskAttrSearchWaitTime | Time in seconds that the unit pauses, playing the idle animations, when changing direction. |
| cTaskAttrCombatLevelFlag | If set to 1, only roam around if the unit is owned by Gaia. |
| cTaskAttrTerrain | Terrain Table that the unit will be allowed to roam on. If -1, use the unit's terrain table. |
| cTaskAttrMovingGraphic | Graphics used for the unit moving around, randomly alternates between them. |
| cTaskAttrProceedingGraphic | Graphics used for the unit moving around, randomly alternates between them. |
| cTaskAttrWorkingGraphic | Graphics used for the unit moving around, randomly alternates between them. |
| cTaskAttrCarryCheck | Distance the unit is allowed to move from its starting position before picking a new direction to return closer. If 0, no limit. |

## 11. Scare/hunt

- ID: 11

- Unknown.

## 12. Unload boat like

- ID: 12

- Ability for a unit to unload when reaching certain terrain.

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue2 | Unknown. |
| cTaskAttrTerrain | Terrain on which unit can unload. |

<h3>XS example</h3>

```xs
/* This code gives player 1 longboats an ability to load and unload friendly berserkers as a transport ship with a capacity of 20. */

const int player = 1;
const int berserk = 692;
const int longboat = 250;
const float range = 1.0;
const int capacity = 20;
const int garrisonUnitTrait = 1;
const int shipUnitTrait = 2;
const int beachTerrain = 2;
const int gaiaYouAndAlly = 4;

xsEffectAmount(cSetAttribute, longboat, cGarrisonCapacity, capacity, player);
xsEffectAmount(cSetAttribute, longboat, cTraits, garrisonUnitTrait + shipUnitTrait, player);

xsResetTaskAmount();
xsTaskAmount(cTaskAttrTerrain, beachTerrain);
xsTask(longboat, cTaskTypeUnloadBoatLike, -1, player);

xsResetTaskAmount();
xsTaskAmount(cTaskAttrWorkRange, range);
xsTaskAmount(cTaskAttrOwnerType, gaiaYouAndAlly);
xsTask(berserk, cTaskTypeGarrison, cWarshipClass, player);
```

## 13. Guard

- ID: 13

- Unknown.

## 14. Unload over wall

- ID: 14

- Ability for units to unload units over buildings. Only works for walls. For other buildings unit is unloaded on the same side as the task containing unit.

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue2 | Unknown. |
| cTaskAttrWorkRange | Unknown. |
| cTaskAttrWorkingGraphic | Graphic of the unit when unloading. |
| cTaskAttrCarryCheck | Unknown. |
| cTaskAttrObjectId | Building id or class over which to unload units. |
| cTaskAttrObjectClass | Building id or class over which to unload units. |

## 21. Make

- ID: 21

- Unknown. Related to farms, fishing traps and similar. Maybe the ability to remake them?

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Unknown. |
| cTaskAttrResourceIn | Unknown; resource being collected. |
| cTaskAttrProductivityResource | Unknown, sometimes resource being deposited to. |

## 101. Build

- ID: 101

- Ability for units to build buildings. Building seems hardcoded for villagers and fishing ships. Military units can use this task to build 1 building.

<h3>Object attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cWorkRate | Rate at which the unit builds. |
| cTraits | Set this bitfield 3rd bit (4) to enable military units to build 1 building. |
| cTraitPiece | Building id to build. |

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Multiplier for **[Work rate (13)](../../attributes/attributes/#13-work-rate)**. |
| cTaskAttrWorkRange | Build range. |
| cTaskAttrSearchWaitTime | Unknown. |
| cTaskAttrProceedingGraphic | Graphic used while the unit is building. |
| cTaskAttrWorkingGraphic | Graphic of the unit building a secondary building. |
| cTaskAttrDepositSound | Sound id of the unit building. |
| cTaskAttrAutoSearch | Unknown. |
| cTaskAttrBuildingPick | Unknown. |
| cTaskAttrObjectId | For units building 1 building must be the id of the building and match the **[Trait piece (56)](../../attributes/attributes/#56-trait-piece)** field, for villagers this value is -1. |
| cTaskAttrObjectClass | For units building 1 building must be the id of the building and match the **[Trait piece (56)](../../attributes/attributes/#56-trait-piece)** field, for villagers this value is -1. |

<h3>XS example</h3>

```xs
/* This code gives player 1 obuch an ability to build fortresses. The unit can build it from a range of 2 and the build rate is its work rate multiplied by 3 */

const int player = 1;
const int obuch = 1701;
const int fortress = 33;
const float workRateMultiplier = 3.0;
const float buildRange = 2.0;
const int obuchAttackGraphic = 12311;
const int enableMilitaryUnitBuilding = 4;

xsEffectAmount(cEnableObject, fortress, cAttributeEnable, 1, player);
xsEffectAmount(cSetAttribute, obuch, cTraits, enableMilitaryUnitBuilding, player);
xsEffectAmount(cSetAttribute, obuch, cTraitPiece, fortress, player);

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkValue1, workRateMultiplier);
xsTaskAmount(cTaskAttrWorkRange, buildRange);
xsTaskAmount(cTaskAttrProceedingGraphic, obuchAttackGraphic);
xsTaskAmount(cTaskAttrTaskType, cTaskTypeBuild);
xsTaskAmount(cTaskAttrObjectId, fortress);

xsModifyObjectTasks(obuch, player);
```

## 102. Make unit

- ID: 102

- Unknown.

## 103. Make tech

- ID: 103

- Unknown.

## 104. Convert

- ID: 104

- Ability for units to convert other units. Monks use task attributes, non-monks use object and task attributes. For non-monk units this ability does not work if the unit does not have an attack or similar task already. When adding this task to regular units, existing units will have empty faith bar and will not regenerate, newly created ones will work fine. In addition I did not find a way to add targeting limitations, it seems whatever values are set you can always convert all units and buildings.

<h3>Object attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cMaxCharge | Amount of value to regenerate to regain conversion ability, usually set to 1. |
| cRechargeRate | Amount of charge regenerated per second. |
| cChargeEvent | Conversion range for non-monks. |
| cChargeType | Set to -4 to enable conversion for non-monks. |
| cButtonIconId | Icon for the conversion button. |
| cShortTooltipId | String ID for the conversion button's short tooltip. |
| cExtendedTooltipId | String ID for the conversion button's extended tooltip. |
| cChargeTarget | Conversion percent chance. For example, for 50% set to 50. Not changeable with triggers yet, use task attributes instead. |

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Minimum conversion time in seconds. |
| cTaskAttrWorkValue2 | Maximum conversion time in seconds. |
| cTaskAttrWorkRange | Conversion range, if positive takes precedence over object attribute. |
| cTaskAttrSearchWaitTime | Unknown, for monks it's set to 3091, for buildings 3049, for siege 3093 and for units to 0. Probably somehow related to these abilities being unlocked by research. Maybe unused. |
| cTaskAttrCombatLevelFlag | Unknown. |
| cTaskAttrProductivityResource | If set associated resource value is a modifier to conversion chance. |
| cTaskAttrUnusedResource | If set enable conversion and apply to the conversion range if the associated resource value is greater than 0. |
| cTaskAttrEnableTargeting | Unknown. |
| cTaskAttrObjectId | Target object or object class to be an eligible target for conversion. |
| cTaskAttrObjectClass | Target object or object class to be an eligible target for conversion. |

## 105. Heal

- ID: 105

- Ability of a unit to heal other units.

<h3>Object attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cWorkRate | Rate at which the unit heals. |

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Multiplier for **[Work rate (13)](../../attributes/attributes/#13-work-rate)**. |
| cTaskAttrProceedingGraphic | Graphic used while the unit is healing. |

<h3>XS example</h3>

```xs
/* This code gives player 1 teutonic knight an ability to heal units. The healing work rate multiplied was set to 5x. */

const int player = 1;
const int teutonicKnight = 25;
const float workRateMultiplier = 5.0;
const float conversionRange = 10.0;

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkValue1, workRateMultiplier);
xsTaskAmount(cTaskAttrProceedingGraphic, 1160);

xsTask(teutonicKnight, cTaskTypeHeal, -1, player);
```

## 106. Repair

- ID: 106

- Ability for unit to repair buildings or units.

<h3>Object attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cWorkRate | Rate at which the unit repairs. |

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Multiplier for **[Work rate (13)](../../attributes/attributes/#13-work-rate)**. |
| cTaskAttrSearchWaitTime | Unknown. |
| cTaskAttrProceedingGraphic | Graphic used while the unit is repairing. |
| cTaskAttrWorkingGraphic | Graphic of a unit repairing, seems to be not needed. |
| cTaskAttrDepositSound | Sound id of the unit repairing. |
| cTaskAttrAutoSearch | Unknown. |
| cTaskAttrBuildingPick | Unknown. |
| cTaskAttrObjectId | If -1 repairs everything that is repairable, if set repairs that specific object or objects of a class. |
| cTaskAttrObjectClass | If -1 repairs everything that is repairable, if set repairs that specific object or objects of a class. |

<h3>XS example</h3>

```xs
/* This code gives player 1 obuch an ability to repair buildings and repairable units. the repair rate is 3 times the work rate. */

const int player = 1;
const int obuch = 1701;
const float workRateMultiplier = 3.0;
const int obuchAttackGraphic = 12311;

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkValue1, workRateMultiplier);
xsTaskAmount(cTaskAttrProceedingGraphic, obuchAttackGraphic);

xsTask(obuch, cTaskTypeRepair, -1, player);
```

## 107. Get auto-converted

- ID: 107

- Ability to be auto-converted to the player based on that player's other nearby units (e.g., sheep). Does not seem to work on normal units and buildings.

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrSearchWaitTime | String ID of a text to display when the unit is converted. |
| cTaskAttrObjectId | Always -1. |
| cTaskAttrObjectClass | Always -1. |

## 108. Discovery artifact

- ID: 108

- Unknown.

## 110. Hunt

- ID: 110

- Gives the ability to gather resources from map objects and place it into player resources. Since drop sites can't be changed with triggers this task can't be added.

<h3>Object attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cWorkRate | Rate at which the unit gathers resources. |
| **Unavailable** — Drop sites | Object at which gathered resources are deposited. |

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Multiplier for **[Work rate (13)](../../attributes/attributes/#13-work-rate)**. |
| cTaskAttrWorkRange | Gather range. |
| cTaskAttrSearchWaitTime | Unknown. |
| cTaskAttrCombatLevelFlag | Unknown. |
| cTaskAttrOwnerType | Controls which objects the task can target based on ownership. Values: **0** — All objects; **1** — Your objects only; **2** — Neutral and enemy objects only; **3** — Gaia only; **4** — Gaia, your and ally objects only; **5** — Gaia, neutral and enemy objects only; **6** — All but your objects. |
| cTaskAttrResourceIn | Resource to take from the hunted animal. |
| cTaskAttrResourceOut | Associated resource to deposit gathered resource into. |
| cTaskAttrUnusedResource | If the associated resource value is 1, the hunted corpse does not decay. |
| cTaskAttrProceedingGraphic | ID of the graphic used while the unit is attacking. |
| cTaskAttrWorkingGraphic | ID of the graphic used while the unit is gathering. |
| cTaskAttrCarryingGraphic | ID of the graphic used while the unit is carrying resources. |
| cTaskAttrAutoSearch | If set to 1 unit searches for nearby objects to continuously gather from. |
| cTaskAttrCarryCheck | If set to 1 check if target object has resource before gathering, if set to 0 use Target Diplomacy (6) instead. |
| cTaskAttrObjectId | The object to gather from. |
| cTaskAttrObjectClass | The object to gather from. |

## 111. Trade

- ID: 111

- Adds the ability of the unit to trade for gold with other buildings. Since drop sites can't be changed with triggers this task can't be added.

<h3>Object attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cWorkRate | Rate at which the unit trades resources. |
| **Unavailable** — Drop sites | Object to which trade resources are returned. |

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Multiplier for **[Work rate (13)](../../attributes/attributes/#13-work-rate)**. |
| cTaskAttrResourceIn | Unknown. |
| cTaskAttrProductivityResource | Productivity for secondary trade resource. |
| cTaskAttrResourceOut | Secondary resource to trade for other than gold when is enabled. |
| cTaskAttrCarryingGraphic | ID of the graphic used while the unit is carrying trade resources. |
| cTaskAttrObjectId | Building to trade with. |
| cTaskAttrObjectClass | Building to trade with. |

## 120. Generate wonder victory

- ID: 120

- Ability for the object to start a wonder victory timer. Adding it to another object does not seem to work.

## 121. Deselect when tasked

- ID: 121

- Unknown. Related to farms finishing traps and similar.

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Unknown. |
| cTaskAttrResourceIn | Unknown; resource being collected. |

## 122. Loot gather

- ID: 122

- Unknown.

## 123. Housing

- ID: 123

- Unknown.

## 124. Pack

- ID: 124

- Unknown.

## 125. Unpack and attack

- ID: 125

- Ability to unpack from one unit to another and attack. Not possible to add this task with triggers currently.

<h3>Object attributes</h3>

| XS constant | Description |
| :-- | :-- |
| **Unavailable** — Transform unit | Unit id to transform to. |

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrCombatLevelFlag | Unknown. |
| cTaskAttrEnableTargeting | Unknown. |

## 131. Off map trade

- ID: 131

- Unknown.

## 132. Pickup unit

- ID: 132

- Ability to pick up targeted objects and turn into a different unit when done. Seems to only work on relics.

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Unit id to change into when picking up an object. |
| cTaskAttrObjectId | Object id to pick up. Seems to ignore this value and only works on relics. |
| cTaskAttrObjectClass | Object id to pick up. Seems to ignore this value and only works on relics. |

<h3>XS example</h3>

```xs
/* This code gives player 1 mangudai an ability to pick up relics and turn into Genghis Khan. Relics are consumed in the process. */

const int player = 1;
const int mangudai = 11;
const int genghis = 731;

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkValue1, genghis);
xsTaskAmount(cTaskAttrTaskType, cTaskTypePickupUnit);
xsTaskAmount(cTaskAttrObjectClass, cRelicClass);
xsModifyObjectTasks(mangudai, player);
```

## 133. Charge attack

- ID: 133

- Ability to increase the object's speed when closing the distance for an attack.

<h3>Object attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cMaxCharge | Value added to the attack while charging. Must be at least 1 for the charge to work. |
| cRechargeRate | Amount of charge regenerated per second. The charge can be used again when it reaches **[Maximum Charge (59)](../../attributes/attributes/#59-maximum-charge)**. |
| cChargeEvent | Must be 0 or 1 for the task to work. |
| cChargeType | Must be 1 for the task to work. |
| cSpecialAbility | Must be 3 for the task to work. |

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Minimum distance from the target for the speed up to start. |
| cTaskAttrWorkValue2 | Maximum distance from the target for the speed to start. |
| cTaskAttrWorkRange | Multiplier on the unit speed while charging. |
| cTaskAttrWorkFlag2 | Must be 2001 for the task to work. |

<h3>XS example</h3>

```xs
/* This code gives player 1 knights an ability to charge enemy units, during which they increase their speed by 2.5 times and their attack by 5. This ability has a minimum range of 2, a max range of 7 and a cooldown of 30 seconds. */

const int player = 1;
const int knight = 38;
const float minDistance = 2;
const float maxDistance = 7;
const float speedMultiplier = 2.5;
const int taskEnableFlag = 2001;
const int chargeAbility = 3;
const int chargeEvent = 0;
const int chargeType = 1;
const float chargeAttackBonus = 5.0;
const float cooldownDuration = 30.0;

xsEffectAmount(cSetAttribute, knight, cSpecialAbility, chargeAbility, player);
xsEffectAmount(cSetAttribute, knight, cChargeType, chargeType);
xsEffectAmount(cSetAttribute, knight, cChargeEvent, chargeEvent);
xsEffectAmount(cSetAttribute, knight, cMaxCharge, chargeAttackBonus, player);
xsEffectAmount(cSetAttribute, knight, cRechargeRate, chargeAttackBonus / cooldownDuration, player);

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkValue1, minDistance);
xsTaskAmount(cTaskAttrWorkValue2, maxDistance);
xsTaskAmount(cTaskAttrWorkRange, speedMultiplier);
xsTaskAmount(cTaskAttrWorkFlag2, taskEnableFlag);

xsTask(knight, cTaskTypeChargeAttack, -1, player);
```

## 134. Transform unit

- ID: 134

- Unknown.

## 135. Kidnap unit

- ID: 135

- Ability to take an enemy unit and when returning to a town center convert it to your own. Attacking another unit while having a kidnapped unit will release that unit. If a unit has another task that can be performed on a target - this task will not work. Units can be kidnapped on their dying animations but will be returned as corpses.

<h3>Object attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cGarrisonCapacity | Unit must have some capacity to hold a kidnapped unit. |
| **Unavailable** — Task swap group | Will swap the kidnapper into a different unit that also has the same value in this attribute after the kidnapping. |

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrOwnerType | Controls which objects the task can target based on ownership. Values: **0** — All objects; **1** — Your objects only; **2** — Neutral and enemy objects only; **3** — Gaia only; **4** — Gaia, your and ally objects only; **5** — Gaia, neutral and enemy objects only; **6** — All but your objects. |
| cTaskAttrObjectId | Unit id or class id that can be kidnapped. |
| cTaskAttrObjectClass | Unit id or class id that can be kidnapped. |

<h3>XS example</h3>

```xs
/* This code removes scout attack ability, but gives it an ability to kidnap enemy villagers, and convert them to player 1 when visiting the town center */

const int player = 1;
const int scout = 448;
const int garrisonCapacity = 1;
const int neutralAndEnemy = 2;
const int previousCombatSearchWaitTime = 3;

xsEffectAmount(cSetAttribute, scout, cGarrisonCapacity, garrisonCapacity, player);

xsResetTaskAmount();
xsTaskAmount(cTaskAttrSearchWaitTime, previousCombatSearchWaitTime);
xsRemoveTask(scout, cTaskTypeCombat, -1, player);

xsResetTaskAmount();
xsTaskAmount(cTaskAttrOwnerType, neutralAndEnemy);
xsTaskAmount(cTaskAttrTaskType, cTaskTypeKidnapUnit);
xsTaskAmount(cTaskAttrObjectClass, cVillagerClass);
xsModifyObjectTasks(scout, player);
```

## 136. Deposit unit

- ID: 136

- Ability to deposit picked up objects (task 132) into a building and change to a different unit when done. Seems to only work on relics.

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Unit id to change into when depositing an object. |
| cTaskAttrObjectId | Building id to deposit the picked up object to, does not seem to work with custom units. |
| cTaskAttrObjectClass | Building id to deposit the picked up object to, does not seem to work with custom units. |

## 149. Shear

- ID: 149

- Unknown.

## 151. Generate resources

- ID: 151

- Ability of an object to gain resources when attacking or idling.

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Amount of resources received. |
| cTaskAttrCombatLevelFlag | For units, set to 2 to generate resources passively. Buildings always generate resources passively. |
| cTaskAttrProductivityResource | The value of this resource is used as a multiplier of the amount received. Must be set to some resource containing a positive value for the task to work. |
| cTaskAttrResourceOut | Resource type to receive. |
| cTaskAttrObjectId | Object which if attacked by a unit will generate resource. |
| cTaskAttrObjectClass | Object which if attacked by a unit will generate resource. |

<h3>XS example</h3>

```xs
/* This code makes player 1 Attila the Hun gain gold when attacking enemy infantry, archer or cavalry units */

const int player = 1;
const int attila = 777;
const float resourceGainRate = 1.0;
const int resourceToGain = cAttributeGold;
const int productivityResource = 600;
const float productivity = 1.0;

xsSetPlayerAttribute(player, productivityResource, productivity);

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkValue1, resourceGainRate);
xsTaskAmount(cTaskAttrProductivityResource, productivityResource);
xsTaskAmount(cTaskAttrResourceOut, resourceToGain);

xsTaskAmount(cTaskAttrTaskType, cTaskTypeGenerateResources);

xsTaskAmount(cTaskAttrObjectClass, cInfantryClass);
xsModifyObjectTasks(attila, player);

xsTaskAmount(cTaskAttrObjectClass, cArcherClass);
xsModifyObjectTasks(attila, player);

xsTaskAmount(cTaskAttrObjectClass, cCavalryClass);
xsModifyObjectTasks(attila, player);
```

## 152. Movement damage

- ID: 152

- Ability for a unit to damage surrounding enemy units while moving.

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Amount of damage to deal per tick. If negative will increase the current HP instead. Will go over max HP. |
| cTaskAttrWorkValue2 | How often the unit damages surrounding units in fraction of seconds. |
| cTaskAttrWorkRange | Range of this damage surrounding the current unit. |

<h3>XS example</h3>

```xs
/* This code gives player 1 war elephant an ability to damage enemy units while moving in a 0.75 range twice per second for 2.5 damage */

const int player = 1;
const int elephant = 239;
const float damage = 2.5;
const float time = 0.5;
const float range = 0.75;

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkValue1, damage);
xsTaskAmount(cTaskAttrWorkValue2, time);
xsTaskAmount(cTaskAttrWorkRange, range);

xsTask(elephant, cTaskTypeMovementDamage, -1, player);
```

## 153. Movable dropsite

- ID: 153

- Ability for a unit to be a movable dropsite. For this task to work this unit needs to be added for the worker unit as a dropsite (currently not possible with triggers or XS).

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrSearchWaitTime | Unknown. |
| cTaskAttrCarryCheck | Unknown. |
| cTaskAttrObjectId | Resources containing object for which this unit exists as a dropsite. |
| cTaskAttrObjectClass | Resources containing object for which this unit exists as a dropsite. |

## 154. Loot

- ID: 154

- Ability of an object to gain resources and attributes after killing or converting an object.

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Amount of resources received. |
| cTaskAttrWorkRange | If set to 0 applies to all units. If set to >0 then it applies to only units whose player matches this value. |
| cTaskAttrWorkFlag2 | If set, maximum number of times this unit can trigger the task. |
| cTaskAttrSearchWaitTime | ID of the object attribute modified by this task. Attributes known to be supported include: **[Hit points (0)](../../attributes/attributes/#0-hit-points),** **[Attack (9)](../../attributes/attributes/#9-attack)**. |
| cTaskAttrCombatLevelFlag | If set to 1, unit will gain attributes. |
| cTaskAttrResourceIn | If set the tech of the associated resources value id will be researched. |
| cTaskAttrProductivityResource | If positive, the associated resource value must be greater than 0 for this task to activate. The positive value multiplies the resources gained. If negative, its absolute value is treated as a technology ID, and that technology must be researched for this task to activate. |
| cTaskAttrResourceOut | Resource type to receive. |
| cTaskAttrUnusedResource | If set the tech of the associated resources value id will be researched. |
| cTaskAttrProceedingGraphic | Graphic that plays when the unit gains an attribute via the task. |
| cTaskAttrCarryCheck | If set, all Tasks 154 with the same Carry Check ID will count towards the same cap. |
| cTaskAttrGatherType | If unit gains attributes this attribute stores the amount of attribute the unit gains. |
| cTaskAttrObjectId | Object which if killed by this unit will trigger resource/attribute gain. If -1 affects all units. Has to be an object that can increase the kill/razing/conversions stats. |
| cTaskAttrObjectClass | Object which if killed by this unit will trigger resource/attribute gain. If -1 affects all units. Has to be an object that can increase the kill/razing/conversions stats. |

<h3>XS example 1</h3>

```xs
/* This code makes player 1 Attila the Hun gain 2 gold when killing enemy unit or destroying an enemy building */

const int player = 1;
const int attila = 777;
const float resourceGainRate = 2.0;
const int resourceToGain = cAttributeGold;

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkValue1, resourceGainRate);
xsTaskAmount(cTaskAttrResourceOut, resourceToGain);

xsTask(attila, cTaskTypeLoot, -1, player);
```

<h3>XS example 2</h3>

```xs
/* This code makes player 1 mangudai gain 1 attack every time they kill an infantry, archer, cavalry or siege unit to a maximum of 5 */

const int player = 1;
const int mangudai = 11;
const int maxNumberOfStatGains = 5;
const int gainAttributesFlag = 1;
const int attribute = cAttack;
const float amountToGain = 1.0;
const int levelUpGraphic = 12263;
const int statGainId = 1;

xsResetTaskAmount();

xsTaskAmount(cTaskAttrTaskType, cTaskTypeLoot);
xsTaskAmount(cTaskAttrWorkFlag2, maxNumberOfStatGains);
xsTaskAmount(cTaskAttrSearchWaitTime, attribute);
xsTaskAmount(cTaskAttrCombatLevelFlag, gainAttributesFlag);
xsTaskAmount(cTaskAttrProceedingGraphic, levelUpGraphic);
xsTaskAmount(cTaskAttrCarryCheck, statGainId);
xsTaskAmount(cTaskAttrGatherType, amountToGain);

xsTaskAmount(cTaskAttrObjectClass, cInfantryClass);
xsModifyObjectTasks(mangudai, player);

xsTaskAmount(cTaskAttrObjectClass, cArcherClass);
xsModifyObjectTasks(mangudai, player);

xsTaskAmount(cTaskAttrObjectClass, cCavalryClass);
xsModifyObjectTasks(mangudai, player);

xsTaskAmount(cTaskAttrObjectClass, cSiegeWeaponClass);
xsModifyObjectTasks(mangudai, player);
```

## 155. Aura

- ID: 155

- Auras are stat modifiers that affect all objects surrounding the aura object (or the aura object itself).

<h3>Object attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cRechargeRate | Amount of charge regenerated per second. Together with **[Maximum Charge (59)](../../attributes/attributes/#59-maximum-charge)**, this controls the temporary aura's cooldown. The cooldown ends when the charge reaches **[Maximum Charge (59)](../../attributes/attributes/#59-maximum-charge)**. For a 60-second cooldown, set **[Maximum Charge (59)](../../attributes/attributes/#59-maximum-charge)** to 1 and **[Recharge rate (60)](../../attributes/attributes/#60-recharge-rate)** to 0.01666667 (1.0 / 60.0). |
| cChargeEvent | For temporary auras stores aura duration when activated. |
| cChargeType | Set to -3 to enable temporary auras. |
| cCombatAbility | Attribute bitfield 6th bit (32) needs to be set for the aura to activate. If 7th bit is set (64) the aura will affect the unit itself instead of the units in range (aura prerequisites still need to be met on other units). |
| cButtonIconId | Icon for the temporary aura button. |
| cShortTooltipId | String ID for the temporary aura button's short tooltip. |
| cExtendedTooltipId | String ID for the temporary aura button's extended tooltip. |

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Aura attribute value to add or multiply. |
| cTaskAttrWorkValue2 | Minimum amount of units to be in range for the aura to activate. |
| cTaskAttrWorkRange | Aura range. If aura targets enemies the targeted enemy units must be in range of aura units sight range. |
| cTaskAttrSearchWaitTime | ID of the object attribute modified by this task. Attributes known to be supported include: [Hit points (0)](../../attributes/attributes/#0-hit-points), [Line of sight (1)](../../attributes/attributes/#1-line-of-sight), [Movement speed (5)](../../attributes/attributes/#5-movement-speed), [Attack (9)](../../attributes/attributes/#9-attack), [Attack reload time (10)](../../attributes/attributes/#10-attack-reload-time), [Maximum Range (12)](../../attributes/attributes/#12-maximum-range) (visual only), [Work rate (13)](../../attributes/attributes/#13-work-rate), [Regeneration rate (109)](../../attributes/attributes/#109-regeneration-rate), [Conversion chance modifier (113)](../../attributes/attributes/#113-conversion-chance-modifier), Melee armor (116), Pierce armor (117), [Regeneration HP percent (120)](../../attributes/attributes/#120-regeneration-hp-percent). |
| cTaskAttrCombatLevelFlag | Bit field of aura settings: **multiply (1)** multiplies attribute value instead of adds it, **circular (2)** makes aura range circular instead of square, **visible (4)** shows range indicator (is affected by ui settings), **temporary (8)** makes aura effect temporary, **activated (16)** the temporary effect is only applied on the moment of aura activation, and remains if target units leave the aura, **translucent (32)** make aura indicator translucent, unsure how it works as its overwritten by ui settings. |
| cTaskAttrOwnerType | Controls which objects the task can target based on ownership. Values: **0** — All objects; **1** — Your objects only; **2** — Neutral and enemy objects only; **3** — Gaia only; **4** — Gaia, your and ally objects only; **5** — Gaia, neutral and enemy objects only; **6** — All but your objects. |
| cTaskAttrProceedingGraphic | Graphic displayed over the units receiving the aura. |
| cTaskAttrGatheringSound | Short Tooltip for UI indicator. |
| cTaskAttrDepositSound | Long Tooltip for UI indicator. |
| cTaskAttrGatherType | UI indicator icon displayed (per icons.json). |
| cTaskAttrEnabled | If set, the associated resource value needs to be set to >0 for the aura to activate. |
| cTaskAttrObjectId | Object targeted by the aura. |
| cTaskAttrObjectClass | Object targeted by the aura. |

<h3>XS example 1</h3>

```xs
/* This code makes player 1 Joan of Arc give friendly infantry, archer and cavalry units within 10 range +5 to their attack */

const int player = 1;
const int joanOfArc = 629;
const int unitsInRangeToActivate = 1;
const float auraRange = 10.0;
const int attribute = cAttack;
const int value = 5;
const int gaiaYouAndAlly = 4;
const int circularFlag = 2;
const int visibleFlag = 4;
const int translucentFlag = 32;
const int auraAbility = 32;

xsEffectAmount(cSetAttribute, joanOfArc, cCombatAbility, auraAbility, player);

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkValue1, value);
xsTaskAmount(cTaskAttrWorkValue2, unitsInRangeToActivate);
xsTaskAmount(cTaskAttrWorkRange, auraRange);
xsTaskAmount(cTaskAttrSearchWaitTime, attribute);
xsTaskAmount(cTaskAttrCombatLevelFlag, circularFlag + visibleFlag + translucentFlag);
xsTaskAmount(cTaskAttrOwnerType, gaiaYouAndAlly);

xsTaskAmount(cTaskAttrTaskType, cTaskTypeAura);

xsTaskAmount(cTaskAttrObjectClass, cInfantryClass);
xsModifyObjectTasks(joanOfArc, player);

xsTaskAmount(cTaskAttrObjectClass, cArcherClass);
xsModifyObjectTasks(joanOfArc, player);

xsTaskAmount(cTaskAttrObjectClass, cCavalryClass);
xsModifyObjectTasks(joanOfArc, player);
```

<h3>XS example 2</h3>

```xs
/* This code makes player 1 Joan of Arc double the movement speed of friendly infantry, archers and cavalry units in range of 10 for 30 seconds, with a 60 second cooldown. Units can leave the aura range and still have the speed increase. */

const int player = 1;
const int joanOfArc = 629;
const int unitsInRangeToActivate = 1;
const float auraRange = 10.0;
const int attribute = cMovementSpeed;
const float value = 2.0;
const int gaiaYouAndAlly = 4;
const int multiplyFlag = 1;
const int circularFlag = 2;
const int temporaryAuraFlag = 8;
const int remainsWhenLeavingRangeFlag = 16;
const int auraAbility = 32;
const int enableTempAuraType = -3;
const float tempAuraDuration = 30.0;
const float tempAuraCooldown = 60.0;
const float maximumCharge = 1.0;
const int buttonIcon = 98;

xsEffectAmount(cSetAttribute, joanOfArc, cCombatAbility, auraAbility, player);

xsEffectAmount(cSetAttribute, joanOfArc, cChargeType, enableTempAuraType, player);
xsEffectAmount(cSetAttribute, joanOfArc, cChargeEvent, tempAuraDuration, player);
xsEffectAmount(cSetAttribute, joanOfArc, cMaxCharge, maximumCharge, player);
xsEffectAmount(cSetAttribute, joanOfArc, cRechargeRate, maximumCharge / tempAuraCooldown, player);
xsEffectAmount(cSetAttribute, joanOfArc, cButtonIconId, buttonIcon, player);

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkValue1, value);
xsTaskAmount(cTaskAttrWorkValue2, unitsInRangeToActivate);
xsTaskAmount(cTaskAttrWorkRange, auraRange);
xsTaskAmount(cTaskAttrSearchWaitTime, attribute);
xsTaskAmount(cTaskAttrCombatLevelFlag, multiplyFlag + circularFlag + temporaryAuraFlag + remainsWhenLeavingRangeFlag);
xsTaskAmount(cTaskAttrOwnerType, gaiaYouAndAlly);

xsTaskAmount(cTaskAttrTaskType, cTaskTypeAura);

xsTaskAmount(cTaskAttrObjectClass, cInfantryClass);
xsModifyObjectTasks(joanOfArc, player);

xsTaskAmount(cTaskAttrObjectClass, cArcherClass);
xsModifyObjectTasks(joanOfArc, player);

xsTaskAmount(cTaskAttrObjectClass, cCavalryClass);
xsModifyObjectTasks(joanOfArc, player);
```

## 156. Additional spawn

- ID: 156

- Spawns additional units when the unit is trained.

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Id of an additional unit to spawn. |
| cTaskAttrWorkValue2 | Number of units to spawn. |
| cTaskAttrResourceIn | If set, the value of the corresponding resource needs to be >0 for the Task to trigger. |
| cTaskAttrProductivityResource | If set, the associated resource value is added to the number of units to spawn. |

<h3>XS example</h3>

```xs
/* This code makes that every time a huskarl unit is spawned for player 1, 2 additional spearline units are also spawned from the same source. */

const int player = 1;
const int huskarl = 41;
const int spearman = 93;
const int amount = 2;

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkValue1, spearman);
xsTaskAmount(cTaskAttrWorkValue2, amount);

xsTask(huskarl, cTaskTypeExtraSpawn, -1, player);
```

## 157. Stinger

- ID: 157

- Stingers are stat modifiers applied on a unit being attacked or the attacking unit.

<h3>Object attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cCombatAbility | Attribute bitfield 8th bit (128) needs to be set for stingers to activate. |

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Stingers attribute value to add or multiply. |
| cTaskAttrWorkValue2 | Effect duration in seconds, if negative it's permanent. |
| cTaskAttrWorkRange | If 0 apply to the attacker, if 1 apply to the target of the attack (including splash damage targets). |
| cTaskAttrSearchWaitTime | ID of the object attribute modified by this task. Attributes known to be supported include: **[Hit points (0)](../../attributes/attributes/#0-hit-points), [Movement speed (5)](../../attributes/attributes/#5-movement-speed), [Attack (9)](../../attributes/attributes/#9-attack), [Attack reload time (10)](../../attributes/attributes/#10-attack-reload-time), [Regeneration rate (109)](../../attributes/attributes/#109-regeneration-rate), Melee armor (116), Pierce armor (117), [Regeneration HP percent (120)](../../attributes/attributes/#120-regeneration-hp-percent)**. |
| cTaskAttrCombatLevelFlag | Bit field of stingers settings: **Multiply (1)** multiplies attribute value instead of adds it, **Not stack (2)** does not allow other stinger tasks that modify same attribute to stack. |
| cTaskAttrOwnerType | Controls which objects the task can target based on ownership. Values: **0** — All objects; **1** — Your objects only; **2** — Neutral and enemy objects only; **3** — Gaia only; **4** — Gaia, your and ally objects only; **5** — Gaia, neutral and enemy objects only; **6** — All but your objects. |
| cTaskAttrProductivityResource | If positive, the associated resource value must be greater than 0 for this task to activate. |
| cTaskAttrObjectId | Object targeted by the stinger. |
| cTaskAttrObjectClass | Object targeted by the stinger. |

<h3>XS example</h3>

```xs
/* This code makes player 1 Joan of Arc slow infantry, archer and 
cavalry units she attacks to 20% of their speed for 5 seconds */

const int player = 1;
const int joanOfArc = 629;
const float value = -0.8;
const float duration = 5.0;
const int affectTarget = 1;
const int attribute = cMovementSpeed;
const int multiplyFlag = 1;
const int dontStackFlag = 2;
const int stingerAbility = 128;

xsEffectAmount(cSetAttribute, joanOfArc, cCombatAbility, stingerAbility, player);

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkValue1, value);
xsTaskAmount(cTaskAttrWorkValue2, duration);
xsTaskAmount(cTaskAttrWorkRange, affectTarget);
xsTaskAmount(cTaskAttrSearchWaitTime, attribute);
xsTaskAmount(cTaskAttrCombatLevelFlag, multiplyFlag + dontStackFlag);

xsTaskAmount(cTaskAttrTaskType, cTaskTypeStinger);

xsTaskAmount(cTaskAttrObjectClass, cInfantryClass);
xsModifyObjectTasks(joanOfArc, player);

xsTaskAmount(cTaskAttrObjectClass, cArcherClass);
xsModifyObjectTasks(joanOfArc, player);

xsTaskAmount(cTaskAttrObjectClass, cCavalryClass);
xsModifyObjectTasks(joanOfArc, player);
```

## 158. HP transformation

- ID: 158

- Transform into another unit based on current HP.

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | ID of the unit to transform to. |
| cTaskAttrWorkValue2 | HP to trigger the transformation. If >0 transforms when the unit's current HP is higher than the value. If <0 transforms when the unit's current HP is lower than the value made positive (currHp < (workVal * -1)). |
| cTaskAttrCombatLevelFlag | Bit field of HP transformation settings: **Multiply (1)** will use the Work value 2 (1) as a multiplier of current HP instead of exact value. |
| cTaskAttrProductivityResource | If positive, the associated resource value must be greater than 0 for this task to activate. If negative, its absolute value is treated as a technology ID, and that technology must be researched for this task to activate. |
| cTaskAttrResourceOut | If set, will add its associated resource value to the Work value 2 (1). |
| cTaskAttrProceedingGraphic | Graphic that plays when units transform. |
| cTaskAttrObjectId | Always -1. |
| cTaskAttrObjectClass | Always -1. |

<h3>XS example</h3>

```xs
/* This code makes player 1 karambit warrior transform into a berserk when under 40% hp, and transform back when above 60% using level up graphic */

const int player = 1;
const int karambit = 1123;
const int berserk = 692;
const float transformAtPercent = -0.4;
const float transformBackPercent = 0.6;
const int multiplyFlag = 1;
const int levelUpGraphic = 12263;

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkValue1, berserk);
xsTaskAmount(cTaskAttrWorkValue2, transformAtPercent);
xsTaskAmount(cTaskAttrCombatLevelFlag, multiplyFlag);
xsTaskAmount(cTaskAttrProceedingGraphic, levelUpGraphic);

xsTask(karambit, cTaskTypeHPTransform, -1, player);

xsTaskAmount(cTaskAttrWorkValue1, karambit);
xsTaskAmount(cTaskAttrWorkValue2, transformBackPercent);

xsTask(berserk, cTaskTypeHPTransform, -1, player);
```

## 159. Amphibious

- ID: 159

- Unit changes graphics based on current terrain.

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Movement Speed multiplier. |
| cTaskAttrWorkValue2 | Attack Speed multiplier. |
| cTaskAttrTerrain | Terrain (or Terrain Type) on which the unit will use the task. If >= 0: Terrain ID. If <0: Terrain Type (can combine multiple bits). |
| cTaskAttrMovingGraphic | Walking Graphic. |
| cTaskAttrProceedingGraphic | Attack Graphic. |
| cTaskAttrWorkingGraphic | Running Graphic. |
| cTaskAttrCarryingGraphic | Idle Graphic. |
| cTaskAttrGatheringSound | Dying Graphic. |
| cTaskAttrDepositSound | Undead Graphic. |

## 160. HP damage modifier

- ID: 160

- Unit has attribute modified based on percentage of missing HP.

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Value to add. |
| cTaskAttrWorkValue2 | Threshold of HP percentage to apply the modifier. |
| cTaskAttrWorkRange | If 0, check the unit's own HP. If > 0, compare the current target's HP. |
| cTaskAttrSearchWaitTime | ID of the object attribute modified by this task. Attributes known to be supported include: **[Attack (9)](../../attributes/attributes/#9-attack)**. |

<h3>XS example</h3>

```xs
/* This code makes player 1 throwing axeman unit gain +2 attack for each 20% of hp that it lost */

const int player = 1;
const int throwingAxeman = 281;
const int value = 2;
const float hpPercent = 0.2;
const int compareToTargetHp = 0;
const int attribute = cAttack;

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkValue1, value);
xsTaskAmount(cTaskAttrWorkValue2, hpPercent);
xsTaskAmount(cTaskAttrWorkRange, compareToTargetHp);
xsTaskAmount(cTaskAttrSearchWaitTime, attribute);

xsTask(throwingAxeman, cTaskTypeHPModifier, -1, player);
```

## 161. Unit refund

- ID: 161

- Resource to grant on death.

<h3>Task attributes</h3>

| XS constant | Description |
| :-- | :-- |
| cTaskAttrWorkValue1 | Value to refund. |
| cTaskAttrWorkRange | If 0, grant the resources to the player who owned the unit. If > 0, grant to the player who killed the unit. |
| cTaskAttrCombatLevelFlag | If 0, use Work Value 1 as a flat value to grant. If 1, use Work Value 1 as a fraction of the unit's associated resource cost. |
| cTaskAttrProductivityResource | If set, multiply Work Value 1 by the value of this resource. |
| cTaskAttrResourceOut | Resource to refund. |

<h3>XS example</h3>

```xs
/* This code makes 10 gold be refunded to player 1 when a monk unit is killed */

const int player = 1;
const int monk = 125;
const int monkWithRelic = 286;
const int value = 10;
const int grantToKiller = 0;
const int valueIsFractionOfCost = 0;
const int resource = cAttributeGold;

xsResetTaskAmount();

xsTaskAmount(cTaskAttrWorkValue1, value);
xsTaskAmount(cTaskAttrWorkRange, grantToKiller);
xsTaskAmount(cTaskAttrCombatLevelFlag, valueIsFractionOfCost);
xsTaskAmount(cTaskAttrResourceOut, resource);

xsTask(monk, cTaskTypeRefund, -1, player);
xsTask(monkWithRelic, cTaskTypeRefund, -1, player);
```
