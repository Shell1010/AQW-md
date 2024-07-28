---
dg-publish: true
dg-metatags:
  og:site_name: AQW Hub
  og:title: Chronomancer Prime
  og:description: Class Usage guide for CMP
  description: Class Usage guide for CMP
  og:image: https://bigrat.monster/media/bigrat.jpg
---
Possibly one of the easiest chronos to use with great overall output. Short nuke cycles with high damage, good for majority of game content, making it a great first pick chronomancer.

Thank you to the following people for providing me with information:
- FurianX2
- Milenius

## Skills Overview

![[Pasted image 20240728172830.png]]
- **Temporal Strike**
	- 60% Hybrid Damage / 0.6 APSP2
	- Short Range Attack
	- 1.5 second cooldown, 0.75 at max haste
	- Single target
	- Stacks temporal rift with each strike
	- Used as the nuke's inherent multiplier
		- 1 Stack = 0.5
		- 2 Stack = 0.7
		- 3 Stack = 1.0
		- 4 Stack and above = 1.5
	- The first temporal rift is used to start the damage recording over the most recent 10 seconds.

Short cooldowns, so spam this for stacking rifts quickly. Used to also start the recording for your damage feeds into the nuke. 

Manage the amount of rifts you use depending on the HP of the enemy.

---
*I usually take images from the wiki, for some reason they didn’t crop it.*
![[Pasted image 20240728175022.png]]
- **Rift Inversion**
	- 70% Hybrid Heal / 0.7 Spell1
	- 12 second cooldown, 6 seconds at max haste
	- Single target
	- Heals based on amount of temporal rifts
	- Increases haste by 15% for 6 seconds
	- Always crits

Used as a heal skill, consumes your stacks of temporal rifts. This also provides you with additional haste so depending on your build you may start with this.

---

![[Pasted image 20240728175355.png]]
- **Rift Collapse**
	- Hybrid Damage / 1 Chrono2
	- Long Range Attack
	- 12 second cooldown, 6 seconds with max haste
	- Scales higher the more rifts you have, but maxes at 4
	- 80% chance to crit (basically guaranteed with base crit)

Uses up your stacks of temporal rifts and nukes, fun skill.

---

![[Pasted image 20240728175554.png]]
- **Rift Burn**
	- Magical Status skill
	- Short Range Attack
	- 12 second cooldown, 6 seconds with max haste
	- Single target
	- Applies a DoT
	- Reduces their dodge by 15%

Reduces enemy dodge, mainly so your nuke doesn’t end up missing.

---

## Enhancements

| Situation            | Enhancements              | Rating | Extra Information                                                                            |
| -------------------- | ------------------------- | ------ | -------------------------------------------------------------------------------------------- |
| Damage               | Dauntless/Anima/Vainglory | 9/10   | Fast haste, utilise 5 to make sure you don’t miss. Drop 3 due to already fat haste buff.     |
| Damage (alternative) | Lacerate/Anima/Vainglory  | 8/10   | Due to lacerate decreasing enemy dodge, you don’t need to use 5. Utilise 3 for a haste buff. |

---
## Gameplay/Combos

Due to the simplicity of the skills the class doesn’t necessarily require you to do much. You just need to know when to use either 5 or 3. You should also manage the amount of stacks of temporal rift you have, as sometimes the boss doesn’t require you to stack to 4 due to it’s lack of HP.

When using dauntless or having supports:
- Avoid using 3 due to the fact you have a haste buff
- 5 2 2 2 2 4
- Reduce the amount of 2 if needed

When using lacerate:
- Optional use of 5 due to the fact it already reduces dodge. But adds some DoT damage.
- (5) 3 2 2 2 2 4
- Reduce the amount of 2 if needed

You can stack upto 7 rifts before the nuke feed reaches 10 seconds.

---
## Extra Information

I don’t have the class myself so there’s no practical testing.

CMP’s Coefficient is 1

The nuke takes the following outgoing modifiers into the nuke:
- All Out
- Mag Out
- Phy Out
- Crit Modifier

Rifts multiplier stacks like this:
- 1 Stack = 0.5
- 2 Stack = 0.7
- 3 Stack = 1.0
- 4 Stack and above = 1.5

Final equation for the nuke multiplier would be this.

$$
RecordedDamaageMod = RiftMulti \times Coefficient \times AllOut \times MagOut \times PhyOut \times CritMod
$$

