---
dg-publish: true
dg-metatags:
  og:site_name: AQW Hub
  og:title: Stats and Misc Guides
  og:description: Player stats and other miscellaneous information 
  description: Player stats and other miscellaneous information 
  og:image: https://cdn.discordapp.com/icons/203072919616618496/f98d38c50b06972678eaaa1aa2c0cedf.png
---
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

**Wisdom**
- Increases Dodge to all stat models, increases Hit and Critical change to caster and hybrid luck models

**Endurance**
- Increases health to all stat models

**Luck**
- Increases Hit, Haste, Dodge, Critical Chance, Critical Damage, AP to melee classes and SP to caster classes, hybrid get both AP/SP.

## Stat Models

Stat models provide different modifiers for specific stats, for example having 30 intellect on the stat model Tank Melee will have a different effect on a class with the stat model Offensive Caster. You can view the stat model of your class through Character > Stat Overview. 

Any values with a * preceding it will have +- 0.0000000001 Deviation per level, this will barely not matter but I'm just saying it exists according to math.

**Tank Melee**
- Strength - 2 AP, * 0.4% Critical Chance 
- Intellect - 2 SP, -1% Mag In
- Dexterity - * 0.2% Hit Chance, * 0.3% Haste, * 0.3% Dodge
- Wisdom - * 0.3% Dodge, 
- Luck - 0.7 AP, * 0.2% Critical Chance, * 0.1% Hit Chance, * 0.1% Haste, * 0.1% Dodge, * 5% Crit Modifier,  

**Dodge Melee**
- Strength - 2 AP, * 0.4% Critical Chance 
- Intellect - 2 SP, -1% Mag In
- Dexterity - * 0.2% Hit Chance, * 0.5% Haste, * 0.5% Dodge
- Wisdom - * 0.3% Dodge, 
- Luck - 0.7 AP, * 0.2% Critical Chance, * 0.1% Hit Chance, * 0.1% Haste, * 0.1% Dodge, * 5% Crit Modifier,  

**Power Melee**
- Strength - 2 AP, * 0.7% Critical Chance 
- Intellect - 2 SP, -1% Mag In
- Dexterity - * 0.2% Hit Chance, * 0.5% Haste, * 0.5% Dodge
- Wisdom - * 0.3% Dodge, 
- Luck - 0.7 AP, * 0.2% Critical Chance, * 0.1% Hit Chance, * 0.1% Haste, * 0.1% Dodge, * 5% Crit Modifier,  

**Defensive Caster**
- Strength - 2 AP
- Intellect - 2 SP, -1% Mag In, * 0.5% Haste, * 1% Mag Out
- Dexterity - * 0.3% Dodge
- Wisdom - * 0.3% Dodge, * 0.2% Hit Chance, * 0.4% Crit Chance
- Luck - 0.7 SP, * 0.2% Critical Chance, * 0.1% Hit Chance, * 0.1% Haste, * 0.1% Dodge, * 5% Crit Modifier

**Offensive Caster**
- Strength - 2 AP
- Intellect - 2 SP, -1% Mag In, * 0.3% Haste, * 1% Mag Out
- Dexterity - * 0.3% Dodge
- Wisdom - * 0.3% Dodge, * 0.2% Hit Chance, * 0.7% Crit Chance
- Luck - 0.7 SP, * 0.2% Critical Chance, * 0.1% Hit Chance, * 0.1% Haste, * 0.1% Dodge, * 5% Crit Modifier

**Power Caster**
- Strength - 2 AP
- Intellect - 2 SP, -1% Mag In, * 0.3% Haste, * 1% Mag Out
- Dexterity - * 0.3% Dodge
- Wisdom - * 0.3% Dodge, * 0.2% Hit Chance, * 0.7% Crit Chance
- Luck - 0.7 SP, * 0.2% Critical Chance, * 0.1% Hit Chance, * 0.1% Haste, * 0.1% Dodge, * 5% Crit Modifier

**Hybrid**
- Strength - 2 AP, * 0.4% Critical Chance
- Intellect - 2 SP, * 0.3% Haste, * 1% Mag Out, -1% Mag In
- Dexterity - * 0.2% Hit Chance, * 0.3% Haste, * 0.5% Dodge
- Wisdom - * 0.3% Dodge
- Luck - 0.7 AP and SP, * 0.2% Critical Chance, * 0.1% Hit Chance, * 0.1% Haste, * 0.1% Dodge, * 5% Crit Modifier

**Luck Hybrid**
- Strength - 2 AP, * 0.4% Critical Chance
- Intellect - 2 SP, * 0.3% Haste, -1% Mag In
- Dexterity - * 0.2% Hit Chance, * 0.3% Haste, * 0.3% Dodge
- Wisdom - * 0.3% Dodge, * 0.2% Hit Chance,  * 0.4% Crit Chance
- Luck - 0.7 AP and SP, * 0.3% Critical Chance, * 0.1% Hit Chance, * 0.3% Haste, * 0.25% Dodge, * 2.5% Crit Modifier

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

Primary stat modifier values

| Enhancement Type | STR  | INT  | END  | DEX  | WIS  | LUK  |
| ---------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| Fighter          | 0.44 | 0    | 0.43 | 0.13 | 0    | 0    |
| Thief            | 0.30 | 0    | 0.25 | 0.45 | 0.0  | 0    |
| Wizard           | 0    | 0.50 | 0.10 | 0    | 0.20 | 0.20 |
| Healer           | 0    | 0.45 | 0.40 | 0    | 0.15 | 0.00 |
| Hybird           | 0.28 | 0.27 | 0.25 | 0.20 | 0    | 0    |
| Lucky            | 0.10 | 0.10 | 0.10 | 0.10 | 0.10 | 0.50 |
| Spellbreaker     | 0.00 | 0.40 | 0.20 | 0.00 | 0.30 | 0.10 |

Kind of looks pointless to have this information but it's pretty much there if you would like to figure out why the member enhances are more despite the modifier being +1. 


**Non-member version of Level 100 enhancement.**
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

Basically if you have member you're 1.8 points better than a f2p player!!! This is heresy!!! P2W!!! I don't know for sure if aqw rounds values up/down in actual backend but like if they don't then yes that's a thing.

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

## DoT/HoT Mechanics

[Referencing some data stated here](https://sites.google.com/view/aqwadvancedmechanics/creditsreferences?authuser=0)

DoT/HoT refers to "Damage over Time" and "Heal over Time". They're effected by All out %, Mag out % but not effected by Phy out %. HoTs are just DoTs but in reverse so they're all effected by the same effects. Weapon Range, % Weapon Damage and Spell/Skill damage, and dps.

**DOT/HOT Squaring**
- When any outgoing modifier, all out, phy out, mag out, is applied before the application of a DoT/HoT, it will cause the all out to be squared during the calculation.
- In a scenario where your base HoT with a fixed weapon is 144 using Bard, after applying drums and potent honour it should equate to 1.95x as your all out modifier. Your HoT should equate to 547, however 144 * 1.95 != 547 so there is obviously the effect of 1.95 being squared during the calculation to reach 547.
- It is preferred to apply your buffs before applying said HoT/DoT because if you apply your buffs after the value will not be squared during calculation and just normal.
- Applying buffs like this Buff > Dot > Buff will lead to the first buff being squared but your 2nd after the DoT will not be squared.

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
*If the DoT is considered refreshable,*
$$
WeaponDamage = WeaponDPS\times2
$$
$$
SpellDamage = SpellDPS\times2
$$

[More equations referencing DoTs here](https://sites.google.com/view/aqwadvancedmechanics/home/dothot-formulae/dot-hot-equations/collection-of-dot-equations?authuser=0) 

---


## Other Mechanics

**%ALL Boosted Weapons effect heals**
Primarily for support classes, running an %all boosted weapon will boost your heals significantly. This doesn't work with tagged weapons.

**Miss chance takes priority over dodge chance**
When fighting an enemy, your miss chance rolls first and then the dodge chance rolls. So if you have a +100% hit chance then you will not miss, but if you stoop below, you will begin to notice that you will start missing rather than them dodging your hit.

**Crit chance being dependent on Dodge chance**
Pretty much if your enemy has a high dodge chance, your crit chance also increases, you would assume it's independent but no.
$$
TrueCritChance = Your Crit Chance +Enemy Dodge Chance
$$
