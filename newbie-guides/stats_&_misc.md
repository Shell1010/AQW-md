---
dg-publish: true
dg-metatags:
  og:site_name: AQW Hub
  og:title: Stats and Misc Guides
  og:description: Player stats and other miscellaneous information 
  description: Player stats and other miscellaneous information 
  og:image: https://bigrat.monster/media/bigrat.jpg
---
I’ve made a Utility application for AQW, mainly terminal based. If anyone’s interested in testing it out it’s on [this repository](https://github.com/Shell1010/aqw-utils). Reason I put it here is because it’s nerd related as most of it is gathered from packet sniffing.

This will entail information regarding player stats alongside some information that may not necessarily fall into other guide sections. Here are some abbreviations so you don't get lost:
- AP - Attack Power
- SP - Spell Power

---

## Primary Stats effect on secondary stats

**Strength**
- Increases AP to all stat models, Critical chance to melee and hybrid models

**Intellect**
- Increases SP to all stat models and Mag In resist, provides Haste and Mag Out to all Caster models and only the Hybrid model.
	- Hybrid Luck gets additional haste but no Mag out

**Dexterity**
- Increases Dodge to all stat models, increases Hit chance and Haste to melee and hybrid models
	- Max dodge is considered to be 86.3%, if an enemy still hits you after having more than 86.3% dodge they probably don't miss
	- Max Haste is 50%, meaning skill cooldowns are decreased by 50%.

**Wisdom**
- Increases Dodge to all stat models, increases Hit and Critical chance to caster and hybrid luck models


**Endurance**
- Increases health to all stat models
- Gives +5 HP per point
$$
BaseHP = (\frac{CurrenLevel - 1}{MaxLevel - 1})^{0.66}\times1640+360
$$
$$
HP = Endurance \times EndMod + BaseHP
$$

**Luck**
- Increases Hit, Haste, Dodge, Critical Chance, Critical Damage, AP to melee classes and SP to caster classes, hybrid get both AP/SP.

## Stat Models

Stat models provide different modifiers for specific stats, for example having 30 intellect on the stat model Tank Melee will have a different effect on a class with the stat model Offensive Caster. You can view the stat model of your class through Character > Stat Overview. There’s a +- 0.0000000001 Deviation per level, this will barely not matter but I'm just saying it exists according to math.

**Tank Melee**
- Strength - 2 AP, 0.4% Critical Chance 
- Intellect - 2 SP, -1% Mag In
- Dexterity - 0.2% Hit Chance, 0.3% Haste, 0.3% Dodge
- Wisdom - 0.3% Dodge, 
- Luck - 0.7 AP, 0.2% Critical Chance, 0.1% Hit Chance, 0.1% Haste, 0.1% Dodge, 5% Crit Modifier  

**Dodge Melee**
- Strength - 2 AP, 0.4% Critical Chance 
- Intellect - 2 SP, -1% Mag In
- Dexterity - 0.2% Hit Chance, 0.5% Haste, 0.5% Dodge
- Wisdom - 0.3% Dodge, 
- Luck - 0.7 AP, 0.2% Critical Chance, 0.1% Hit Chance, 0.1% Haste, 0.1% Dodge, 5% Crit Modifier

**Power Melee**
- Strength - 2 AP, 0.7% Critical Chance 
- Intellect - 2 SP, -1% Mag In
- Dexterity - 0.2% Hit Chance, 0.5% Haste, 0.5% Dodge
- Wisdom - 0.3% Dodge, 
- Luck - 0.7 AP, 0.2% Critical Chance, 0.1% Hit Chance, 0.1% Haste, 0.1% Dodge, 5% Crit Modifier,  

**Defensive Caster**
- Strength - 2 AP
- Intellect - 2 SP, -1% Mag In, * 0.5% Haste, * 1% Mag Out
- Dexterity - 0.3% Dodge
- Wisdom - 0.3% Dodge, 0.2% Hit Chance, 0.4% Crit Chance
- Luck - 0.7 SP, 0.2% Critical Chance, 0.1% Hit Chance, 0.1% Haste, 0.1% Dodge, 5% Crit Modifier

**Offensive Caster**
- Strength - 2 AP
- Intellect - 2 SP, -1% Mag In, 0.3% Haste, 1% Mag Out
- Dexterity - 0.3% Dodge
- Wisdom - 0.3% Dodge, 0.2% Hit Chance, 0.7% Crit Chance
- Luck - 0.7 SP, 0.2% Critical Chance, 0.1% Hit Chance, 0.1% Haste, 0.1% Dodge, 5% Crit Modifier

**Power Caster**
- Strength - 2 AP
- Intellect - 2 SP, -1% Mag In, 0.3% Haste, 1% Mag Out
- Dexterity - 0.3% Dodge
- Wisdom - 0.3% Dodge, 0.2% Hit Chance, 0.7% Crit Chance
- Luck - 0.7 SP, 0.2% Critical Chance, 0.1% Hit Chance, 0.1% Haste, 0.1% Dodge, 5% Crit Modifier

**Hybrid**
- Strength - 2 AP, 0.4% Critical Chance
- Intellect - 2 SP, 0.3% Haste, 1% Mag Out, -1% Mag In
- Dexterity - 0.2% Hit Chance, 0.3% Haste, 0.5% Dodge
- Wisdom - 0.3% Dodge
- Luck - 0.7 AP and SP, 0.2% Critical Chance, 0.1% Hit Chance, 0.1% Haste, 0.1% Dodge, 5% Crit Modifier

**Luck Hybrid**
- Strength - 2 AP, 0.4% Critical Chance
- Intellect - 2 SP, 0.3% Haste, -1% Mag In
- Dexterity - 0.2% Hit Chance, 0.3% Haste, 0.3% Dodge
- Wisdom - 0.3% Dodge, 0.2% Hit Chance,  0.4% Crit Chance
- Luck - 0.7 AP and SP, 0.3% Critical Chance, 0.1% Hit Chance, 0.3% Haste, 0.25% Dodge, 2.5% Crit Modifier

These are however then multiplied by the efficiency value of the current level.

---
## Stat efficiency

As you increase in levels your stat efficiency decreases per stat, so the overall power increase per level is very minimal.

Formula to calculate efficiency

$$
Efficiency = \frac{1}{64 \div  16000 \times (CurrentLevel - 1 \div MaxLevel - 1)^{0.66}}\times1640 + 360
$$

[Graph for efficiency](https://www.desmos.com/calculator/lkmzantsca)

[Sheet for efficiency](https://docs.google.com/spreadsheets/d/1fKQkhkXpeDnWyyK9zgnBiJmhpBYeZL-Cr6Nm8Zyn8to/edit?gid=1414839272#gid=1414839272)

---

## Enhancements stats calculations

Formula for stat total is below:

$$
StatTotal = 12 + \frac{EnhanceLevel+EnhanceModifier-1}{MaxLevel-1}\times560
$$

[Graph for enhancement equation](https://www.desmos.com/calculator/i87afcbc9v)

Enhancement type modifier values

| Enhancement Type | Stat Total |
| ---------------- | ---------- |
| Weapon           | 0.33       |
| Class            | 0.25       |
| Helm             | 0.25       |
| Cape             | 0.20       |

Primary stat modifier values, the inaccurate ones are done by me and I am pretty sure they're correct but it's based on the values given for each enhancement and rounded to 2 DP. By adding all the modifiers they should equal 1.

| Enhancement Type     | STR   | INT   | END   | DEX   | WIS   | LUK   |
| -------------------- | ----- | ----- | ----- | ----- | ----- | ----- |
| Fighter              | 0.44  | 0.00  | 0.43  | 0.13  | 0.00  | 0.00  |
| Thief                | 0.30  | 0.00  | 0.25  | 0.45  | 0.00  | 0.00  |
| Wizard               | 0.00  | 0.50  | 0.10  | 0.00  | 0.20  | 0.20  |
| Healer               | 0.00  | 0.45  | 0.40  | 0.00  | 0.15  | 0.00  |
| Hybrid               | 0.28  | 0.27  | 0.25  | 0.20  | 0.00  | 0.00  |
| Lucky                | 0.10  | 0.10  | 0.10  | 0.10  | 0.10  | 0.50  |
| Spellbreaker         | 0.00  | 0.40  | 0.20  | 0.00  | 0.30  | 0.10  |
| Forge                | 0.25  | 0.25  | 0.00  | 0.00  | 0.00  | 0.5   |
| Anima, Clairvoyance  | 1.35  | 0.16  | -0.90 | 0.24  | 0.16  | 0.00  |
| Pneuma, Clairvoyance | 0.24  | 1.18  | -0.90 | 0.24  | 0.24  | 0.00  |
| Vim, Ether           | 0.10  | 0.00  | -0.90 | 1.31  | 0.00  | 0.50  |
| Examen, Ether        | 0.00  | 0.10  | -0.90 | 0.00  | 1.31  | 0.50  |
| Grimskull, Hearty    | -0.11 | -0.12 | 1.59  | -0.12 | -0.12 | -0.12 |
| Acheron, Depths      | 0.00  | 0.50  | 0.00  | 0.00  | 0.00  | 0.50  |

Kind of looks pointless to have this information but it's pretty much there if you would like to figure out why the member enhances are more despite the modifier being +1.  Also probably on an unrelated note but dauntless uses fighter and elysium uses wizard if it wasn't already established.


**Member version of Level 100 enhancement.**
![[Pasted image 20240624151123.png]]
$$
12 + \frac{100+5-1}{100-1}\times560 = 600.283
$$

We can then find the true values for this enhancement.

*We use the weapon modifier value to get the base stat total for this enhancement type*
`600 x 0.33 = 198` 
*We then use the primary stat modifier values for this enhancement type (Luck) to get the stat for each value*
```
198 x 0.10 = 19.8 - STR
198 x 0.10 = 19.8 - INT
198 x 0.10 = 19.8 - WIS
198 x 0.10 = 19.8 - END
198 x 0.10 = 19.8 - DEX
198 x 0.50 = 99 - LUK
```

**Non-member version of Level 100 enhancement.**

![[Pasted image 20240624151156.png]]

$$
12 + \frac{100+4-1}{100-1}\times560 = 594.626
$$

We can now find the true values for this enhancement.

*We use the weapon modifier value to get the base stat total for this enhancement type*
`595 x 0.33 = 196.35` 
*We then use the primary stat modifier values for this enhancement type (Luck) to get the stat for each value*
```
196.35 x 0.10 = 19.635 - STR
196.35 x 0.10 = 19.635 - WIS
196.35 x 0.10 = 19.635 - END
196.35 x 0.10 = 19.635 - DEX
196.35 x 0.10 = 19.635 - INT
196.35 x 0.50 = 98.175 - LUK
```

Basically if you have member you're 1.65 points better than a f2p player!!! This is heresy!!! P2W!!! I don't know for sure if aqw rounds values up/down in actual backend but like if they don't then yes that's a thing.


---

## Stat Caps

Caps for each stat below. 

- Damage Resistance: 80% (0.2 All In)
- Damage Boost: -90% (0.1 All Out)
- Physical Resistance: 80% (0.2 Phys In)
- Physical Boost: not capped
- Magical Resistance: 80% (0.2 Mag In)
- Magical Boost: has a cap, but because of weird circumstances regarding the magical damage type, it actually doesn't matter
- Healing intake: not capped (you can have negative healing intake and take damage from healing sources)
- Healing boost: unknown, pretty much irrelevant if it is or not, we just haven't been able to confirm it yet with current tools
- DoT resist: 80% (0.2 DoT In)
- DoT boost: Unknown
- Haste: 50% (1.5 Haste)

---

## Monster Secondary Stats

Assuming no other skills passives or mechanics are present Monster Secondary Stats: 
- Hit chance: 90% 
- Haste: 37.5% 
- Crit chance: 15% 
- Evasion: 10% 
- Crit Mod: 200% 
- Base auto cd: 4s 
- Base damage range: 27-33

---

## Character Secondary Stats

This is base stats without additions from stats from enhancements.

- Hit Chance: 90%
- Crit Chance: 5%
- Crit Multiplier: 150%
- Dodge Chance: 4%
- Haste: 0%
- Health: 1640*((Level-1)/99)^0.66+360
- All Ins and Outs: 100%

---
## DoT/HoT Mechanics

[Referencing some data stated here](https://sites.google.com/view/aqwadvancedmechanics/creditsreferences?authuser=0)

DoT/HoT refers to "Damage over Time" and "Heal over Time". They're effected by All out %, Mag out %, DoT out %, but not effected by Phy out %. HoTs are just DoTs but in reverse so they're all effected by the same effects. Weapon Range, % Weapon Damage and Spell/Skill damage, and dps.

**DOT/HOT Squaring**
- When any outgoing modifier, all out, phy out, mag out, is applied before the application of a DoT/HoT, it will cause the all out to be squared during the calculation.
- In a scenario where your base HoT with a fixed weapon is 144 using Bard, after applying drums and potent honour it should equate to 1.95x as your all out modifier. Your HoT should equate to 547, however 144 * 1.95 != 547 so there is obviously the effect of 1.95 being squared during the calculation to reach 547.
- It is preferred to apply your buffs before applying said HoT/DoT because if you apply your buffs after the value will not be squared during calculation and just normal.
- Applying buffs like this Buff > Dot > Buff will lead to the first buff being squared but your 2nd after the DoT will not be squared.

*Squared DoT calculation*
$$
TotalDoT = (1 + Buffs)^2 \times UnboostedDoT
$$


**Physical DoTs**
They're concerned with weapon damage and weapon dps. First you have to calculate the original HoT/DoT without buffs by dividing by the All outs, next divide by the weapon DPS.
$$
Physical DoT = \frac{CurrentValue}{buffs^2}\div WeaponDPS
$$

**Magical DoTs**
$$
Factor = 360 + (\frac{Weapon Enh Level - 1}{MaxLevel - 1})^{0.66}\times1640
$$
$$
WeaponDPS = (\frac{Factor}{2000}\times 0.85 \times 100) + 0.1(Total AP)
$$
$$
SpellDPS = (\frac{Factor}{2000}\times 0.85 \times 100) + 0.1(Total SP)
$$
*If the DoT is considered refreshable*
$$
WeaponDamage = WeaponDPS\times2
$$
$$
SpellDamage = SpellDPS\times2
$$

[More equations referencing DoTs here](https://sites.google.com/view/aqwadvancedmechanics/home/dothot-formulae/dot-hot-equations/collection-of-dot-equations?authuser=0) 

**Dynamic and Static stats**

Stats that are dynamic means it’ll calculate per tick, and static meaning on initial application.

- all out - dynamic & static
- all in - dynamic 
- mag out - dynamic
- mag in - x
- phys out - x
- phys in - x
- dot out - static
- dot in - dynamic

*Squaring demonstration below*
[Post is here](https://www.reddit.com/r/AQW/comments/1iiitgx/squaring_demonstration/)

---
## Chronos and their weird intricacies

*Majority of this information is from mole, slgma and other smart people in the community*

Usually what defines a chrono class to other classes is that they can do big boy numbers through the use of a recorded nuke in the span of 10 seconds. All these chronos do this through the use of a variation of the “rift” skill like temporal rift, or chaos rift. They then have some form of “rift collapse” where they basically just consume all their rifts and do a nuke based on the damage they've done in these 10 seconds.

Rifts at their base do two sorts of things, it controls the nuke multiplier through the amount of rift stacks. And it also starts the damage recording from the very start of the first rift being applied.

All rifts stack to 4 however, each rift added will also increase the amount of damage you do from your nuke. Below is the multipliers at each stack:
- 1 Stack = 0.5
- 2 Stack = 0.7
- 3 Stack = 1.0
- 4 Stack and above = 1.5

For recording damage, it only records the most recent 10 seconds. If your nuke exceeds 10 seconds, it will not add any extra damage and just waste time. [Refer to this amazing animation made by SLGMA for an example of how the damage changes if you exceed 10 seconds.](https://streamable.com/msrl8) Do understand that the damage recorded during this time period doesn’t take into outgoing modifiers. So if you did 5000 with 1.2 all out, it does 5000/1.2 and that will be your raw damage that is recorded. However, it does take into account weapon boosts and crits.

The total damage done during that timespan is then multiplied by any additional all-out, mag-out, phy-out, dot-out (if nuke is dot) buffs, then multiplied by the rift modifiers below. I'm going to refer to the [[Shadow Stalker of Time#Extra information|SSOT Guide]] as it provides an example of how you'd calculate the final "damage recorded". Divide the damage recorded by any outgoing damage modifiers **BEFORE** putting in the multiplier for nukes, as nukes record the raw damage unaffected by outgoing damage modifiers. The only modifier that is considered to be part of the raw damage would be crit modifiers.

Calendar Classes' Rift Mods (post-coefficient changes + post-rift multipliers) at 4 stacks:
- CDK: 2.17
- Chrono Commander: 1.95
- Chrono Corruptor: 1.5
- Chronomancer: 1.5
- TCM: 1.95
- IC: 2.7
- SSoT: 0.3
- TimeKiller: 1.5
- Nechronomancer: 0.45
- CSS: 0.45

The values below are the coefficients, these are multiplied by the 4 stack rift multiplier to reach the modifiers above. 

Calendar Classes' coefficients:
- CDK: 1.45
- Chrono Commander: 1.3
- Chrono Corruptor: 1
- Chronomancer: 1
- TCM: 1.3
- IC: 1.8
- SSOT: 0.2
- TK: 1
- Nechronomancer:  0.3
- CSS: 0.3

You can utilise this information to understand more about your chrono, especially in bossing situations where you are in a party, you can use this information to calculate the bare minimum amount of rifts required to kill a boss and avoid wasting extra time stacking for extra farming efficiency.

It’s good to know that damage boosts scale even higher with chronos, the 75% + 35% combo is especially deadly at reaching extra high nukes.

Example with IC:
1 Stack: 1.8 * 0.5 = 0.9
2 Stack: 1.8 * 0.7 = 1.26
3 Stack: 1.8 * 1 = 1.8
4 Stack: 1.8 * 1.5 = 2.7

If you have a sort of idea of what sort of damage you're dealing at different stages of your nuke, you will not need to fully stack to deal great amounts of damage with certain classes that have high coefficients.

I’ve created a [google sheet](https://docs.google.com/spreadsheets/d/1Na6TZo-2t053aG1lz2qJtZ8EtZvfiNqh1wxW-Tlv39Q/edit?usp=sharing) if you’d like to test out numbers for nukes on chronos. You’d have to input damage, outgoing modifiers, crit modifiers, and gear boosts. But the rest of the sheet should more or less calculate itself.

---
## Skill Functions

Certain skills have different functions for damage. Screenshot below goes over some of the functions. Check the spreadsheet for a more comprehensive list.

![](https://media.discordapp.net/attachments/476856315554037771/948008719768240208/Screenshot_2022-02-28-22-15-43-34.jpg?ex=66a391ab&is=66a2402b&hm=61094e79d8ca85be2ea42d62e83a714d03570f22bc917d7ebba4c3beac946f84&)

This very cool [spreadsheet](https://docs.google.com/spreadsheets/d/1WeO37yc7UnPXCya4iiAgBZbSxpLH8nSZiPoOmWuGSuk/edit?gid=101348511#gid=101348511) (idk who’s the owner) holds some of the functions used for each class. I don’t think it’s fully completed but if you want to be a nerd the stuff exist yes. Found some inconsistencies though, for example when I checked css it used a 1.15 Hours1 damage function but spreadsheet uses 1.05. This is probably due to the fact CSS was changed on March 8th 2024, either way it’s still a decent thing to know.

(I will try make an updated version of the above spreadsheet [here](https://docs.google.com/spreadsheets/d/1wU6JlyrK_jYn5mVAzrLI4pRA4UM8LgY715kKU2U1vbQ/edit?gid=101348511#gid=101348511) but I just started so it’ll be slow)

Chrono2 follows this formula and is only for chronos

$$
RecordedDamageMod = RiftMod \times Coefficient \times Outgoing Modifiers \times Incoming Modifiers \times CritMod
$$

Then the `RecordedDamageMod` is multiplied by the Raw damage, without outgoing or incoming modifiers.


---


## Other Mechanics

**%ALL Boosted Weapons effect heals**
Primarily for support classes, running an %all boosted weapon will boost your heals significantly. This doesn't work with tagged weapons.

**Miss chance takes priority over dodge chance**
When fighting an enemy, your miss chance rolls first and then the dodge chance rolls. So if you have a +100% hit chance then you will not miss, but if you stoop below, you will begin to notice that you will start missing rather than them dodging your hit.

**Crit chance being dependent on Dodge chance**
Pretty much if your enemy has a high dodge chance, your crit chance also increases, you would assume it's independent but no. All rolls are calculated on the same hit, rolling a crit on an enemy with 80% dodge rate implies that you have already hit a high roll so are more likely to have went past the dodge threshold.
$$
TrueCritChance = Your Crit Chance +Enemy Dodge Chance
$$

**Different damage Boosts stacking**
This is a known mechanic in the community but I'll add it to be thorough. Damage boosts can stack multiplicatively if they are not the same tag. So %All + %All will not work, and only the highest damage boost item will be the final boost. But having %All + %Human will make them stack multiplicatively.

`51% (1.51) * 50% (1.5) = 126%`
`75% (1.75) * 35% (1.35) = 136%`

**Quest Reward drop manipulation**
![[Pasted image 20240707230129.png]]
If a quest states **You will receive one of the following items**, by accepting one of the drops and having it in your invetory you make the other drops guaranteed. This is a useful mechanic for certain farms, in this case the uni 34 can be obtained much easier.

