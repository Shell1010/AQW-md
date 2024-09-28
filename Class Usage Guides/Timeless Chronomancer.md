---
dg-publish: true
dg-metatags:
  og:site_name: AQW Hub
  og:title: Timeless Chronomancer
  og:description: Class usage guide for TCM
  description: Class usage guide for TCM
  og:image: https://bigrat.monster/media/bigrat.jpg
---
Timeless chronomancer (TCM) is possibly one of the more complex chronos to use, mainly due to the fact it has multiple consumables which will prioritise different sorts of playstyles.

Since this is the case, I will add a separate guide per hourglass for the purposes of being thorough:

```dataview
TABLE 
FROM #tcm
```

Outside of hourglasses there are other consumables, for TCM they are known as corruptions, and it is important to note that Underworld chronomancer’s (UCM) timepiece’s also apply for TCM. Due to the fact there are a lot of consumable’s to cover I’m going to try list what changes they do in the skills overview section.

With thanks to the following for extra information:
- FireWizardGamer ([their guide](https://docs.google.com/document/d/1NW-HEycuuIPW6nmb9eP1i_Jb-8dYiDcmW6L6_mNe96w/edit))
- SLGMA ([their guide](https://docs.google.com/document/d/1pHEYDB5JM2qSBFYwVs6Hkj17x24TElB1mtuQUyidv18/edit))

*DISCLAIMER: I do not personally own UCM, so the consumables specific to UCM are not really tested so I cannot give any additional information than what is already given by SLGMA and others. If you’d like to test these yourself then that’ll be great.*

---
## Skills Overview

![[Pasted image 20240715151723.png]]

- **Corrupted Sand Strike - Auto Attack**
	- 100% Weapon Damage (Physical) / 1 AP2
	- Short Range Attack
	- 2 second cooldown, 1 seconds at max haste
	- Single Target
	- **Infinite Corruption - TCM**
		- Applies Infinity Rend
		- DoT that stacks to 15
	- **Timepiece of Madness - UCM**
		- Applies Mad, increasing all out by 3%
		- At 5 Stacks of Mad applies Eternal
			- Increases critical chance by 80% and reduces all out by 30%

This is your auto attack which tends to do the most damage outside of your nuke, this will be what mainly feeds into your nukes recorded damage. 

---

![[Pasted image 20240715152710.png]]
- **Sand Rift**
	- Hybrid Damage / 0.1  APSP2
	- Short Range Attack
	- 2.5 second cooldown, 1.25 seconds at max haste
	- Uses 15 mana
	- Single Target
	- Applies temporal rift, stacks to 4
		- Used as the nuke’s (5) inherent multiplier
			- 1 Stack = 0.5
			- 2 Stack = 0.7
			- 3 Stack = 1.0
			- 4 Stack and above = 1.5
		- The first temporal rift is used to start the damage recording over the most recent 10 seconds.
		- Consumed by Temporal Collapse (5)

This skill is used to stack temporal rifts for your nuke as well as starting the recording for the damage feed into the nuke. It is meant to be used a lot so that you can stack your rifts for the eventual nuke.

---

![[Pasted image 20240715153911.png]]
- **Hourglass Inversion**
	- Hybrid Heal / -3 Spell1
	- Infinite Range Attack
	- 8 second cooldown, 4 seconds at max haste
	- Single Target
	- Heals based on the stacks of temporal rifts from your 2 skill, consumes rift stacks
	- **Infinite Corruption - TCM**
		- Applies HoT for 20 seconds

This skill is usually used after your nukes in order to heal, using the base class rotation. Or if you get hit hard you may have to just heal instead of nuking to avoid death. 

With infinite corruption it is useful to use this after your 4 to increase your all out and to make sure your HoT is squared. Refer to [[Stats & Misc#DoT/HoT Mechanics|DoT and HoT mechanics]] section.

---

![[Pasted image 20240715155040.png]]
- **Corruption Through Time**
	- Hybrid Status Skill
	- Long Range Attack
	- 6 second cooldown, 3 seconds at max haste
	- Uses 20 mana
	- Single target
	- Applies corruption through time, 20% increase to all out
	- **Entropic Corruption - TCM**
		- Entropic Harm, increases all in to yourself by +150%
		- Entropic Mana, increases haste by 30%, reduces mana costs by -50%
		- Entropic Power, increases all out by 100%
		- Focus for 3 seconds, enemy attacks you
	- **Foresee Corruption - TCM**
		- Applies Foresee for 150 seconds
		- Using **Foresee Corruption** again, replaces Foresee with Seer for 20 seconds
		- Using Corruption Through Time (4) again, replaces Seer with Change the Future. This applies the following for 5 seconds:
			- Decrease your all in by 80%
			- increasing dodge, haste, hit chance, damage, and crit damaage by 100%
	- **Timepiece of Madness - UCM**
		- Applies Potential for 20 seconds. Increases your hit chance by 20% for 20 seconds. This aura has a CD of 20 seconds.
	- **Timepiece of Inevitability - UCM**
		- Applies Inevitable Corruption. Increases all out and haste by 12% for 20 seconds
		- Using **Timepiece of Inevitability** again while Inevitable Corruption is active applies Snap to the enemy. Deals high damage after a short delay.
	- **Timepiece of Pestilence - UCM**
		- Applies Infectious Air, decreasing enemy all in by -20% for 10 seconds, stacks to 3, consumed by Temporal Collapse (5).
		- Increases your own all-in by 100% for 10 seconds
		- Applies light DoT to enemy
		- Applies decay to enemy, to prevent them healing

This skill is usually what you start every rotation with due to the buffs it applies. It also activates majority of the consumables buffs/debuffs so it is integral to the use of the class. 

---

![[Pasted image 20240715162104.png]]
- **Temporal Collapse**
	- Magical Damage / 1.3 Chrono2
	- Short Range Attack
	- 15 second cooldown, 7.5 seconds at max haste
	- Uses 35 mana
	- Single target
	- Deals damage based on the amount of rifts stacked from your 2 skill and the recorded damage in the most recent 10 seconds

Used to just nuke hit hard and big boom. Use once you have 4 rifts, though it is okay to use it with 3 stacks as it also provides decent ish damage.

---

## Consumables

While I have specified what the non hourglass consumables do in each skill, here I’ll reiterate and explain the general use for each consumable.

---
### Entropic Corruption

![[Pasted image 20240715181254.png]]
- When using 4 while active, applies the following:
	- Entropic Mana: Increase Mana reduction by 50%, Haste by 30%
	- Entropic Harm: Increases all in to self by 150%
	- Entropic Power: Increases all out by 100%

Big damage, big risks, great in parties due to boost scaling. Often used alongside Hourglass of Power.

---
### Infinite Corruption

![[Pasted image 20240715182306.png]]
- While this is active it applies the following:
	- Auto Attack applies a DoT that stacks to 15 and lasts 40 seconds
	- Hourglass Inversion (3) applies a HoT for 20 seconds

Often used with Hourglassof Transience if you do not have dauntless. Due to the fact the HoT output is kinda low ish, it is recommended to square the output. So utilise Corruption Through Time’s (4) 20% all out buff and then apply the HoT.

---
### Foresee Corruption

![[Pasted image 20240715182701.png]]
- While this is active, using Corruption Through Time (4) applies the following:
	- The initial use of 4 applies Foresee for 150 seconds
	- Using the consumable (6) again while Foresee is active will then replace it with Seer
	- While Seer is active using Corruption Through Time (4) again will apply Change the Future
		- This reduces all in by 80%
		- 100% Dodge, Haste, Hit chance, Crit Damage, and all out increase
		- Taunt

Generally this allows a slow but large nuke, but it is often much better to use the other consumables due to the slow overall dps. This only procs every 40 or so seconds.

---
### Timepiece of Inevitability

![[Pasted image 20240715183833.png]]
- While this is active, using Corruption Through Time (4) applies the following:
	- Applies Inevitable Corruption, Increases your all out and haste by 12% for 20 seconds
	- Using the consumable (6) while this is active applies Snap, dealing high damage after a short delay

I can’t account for the playstyle or use cases myself for the timepieces, the information below is based on SLGMA’s guide.

Refer to his guide [here](https://docs.google.com/document/d/1pHEYDB5JM2qSBFYwVs6Hkj17x24TElB1mtuQUyidv18/edit).

Used with Hourglass of Power + Inevitability due to the extra damage feeded in from snap. For overall higher nukes. There is a complex Hourglass of Transcience rotation with this also.

---
### Timepiece of Madness

![[Pasted image 20240715185417.png]]
- While this is active it applies the following:
	- Auto Attack applies Mad, increasing all out by 3%
		- Once at 5 stacks of Mad, you become eternal
		- Increasing Critical Chance by 80% and decreasing all out by 30%
	- Corruption Through Time (4) applies Potential, increasing hit chance by 20% for seconds

With Hourglass of Power + Madness, the idea is to line up your nukes with the 5 stacks of Mad to deal big funny numbers. There is a Transcience + Madness rotation but you are required to manage your HP well to avoid accidentally dying.

---
### Timepiece of Pestilence

![[Pasted image 20240715190314.png]]
- While this is active, Corruption Through Time (4) applies the following:
	- Infectious Air, increasing damage takes by 20% and stacks to 3 and lasts 10 seconds. Is consumed by Temporal Collapse (5).
	- All In is increased by 100% for 10 seconds
	- Applies a light DoT to your opponent
	- Applies Decay to your opponent

General idea with this timepeice is to gather stacks while nuking. This reduces your own defense so it can be quite risky.

---
## Enhancements

| Situation          | Enhancements                                   | Rating | Extra Information                               |
| ------------------ | ---------------------------------------------- | ------ | ----------------------------------------------- |
| Solo               | Dauntless/Anima/Vainglory or Lament            | 9/10   | Good for all out damage.                        |
| Solo (alternative) | Lacerate or Valiance/Anima/Vainglory or Lament | 8/10   | Can be swapped for Lament for more crit chance. |

There are no farming alternatives here, if you’re ever going to farm with this class you’re going to farm a boss to which you’d use either example above. Don’t use this to farm mobs.

---
## Gameplay/Combos

This class has many consumables but generally with this you will not necessarily deviate much from the basic 4 rift combo, though depends on the situation. 

**Basic 4 Rift Rotation**
4-2-2-2-4-2-5-3

Sometimes it’s just better to just pot and run [feli](http://aqwwiki.wikidot.com/felicitous-philtre) if you’re not using a corruption/timepiece. Entropy works too but you also lose some survivability.

---
## Extra Information

Refer to the [[Stats & Misc|Chrono Section]] for the Stats & Misc area for general information, this will be specified for TCM. This section is to tell you how to optimise damage with TCM, I will go over the base class in this section as well as under the effects of particular consumables if they effect the class nukes in any way.

Chronos like TCM are literally funny number machine due to the fact they utilise so many buffs together the damage for nukes is exponential. Utilising pots and 

The base class takes in the following buffs into the nuke:
- All Out
- Mag Out
- Crit Modifier

TCM’s coefficient is 1.3

Rifts multiplier stacks like this:
- 1 Stack = 0.5
- 2 Stack = 0.7
- 3 Stack = 1.0
- 4 Stack and above = 1.5

The base mag out for TCM is at 32% so 1.32

The base crit mod for TCM is at 260% so 2.6

All out is at 1.2 or 20% due to the fact you’re most likely going to be nuking while Corruption Through Time (4) effect is active.

So our final equation looks like this (this assumes you crit)

$$
RecordedDamageMod = RiftMulti \times Coefficient \times AllOutBuffs \times MagOutBuffs \times CritMod
$$

With the base class this will be at 4 rifts:
`1.5 (4 rifts) x 1.3 (coefficient) x 1.2 (all out buffs) x 1.32 (mag out buffs) x 2.6 (crit mod buffs) = 8.031`

All Out is at 1.2 since you get 20% buff from using Corruption Through Time (4). And 99% of scenarios you’re going to have 4 active when you nuke

Damage done during the most recent 10 seconds from the first temporal rift applying, will then be multiplied by the value above at 4 rifts, assuming you are using the base class.

While this is technically the most damage you can do without the use of corruptions/pots using the base class, you can shorten your nuke cycles by using less rifts, however your damage will be much less effective. Here are the multipliers at different stacks (non-crit in brackets):
- 4 Rifts (1.5) - 8.03 (3.09)
- 3 Rifts (1) - 5.35 (2.06)
- 2 Rifts (0.7) - 3.75 (1.44)
- 1 Rift (0.5) - 2.68 (1.03)

It is recommended to nuke at 3 stacks while you still have mostly effective nuke multipliers, . This knowledge can be useful when trying to quickly farm bosses and prevent you from overkilling the boss.

With the information  established above, I will now state the differences in nukes with some of the different corruptions.

**Entropic Corruption**
Gives an All Out buff of 100% and a haste buff of 30% so you can feed in more damage. The all out buff total is going to be 120%, which is big so you’ll see some significant changes in the nuke multiplier (non-crit in brackets).
- 4 Rifts (1.5) - 14.72 (5.66)
- 3 Rifts (1) - 9.82 (3.78)
- 2 Rifts (0.7) - 6.87 (2.64)
- 1 Rift (0.5) - 4.91 (1.89)

I’m pretty sure you see the numbers above but just to reiterate, if you did 30k damage in 10 seconds (you’ll do a lot more trust me), it would cause the final nuke to do 441k worth of damage on crit. Supports with this class scale so well it’s crazy.

**Foresee Corruption**
This one gives a multitude of buffs during the Change The Future aura, it applies 100% to Dodge, Haste, Hit chance, Crit Damage, and all out increase. The main two we’re interested in is the 100% to all out and 100% to crit damage (crit mod). This’ll lead 120% all out and 360% crit multi, very big improvements, though this can only be accessed every 40 seconds.
- 4 Rifts (1.5) - 20.39 (5.66)
- 3 Rifts (1) - 13.59 (3.78)
- 2 Rifts (0.7) - 9.51 (2.64)
- 1 Rift (0.5) - 6.80 (1.89)

**Felicitous Philtre**
A potion that grants 50% more luck, pretty great on this chrono due to the fact it applies to the damage you feed in and the actual nuke too. Numbers may vary but should be around the same.
![[Pasted image 20240717012630.png]]
This leads to a 315% crit mod, a boost in other areas but they don’t necessarily apply to our nuke.
- 4 Rifts (1.5) - 9.73 (3.09)
- 3 Rifts (1) - 6.49 (2.06)
- 2 Rifts (0.7) - 4.54 (1.44)
- 1 Rift (0.5) - 3.24 (1.03)
