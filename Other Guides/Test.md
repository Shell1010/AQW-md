---
dg-publish: true
dg-metatags:
  og:site_name: AQW Hub
  og:title: Secret Test
  og:description: Player stats and other miscellaneous information
  description: Player stats and other miscellaneous information
  og:image: https://bigrat.monster/media/bigrat.jpg
---

<div class="wiki-container">

---

## Quick Navigation
* [Mana Models](#mana-models)
* [Primary Stats & Base Stats](#primary-stats)
* [Damage Types & DoT Squaring](#damage-types)
* [Combat Math & Skills](#combat-math)
* [Auras & Instancing](#auras)
* [Chronomancers & Rift Math](#chronomancers)
* [Sources & Enemy Stat Sheets](#sources)

---

## 1. Introduction

Hewwo, I will attempt to do a breakdown of the underlying logic for AQW. Over the years, due to the devs spaghetti code and player discovery, the game has evolved far more than just cute fashion game. This guide is specifically made for the curious, the min-maxxers, and veterans who want to deeply understand the mechanics of the game beyond just "button mash to win".

If you are looking for a class guide tutorial, this is not for you. Most resources will tell you what to equip, but this resource will hopefully explain the "why" behind such a decision. I'll try to keep things digestible but some things are just hard to explain so I'll try to provide some examples.

AQW is known to be a very opaque game when it comes to mechanics. Nothing is very clear, the in-game UI isn't always truthful, descriptions provided by devs aren't always true, there's also barely any actual math shown to the player. This kind of thinking has led to the community paying no mind to mechanics or intricacies regarding the game.

The way the information in this guide is obtained is a culmination of years of community nerding. It's not really a one person effort, but all pretty much stuck to two main ways of verifying information. The first is just plain old rigorous experimental testing. This is just isolating a particular variable and reversing calculations, it's pretty much the foundation of our testing and how we determine things like damage functions, and skill coefficients. But this can be used for other things like stats too. The other way we did it, is through packet sniffing. This is mostly for heavily obscured mechanics that are often invisible to the player, it helps us understand how the game works in terms of order of execution, gives us raw data hidden to the player, and also helps us find aura related behaviours.

Anyway, I just wanted to state the methods we used to gather information.

### Sources & Methods

* [Scribe](https://github.com/Shell1010/Scribe)
* [jpexs-decompiler](https://github.com/jindrapetrik/jpexs-decompiler)
* [AQW-Dex](https://aqwhub.com/aqwdex)
* [AQW Hub](https://aqwhub.com)
* [My Discord server](https://discord.gg/unubuPvJ3F)

---

<h2 id="mana-models">2. Mana Regeneration Models</h2>

### Passive Mana Regeneration

All classes regain mana passively over time. In combat, you passively regenerate 3 mana every 9 seconds. No other factors influence this.

Out of combat, you passively regenerate 15% of your max HP and 15 mana every 6 seconds.

When resting, you regenerate 15% of your max HP and 15 mana every second.

### Mana Regen Models

I personally barely know about this topic in general, it's like the one part of AQW I haven't really delved into because I thought it was boring (personally). Anyway I'll literally be stealing from mole ig. I would like to make some changes though based on my own knowledge.

One thing I will mention is that the class overview may often describe specific things like Auras or Skills that give the player mana back. This is not a result of the model itself, but rather a property of the skill/aura.

Rest I stole from that site. See [sources](#sources).

#### Warrior

* Classes gain mana when they:

* * Strike an enemy in combat (more effective on crits)
* * Are struck by an enemy in combat

Warrior mana model only regenerates mana from positive hits using the class's auto attack. 6 mana is returned on noncrits, and 9 mana is returned on crits. As well, 3 mana is returned whenever the class is struck by an enemy for positive damage.

#### Mage

* Classes gain mana from all hits landed in combat, and especially on crits. The amount depends on damage relative to their own HP total.

Mage mana model regenerates mana from any positive on-hit damage (so, not including DoT ticks) from any skill, and generates mana equivalent to 40\*dmg/hp with Crits providing a 1.5x multiplier.

#### Rogue

* Classes gain mana when they:

* * Strike an enemy in combat (more effective on crits)
* * Dodge any attack (restores HP as well)

Like Warrior, Rogue mana model only generates mana from the auto attack. 3 mana on hit, 5 on crit, and 9 when you dodge any attack. If the monster misses, you do NOT generate dodge mana. As well, you regenerate 2% of your max HP (after END).

#### Deathknight

* Classes gain mana whenever an enemy takes damage from one of the Class's skills.

Deathknights generate 2 mana from ALL positive damage dealt to your enemies during combat, including DoT ticks.

#### Ninja

* Classes gain mana when they:

* * Land the first strike in combat
* * Strike an enemy in combat (more effective on crits)
* * Cast "Shadowburn" on a target without "Shadowblade"

Ninja mana model is relatively unique, generating 82 mana from being the one to initiate a fight. Then, like Warrior, it generates damage from positive auto-attack on-hits - 1 per hit and 2 per crit. As well, Shadowburn will generate 20 mana if Shadowblade is not active.

#### Zeal

* Classes gain mana when they:

* * Strike an enemy in combat while Zeal is active
* * Are struck by an enemy in combat while Zeal is active

Zeal mana model literally becomes Warrior mana model while Zeal is applied to the user.

#### Temporal Rift

* Classes gain mana when they:

* * Attack while under effect of Temporal Rift

Temporal Rift mana model will generate from positive autoattacks whilst Temporal Rift is active on the user. Generates 3 mana per noncrit, and 9 per crit.

---

<h2 id="primary-stats">3. Primary Stats & Base Stats</h2>

### Base Stats / LIST

The game calculates a "total pool" of Primary Stats based on your level, and then distributed based on your Class Model. This pool is referred to as the LIST or Level-Interstat-Total. Or more simpler, it's your total base stats.

After calculating this LIST value (or total base stats), the game then distributes the total depending on your Class Model. Below is a table indicating how it's distributed, the total is multiplied by a stat ratio. This is basically how the game calculates a class' base stats, ignoring equipment.

| Class Model | STR | INT | DEX | END | WIS | LUK |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| **Tank Melee** | 0.27 | 0.05 | 0.22 | 0.30 | 0.10 | 0.06 |
| **Dodge Melee** | 0.20 | 0.05 | 0.33 | 0.22 | 0.10 | 0.10 |
| **Power Melee** | 0.30 | 0.02 | 0.30 | 0.18 | 0.06 | 0.14 |
| **Offensive Caster** | 0.06 | 0.33 | 0.11 | 0.20 | 0.15 | 0.15 |
| **Defensive Caster** | 0.08 | 0.30 | 0.10 | 0.27 | 0.10 | 0.15 |
| **Power Caster** | 0.06 | 0.28 | 0.05 | 0.23 | 0.28 | 0.10 |
| **Full Hybrid** | 0.24 | 0.24 | 0.20 | 0.20 | 0.07 | 0.05 |
| **Luck Hybrid** | 0.22 | 0.08 | 0.21 | 0.18 | 0.08 | 0.23 |

You may find that after rounding, some of your values may not match directly of that in-game. You will likely be off by +1 in some of your calculations for different stats.

### Gear Stats / GIST

The game calculates a "total pool" of Primary Stats for your gears, based on the enhancement. Similar to how the game calculates the base stats for your Class Model based on your level, the game calculates the base stats for your Gear based on the Enhancement Level, and the Rarity (the +5 value). This is known as the GIST, or Gear-Interstat Total.

Different Gear Types have different limits on their base stat totals. So the game multiplies the GIST by a Gear Type ratio, to get the specific total for that type of gear.

| Gear Type | Ratio |
| :---- | :---- |
| **Cape** | 0.2 |
| **Helm** | 0.25 |
| **Weapon** | 0.33 |
| **Class** | 0.25 |

After you get the total for a specific Gear Type, the game then distributes this final pool based on Enhancement Type. Each enhancement has a unique stat spread, similar to Class Models.

| Enhancement | STR | INT | DEX | END | WIS | LUK |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| **Adventurer** | 0.16 | 0.16 | 0.16 | 0.17 | 0.16 |  |
| **Fighter** | 0.44 |  | 0.13 | 0.43 |  |  |
| **Hybrid** | 0.28 | 0.27 | 0.20 | 0.25 |  |  |
| **Thief** | 0.30 |  | 0.45 | 0.25 |  |  |
| **Wizard** |  | 0.50 |  | 0.10 | 0.20 | 0.20 |
| **Healer** |  | 0.45 |  | 0.40 | 0.15 |  |
| **Spellbreaker** |  | 0.40 |  | 0.20 | 0.30 | 0.10 |
| **Lucky** | 0.10 | 0.10 | 0.10 | 0.10 | 0.10 | 0.50 |
| **Depths** |  | 0.50 |  |  |  | 0.50 |
| **Forge** | 0.25 | 0.25 |  |  |  | 0.50 |
| **Vim** | 0.1 |  | 1.3 | -0.9 |  | 0.50 |
| **Examen** |  | 0.1 |  | -0.9 | 1.3 | 0.50 |
| **Anima** | 1.34 | 0.16 | 0.24 | -0.9 | 0.16 |  |
| **Pneuma** | 0.24 | 1.18 | 0.24 | -0.9 | 0.24 |  |
| **Hearty** | -0.2 | -0.2 | -0.2 | 1.5 | -0.2 | -0.2 |
| **Armsman (dead now)** | 0.38 |  | 0.36 | 0.26 |  |  |

A common misconception is that base enhancements have different effects on gameplay. For example, some people believe Healer makes your heals stronger, or Lucky improves drop rates. Enhancements are pretty much ONLY stat spreads, other than forge/awe enhancements which have specific passive effects or may have an additional proc.

### Secondary Stats

These are your Secondary Stats, they are directly used in combat calculations. Each stat is broken down into its own card below.

<div class="wiki-grid-2">

<div class="wiki-card">
<h5>Attack Power/Spell Power (AP/SP)</h5>
<p>Used to determine base damage of most skills in the game. As a result, having higher AP/SP will lead to more damage.</p>
</div>

<div class="wiki-card">
<h5>Hit Chance</h5>
<p>Chance to hit enemy. Having 100% Hit Chance = 0% Miss Chance. Enemy still has a chance to dodge because of nominal dodge theory (explained later). Base 90%.</p>
</div>

<div class="wiki-card">
<h5>Haste/Cooldown Reduction</h5>
<p>Reduces cooldowns of skills. Caps at 50% or half the cooldown of a skill. Skills are effected by haste dynamically, so if haste changes mid fight, your skill CDs are effected too. Base 0%.</p>
</div>

<div class="wiki-card">
<h5>Evasion/Dodge Chance</h5>
<p>Chance of dodging enemy. From extensive testing, max dodge is at 86.05%, due to a combination of enemy miss chance/nominal dodge. Base 4%.</p>
</div>

<div class="wiki-card">
<h5>Crit Chance</h5>
<p>Chance to crit when hitting an enemy. Healing is a little weird, will explain later.</p>
</div>

<div class="wiki-card">
<h5>Crit Modifier/Crit Mod</h5>
<p>Self explanatory, base is 150% (1.5).</p>
</div>

<div class="wiki-card">
<h5>Damage Boost/All Out</h5>
<p>Increases all outgoing damage (minus true damage). Base is 100%.</p>
</div>

<div class="wiki-card">
<h5>Physical Boost/Phy Out</h5>
<p>Increases outgoing damage for Physical Damage type. Base is 100%.</p>
</div>

<div class="wiki-card">
<h5>Magical Boost/Mag Out</h5>
<p>Increases outgoing damage for Magical Damage type. Base is 100%.</p>
</div>

<div class="wiki-card">
<h5>Max HP</h5>
<p>Self explanatory. Derived from Player Level and END.</p>
</div>

<div class="wiki-card">
<h5>Damage Resistance/All In</h5>
<p>Reduces all incoming damage (minus true damage). Base is 100%. Increases in reverse. i.e 80% on stat page = 0.2 or 20% in reality.</p>
</div>

<div class="wiki-card">
<h5>Physical Resistance/Phy In</h5>
<p>Increases damage resistance from Physical Damage type. Base is 100%. Increases in reverse. i.e 80% on stat page = 0.2 or 20% in reality.</p>
</div>

<div class="wiki-card">
<h5>Magical Resistance/Mag In</h5>
<p>Increases damage resistance from Magical Damage type. Base is 100%. Increases in reverse. Increases in reverse. i.e 80% on stat page = 0.2 or 20% in reality.</p>
</div>

<div class="wiki-card">
<h5>Healing Intake/Heal In</h5>
<p>Increases incoming heals. Base is 100%.</p>
</div>

<div class="wiki-card">
<h5>Healing Boost/Heal Out</h5>
<p>Increases outgoing heals. Base is 100%.</p>
</div>

<div class="wiki-card">
<h5>DoT Resistance/DoT In</h5>
<p>Increases damage resistance from DoT Damage type. Base is 100%. Increases in reverse. Increases in reverse. i.e 80% on stat page = 0.2 or 20% in reality.</p>
</div>

<div class="wiki-card">
<h5>DoT Boost/DoT Out</h5>
<p>Increases outgoing damage for DoT Damage type. Base is 100%.</p>
</div>

<div class="wiki-card">
<h5>Mana Consumption</h5>
<p>Amount of mana used by skill. Base is 100%.</p>
</div>

</div>

### Primary to Secondary Stat Conversions

[Refer to this](https://docs.google.com/spreadsheets/d/1fKQkhkXpeDnWyyK9zgnBiJmhpBYeZL-Cr6Nm8Zyn8to/edit?gid=1414839272#gid=1414839272) for the full dataset on how Class Models convert Primary Stats to Secondary Stats.

Secondary Stats are converted per Class Model. Each Class Model has a unique way of converting Primary Stats into Secondary Stats. Before they do this, they first calculate the Stat Efficiency. Stat Efficiency is the game's way of making sure there isn't a significant difference between a Level 100 and a Level 60, by reducing the conversion rate between Primary and Secondary Stats.

Depending on the class model, the game converts Primary Stats to Secondary Stats differently.

### Example Conversion

In this instance, I am using Swordmaster Assassin and trying to calculate the crit chance.

I am Level 100, and I calculate my efficiency by plugging in my Levels into the formula. Once I have the efficiency (x), I then multiply it with the Strength value and its Crit Chance ratio. I do the same with the Luck stat. I add 5 because the base crit chance is 5%. I then add 12 because SMA has a 12% Crit Chance passive. This leads to my final value which is exactly as shown in-game (or rounded to 2 d.p).

### Useful Information on Stats

Some general information applicable without nerding.

* Luck is the best stat, provides crit mod, provides AP/SP depending on Class Model (Melees gets AP, Caster gets SP, Luck Hybrid gets both), as a result it's also technically the jack of all trades stat.

* Generally Melee models rely on AP scaling skills, so investing into STR to get more AP is usually a good idea, minimise INT investment.

* Similar case with Caster models, they rely on SP scaling skills usually so invest into INT over STR.

* Luck Hybrid is the best Class Model because it abuses Luck stat even more. Gives you the most AP and SP per Primary Stat (Total across stats is 3.8, whereas other models only provide 2.7). Improves Crit Mod the most, generally disproportionately favours Luck over any other model.

* INT on Casters provide Mag Out and Mag In, whereas INT only provides Mag In for Melees. As a result, due to Mag Out scaling, if your caster has majority Magical skills, it might be more important to run Wizard over Luck. Depends situationally.

* Some classes are built around having ASS Haste/Crit Chance, therefore for those specific classes, it'd be a good idea to build around WIS/DEX builds.

* Class Models, while very important, aren't everything for a class. As we'll go over in a later section, skill scaling, types, and properties matter in how you build a class too.

Ultimately, the overarching purpose of this is to provide you with a concrete understanding of stat scaling within AQW. While knowing this isn't everything to building a class, as you still need to account for skills themselves, it's still the foundation for optimisation.

We'll next be discussing damage types, and how stats themselves interact with each other.

---

<h2 id="damage-types">4. Damage Types, DoT Squaring & Stat Caps</h2>

### Damage Types

Now we begin talking about damage types. When a skill is used, it first calculates base damage then it is multiplied by secondary modifiers. What modifiers it uses when dealing damage is determined by the damage type. There are 5 damage types in this game (4 officially) and I'll go over what stats they use. If you don't know this already, enemies have secondary stats too exactly like players.

<div class="wiki-grid-2">

<div class="wiki-card">
<h5>Physical Damage</h5>
<ul>
<li><strong>Player Stats</strong> - Phy Out, All Out, Weapon Boost, Crit Mod</li>
<li><strong>Enemy Stats</strong> - Phy In, All In</li>
</ul>
</div>

<div class="wiki-card">
<h5>Hybrid Damage</h5>
<ul>
<li>Uses the same modifiers as Physical Damage</li>
</ul>
</div>

<div class="wiki-card">
<h5>Magical Damage</h5>
<ul>
<li><strong>Player Stats</strong> - Mag Out, All Out, Weapon Boost, Crit Mod</li>
<li><strong>Enemy Stats</strong> - Mag In, All In</li>
</ul>
</div>

<div class="wiki-card">
<h5>True Damage</h5>
<ul>
<li><strong>Player Stats</strong> - Weapon Boost, Crit Mod</li>
</ul>
</div>

</div>

The base damage of a skill is multiplied by each secondary stat for its particular type. So a Physical Damage skill with 110% All Out, 110% Phy Out, and a base damage of 1000 will be calculated like this.

1000 \* 1.1 \* 1.1 = 1210

When you are healing a player, the Heal Out/Heal In modifiers come into play.

### DoT Damage Type

DoT Damage is an unofficial damage type, but they are the most complicated of the bunch. This is because of the mechanics associated with them.

Unlike regular forms of damage which are calculated immediately, because DoTs/HoTs can last they have two points in which they are calculated.

* First at aura application, where they "store" a stat's value (known as static)

* Secondly right before each tick, where they use your stats (known as dynamic).

A secondary stat can be considered Dynamic, or Static, depending on when it's calculated/used for the DoT. Below is a list.

* All Out - dynamic & static

* All In - dynamic

* Mag Out - dynamic

* Dot Out - static

* Dot In - dynamic

* Heal In - dynamic (if HoT)

* Heal Out - dynamic (if HoT)

First thing is that a DoT/HoT is considered "pseudo-magical", this is because they only use Mag Out, but they do not use the enemy's Mag In stat when calculating damage.

You will also notice that the All Out stat is both Dynamic and Static. This means it's multiplied twice in calculation, and the community refers to this concept as squaring.

DoTs do not utilise Crit Mod or Weapon Boosts, probably fair for balance purposes (squaring OP).

### Secondary Stat Caps

Secondary Stats have individual caps and also when interacting with each other. As a result, there's limitations on what can be done to enemies/players through buffs/debuffs alone.

First I will introduce you to individual caps, however these aren't always true because you're likely not working with caps in a vacuum.

<div class="wiki-grid-2">

<div class="wiki-card">
<h5>Damage Resistance</h5>
<p>80% (0.2 All In)</p>
</div>

<div class="wiki-card">
<h5>Damage Boost</h5>
<p>-90% (0.1 All Out)</p>
</div>

<div class="wiki-card">
<h5>Physical Resistance</h5>
<p>80% (0.2 Phys In)</p>
</div>

<div class="wiki-card">
<h5>Physical Boost</h5>
<p>Not capped</p>
</div>

<div class="wiki-card">
<h5>Magical Resistance</h5>
<p>80% (0.2 Mag In)</p>
</div>

<div class="wiki-card">
<h5>Magical Boost</h5>
<p>Has a cap, but because of weird circumstances regarding the magical damage type, it actually doesn't matter</p>
</div>

<div class="wiki-card">
<h5>Healing Intake</h5>
<p>Not capped (you can have negative healing intake and take damage from healing sources)</p>
</div>

<div class="wiki-card">
<h5>Healing Boost</h5>
<p>Unknown, pretty much irrelevant if it is or not, we just haven't been able to confirm it yet with current tools</p>
</div>

<div class="wiki-card">
<h5>DoT Resist</h5>
<p>80% (0.2 DoT In)</p>
</div>

<div class="wiki-card">
<h5>DoT Boost</h5>
<p>Unknown</p>
</div>

<div class="wiki-card">
<h5>Haste</h5>
<p>50% (0.5 Haste)</p>
</div>

<div class="wiki-card">
<h5>Crit Mod</h5>
<p>Not capped</p>
</div>

</div>

I would like to remind you that the stat page lies. Reducing incoming stats (All In, Phy In, Mag In) actually decreases the amount of damage you take. So 80% All In on the stat page is actually saying the stat is now at 20% or 0.2 in reality (lower = better for you).

Should be obvious but just mentioning this because seen people get confused.

As I stated before, if you're in a situation where you've only got reduced All In then these caps are likely to be the case. However, in Ultras like Speaker, who reduces your Mag In, it is a lot more different.

### Combined Caps

Combined caps get wacky, because despite stats having individual caps. What first resolves is the Combined Caps. So this means that when it's first calculating the Combined Cap of Mag In and All In, these two stats are at their uncapped states during calculation.

So in a hypothetical situation, we're in Ultra Speaker, let's say Malgor is about to throw a Truth nuke at us. Let's say their base damage is 2500. We have already taken a truth before this, so we're about to take 300% more damage than usual (more damage taken = higher all in stat). However, we're VDK, we have 50% All In passive, 25% from Penitence, AP is buffing us for an additional 20%, and also QCM for another 30%. So our real total All In is -25% (base is 100%, lower is better).

So we'll be multiplying -25% All In and 300% Mag In. So our final calculation is this.

2500 \* -0.25 \* 3 = -1875

But because the combined caps of -0.25 \* 3 < 0.2, the game forces the final damage to be multiplied by 0.2

2500 \* 0.2 = 500

So despite us being debuffed by Mag In significantly, we're still about to take a minimal amount of damage thanks to the abuse of combined caps.

There is actually a Speaker chart centered around this mechanic.

For the left chart, QCM can optionally take the 4th zone.

---

<h2 id="combat-math">5. Damage Interactions, Combat Math & Order of Execution</h2>

### Enemy Secondary Stats

Enemies similar to players have base secondary stats, this is the usual setup for most enemies, though there's obviously differences.

<div class="wiki-grid-2">

<div class="wiki-card">
<h5>Hit Chance</h5>
<p>90%</p>
</div>

<div class="wiki-card">
<h5>Haste</h5>
<p>37.5%</p>
</div>

<div class="wiki-card">
<h5>Crit Chance</h5>
<p>15%</p>
</div>

<div class="wiki-card">
<h5>Evasion</h5>
<p>10%</p>
</div>

<div class="wiki-card">
<h5>Crit Mod</h5>
<p>200%</p>
</div>

<div class="wiki-card">
<h5>Base Auto CD</h5>
<p>4s</p>
</div>

<div class="wiki-card">
<h5>Base Damage Range</h5>
<p>27-33</p>
</div>

</div>

### Nominal Dodge

This is a theory where monsters have a base dodge stat that isn't affected by your own hit chance. In fact, the only way to get around this is by reducing your opponents dodge stat through debuffs. So if you've ever noticed a monster dodging your attacks despite having over 100% hit chance, it's because of this.

### Heal Crit Interactions

So a heal that isn't guaranteed to crit (e.g. LC 4 Skill) may seem like it's not critting majority of the time despite having 100% Crit Chance. This is because when you heal a player, the players dodge comes into play. It doesn't make sense for a heal to Miss/Dodge, so they're evaluated as non-crit (Hit) results. That's why it seems you non-crit more than you crit during heals.

### Hit / Miss / Dodge / Crit Interactions

[Link](https://www.reddit.com/r/AQW/comments/1itjyom/hit_miss_dodge_crit_mechanics_to_date/) to full post.

Miss / Hit is resolved first. What this means is given 100% effective dodge and 100% effective hit chance reduction, the result will always be a miss. This is important for Rogue mana model, since you need dodges.

Dodges are resolved next. Misses and Dodges eat away at opposite ends of the chance roll, meaning that they're additive. 40% effective miss chance (60% hit) and 60% effective dodge means you will avoid every hit. Hit chance buffs add to this range, and dodge plays catch up. If you have 110% effective hit chance, you can never miss, and the opponent needs 110% dodge chance to avoid every hit.

Crit is then resolved between the Dodge and Hit range. Crit chance always occupies the lower range of hit chance rolls, while dodge removes from the top of the range. What this means is given effective 90% dodge chance and 10% crit chance, all results that make it through will be crits, because the ranges overlap.

The interaction between Crit and Miss is not fully understood. The running hypothesis is the lowest end of Crit rolls starts after the hit roll, meaning that Hit chance doesn't eat away at crit chance, but Dodge chance eats away at Hit/Crit result.

Edit: It's important to mention that Crit rolls could start the other way around. It's just described this way because Dodge x Crit was observed first, and which eats at which end of the roll is irrelevant. Either way, Dodges and Misses seem to pinch crits in the middle.

### Miss Results

When you miss, you don't apply Auras, nor do you damage the enemy. This is why Classic Ninja in Dage works, because of Shadowblade, it forces the enemy to miss. As a result, Dage never stacks any auras, leading to a faster overall kill.

### Skills

The basics is that a skill in AQW that deals damage has a base function. This is the damage source or also called the damage function. It dictates what base stats are used to create the initial base damage. This is then multiplied by the value in the "damage" key. Then it is multiplied by the type modifiers, so in this case Strike of Order is a physical skill, multiplied by the modifiers associated with physical damage type. Skills can also have specific properties, in the case of Lord of Order, every skill can crit for example.

In the example above, taken from my discord bot, the damage is 0.7, the function is APSP1, and the type is Physical. It has the property forceResult crit, this means that whenever this skill is used, it will always force a crit result.

### Functions

Damage Functions Sheet. Somewhat nerdy section, you just need to know how a function scales, rather than do math every time.

Thankfully due to other nerd contributions, we've figured out what a lot of skill functions do and their dedicated formulas. You can view the sheet linked above, under the "Known Functions" tab to view the formulas we've figured out so far.

In AQW, most of the functions derive from one of the base functions. These are the most primitive functions, in the sense all that they do is deal damage, they don't deal with stacking or anything else.

If you're planning to do some math yourself, just know if you're level 100, WDPS is always 85.

WepRange is the Weapon Range value, dictated by your weapon. Usually it will say something like 30-30 or 27-33. Weapon Range is a decimal value, and depends on the range you're dealing with. It indicates a damage roll. If a weapon is 30-30 (static), then the range is 1.0 by default. If the range is 27-33, the range can vary between 0.9-1.1.

Stacking functions exist, where for every stack of an aura, the skills damage increases by a modifier of +0.5.

### Skill Damage / Coefficients

The function dictates the base damage, but then a skill is then multiplied again by the value in the damage key. It's just simple multiplication. For example, AP1 calculates to 500. Damage is stated to be 1.5 or 150%. Multiply by 1.5. Damage is now 750.

Heals in this game are just negative damage, so you'll find heals to have negative coefficients.

### Properties / Packet Terminology

Skills can have unique properties that dictate certain traits for that skill. This kinda falls into backend terminology. I'll list some stuff we've figured out below.

* tgt - Determines the target of the skill.

  * h - enemy

  * s - self

  * f - friendly

* dsrc - Damage Source, refers to the functions.

* typ - Damage Types.

  * p, ph, aa - physical (Auto is always physical, unless manual)

  * m - magical

  * ma - true damage

  * pm, mp - hybrid

* ref - Reference of skill (aa, a1, a2, a3, a4)

* cd - Cooldown of skill in ms

* mp - Mana cost of skill

* dmgfct - Damage Factor? Idk what this represents though, math doesn't involve it.

* forceresult - Determines whether a skill is forced to evaluate to a result.

  * crit - Always crits

  * nomiss - Can't miss. Can be crit or hit result types.

    * hHit - Always hit result type (non-crit)

  * addCrit - Literally add crit chance on a specific skill

  * xDmg - Specifies how much self damage you take in relation to MaxHP

  * randomLength - Skill can apply specific effects randomly, shows amount of effects - 1.

  * manaBack - Something weird with PMB, basically gives mana back but somehow different to just having negative mp cost?

### Enhancements

Forge Enhancements and Awe Enhancements can have skills attributed to them, e.g Elysium. They can apply auras and have damage types, damage functions, and all other properties that are usually attributed to regular skills associated with classes.

### Enemy Skills

Enemies also hold similar data to players, except their base Weapon DPS is usually insane (Desolich is 852). Not a lot of damage functions related to enemy is known because of lack of data.

Issue is you can only get WDPS of enemies through sniffing, you multiply WDPS \* 2.5 to get your average damage or 1.0 range. They also have coefficients. So WDPS \* 2.5 \* Coefficient for some specific enemies where WDPS \* 2.5 is too low.

### AOE Target Ordering - Player

For the player, AOE targets follow the monster's map ID. Starts from m:1, goes higher with every enemy. Picks lowest ID in the current screen.

### AOE Target Ordering - Enemy

When an enemy fires an AOE attack, the target ordering follows the player with the lowest HP. This is important for Speaker, as for each subsequent player hit, they take extra 100% damage. Important for double zone tactics, hence why you need specific HP thresholds for it to work.

### Order of Execution

Skills resolve in this order:

* Damage -> Auras -> Enhancement Damage (if applicable) -> Enhancement Aura (if applicable)

Keep this in mind if you're trying to calculate damage during fights.

### DoT Calculations

They're calculated by finding the coefficient of a single tick, then multiplying by duration. DoTs are reliant on max durations to get accurate calculations, which is also required for some funny bugs. You can't sniff the raw values of a DoT, you have to do it through math.

A thing I didn't bring up earlier is that Functions are static. This means that the Primary Stats you pass into the DoT function are not erased, so it's recommended to buff yourself with LOO 2, or Valiance, to further improve your DoTs/HoTs.

---

<h2 id="auras">6. Auras & Instancing</h2>

### Auras

Skills can apply auras on the enemy and yourself. They're usually just buffs/debuffs or associated with DoTs, but they can also be unique auras that apply mechanics. Auras are a lot less straightforward than skills since there's a lot more nuance to them.

### Buffs / Debuffs

Any buffs/debuffs to primary stats are multiplicative, whereas any buffs/debuffs to secondary stats are additive. So Lord of Order buffs Primary Stats by a multiplicative 20% (1.2x), whereas it only buffs All Out by an additional 30%.

### Aura Profiling

Auras have different profiles that affect how they work. This is mostly related to DoTs/HoTs, but generally applicable for all auras.

* Non-Stacking Non-Overtakeable - When you apply the aura again, it refreshes the time but keeps the same values.

  * This is one of the more common types of auras, most DoTs are like this.

* Stacking Refreshable - Everytime you apply the aura again, it refreshes the timer and value (even at max stacks).

  * Also common, think of Acheron self-DoT.

* Non-Stacking Non-Refreshable - You cannot update the time nor value, eventually fades after application.

* Non-Stacking Refreshable - When you apply it, it destroys the previous instance and applies a new one.

  * Dragon of Time 4 Skill DoT "Destiny Alight" has this property

  * This property is somewhat interesting as in my experience, all auras that have this profile allows stacking between multiple instances

* Stacking Non-Refreshable - You cannot update the time, but you can change the value for the duration of the aura. (I might be wrong)

  * Exalted Soul Cleaver's 5th Skill applies "For the Legion!" which is how this one works.

### Aura Instancing

I'd like you guys to know that this is still an area of the game that's being explored. I only just came up with this hypothesis during the creation of this guide, but it's still got some issues.

Non-Stackable auras can be interacted with between multiple instances. If a skill is meant to scale with the consumed aura, it doesn't scale but does consume the aura.

E.g Cryo, CAV Branded, AP Seal, DS 5

Stackable auras however can only be seen between multiple instances. Their auras are not consumed. If a skill is meant to scale with the consumed aura, it scales but doesn't consume the aura.

E.g HBV Grace, Old AP

To help explain the theory, I'll ask a few questions.

In the olden days, Archpaladin's Eden consumed Commandment stacks. You have two Archpaladins in a room. Archpaladin's Commandment is a stackable aura.

How many total stacks of Commandment can we get between the two APs?

1) 50

2) 100

What happens when you use Eden? Assume both APs stacked 50 each.

1) It eats all 100 stacks and deals double damage

2) It eats only 50 stacks and deals full damage

3) It eats only your Commandment stacks, and deals full damage

If you have 0 stacks of Commandment, but the other player has 50, and you use Eden.

1) Eden eats no stacks and does minimum damage

2) Eden eats no stacks and does full damage

3) Eden eats all stacks and does full damage

4) Eden eats all stacks and does minimum damage

The answer to question 1 is a, you can get 100 stacks between the two APs. Because the aura's are in different instances, the Commandment stacks do not care for the other instances of Commandment. It only cares for itself. Doesn't apply to all stackable auras however, because there are stackable auras that are separate instance aware. Just providing you the majority interaction.

The answer to question 2 is c, it consumes your Commandment stacks because those are the auras it has access to. As we are unable to interact with another player's aura instances (since it's stackable). It checks for the highest count aura and attempts to consume them (if it's your instance), then scales based on that.

The answer to question 3 is b, it deals full damage because we're aware of the other instances (it's stackable). The game checks for the highest stack count amongst all instances, then attempts to consume it. But because the aura isn't part of your own instance, you cannot consume the aura. It scales based on the highest count recorded, not the amount consumed.

Similarly, say you have an FB with a mega big HoT after potloading/squaring, but then you carry that HoT over to Yulgar and their HoT is only 1000. It's because the players need to be present in the room

Based on this information, in some edge cases it's actually beneficial to have multiple of the same class in the same room. The default notion is that it's useless, but it's not always true. There's a lot of funny edge cases where having the same type of a specific aura is nice to have.

### DoT Interactions with Aura Profiling

As I've gone over it already partially, DoTs/HoTs have different behaviours when having different aura profiles. The Non-Stacking Overtakeable is the default for DoTs/HoTs, it's the usual aura profile ideal for squaring logic. If you refresh them, their values stay the same.

But Stacking Refreshable and Non-Stacking Refreshable kind of break this idea, because they force the DoT to recalculate their value. So squaring logic you do prior to applying the DoT is made null after refreshing them.

### Interaction based Auras

So outside of buffs/debuffs and DoTs, there are auras that have specific interactions/mechanics. They often do stuff that doesn't involve the stat page, and do calculations separately. I'll list a few auras below that fit this description.

* Arcane Shield - Additional damage reduction based on 30% of your Spell Power

  * Loses 8 mana per hit

  * Does nothing to True Damage

* Event Horizon - Additional damage reduction based on 25% of your Attack Power

  * Does nothing to True Damage

* Safeguard - Acts as additional HP, amount is dependent on the class

  * Fades after damage exceeds the amount

* Noxious Decay - Inverts all incoming healing except lifesteal

* Curse of Blades - Inverts crits as heals

* Mana over Time auras (Spirits Within, old Cupcake Mana)

  * Weird thing about them, they never spread to allies. Cupcake Mana literally didn't work in groups.

### Aura Properties / Packet Terminology

* isNew - Simple boolean

  * Determines whether an aura is a new instance

  * In the case of Non-Stacking Refreshable Auras, these auras instead of refreshing the timer, would instead apply a new instance by destroying the old and setting a new with this.

* aura++ / aura+ - Creating an aura instance or refreshing an existing one

* aura-- / aura- - Deleting an aura instance or expiring one

* val - Multiplier applicable for said aura, used in stacking functions

* stk - Used by the UI, generally determines how many stacks of an aura there are. However, not necessarily accurate (SMA, GD, for example).

* aura+p - Aura instances related to class passives.

---

<h2 id="chronomancers">7. Chronomancers & Rift Math</h2>

### Chronomancers

Gonna have a whole dedicated section to the weirdness that is chronos. I will be talking about chronos that have a nuke based on the damage they recorded, as this function is weird and has some intricacies. As a result, we'll be ignoring Infinity Knight and Archivist of Time since this doesn't apply to them.

### Rift Modifiers

Chronos have rifts. They either have Temporal Rift, or Chaos Rift, and this aura stacks to 4. Each stack has a different multiplier.

* 1 Stack = 0.5

* 2 Stack = 0.7

* 3 Stack = 1.0

* 4 Stack and above = 1.5

Damage recording begins from the application of the first rift, and holds a 10s interval of damage. If damage recording exceeds 10s, the 10s window shifts in accordance to damage dealt within a period.

[Use this amazing animation](https://streamable.com/msrl8)

### Chrono2

This is the Damage Function associated with Chronos that records damage. Each chrono has a unique nuke multiplier, this is the coefficient associated with a skill. I'll list them below.

* CDK: 1.45

* Chrono Commander: 1.3

* Chrono Corruptor: 1

* Chronomancer: 1

* TCM: 1.3

* IC: 1.5

* SSOT: 0.2

* TK: 1

* Nechronomancer: 0.3

* CSS: 0.3

* PhCM: 0.16

When Chrono2 is calculated, it uses Weapon Boosts, Crit Mod, and the modifiers associated with its damage type to calculate the damage. Classes like VDK or Arach don't contribute to Chrono2 because they're debuffs, and Chrono2 only works with buffs.

This is different for DoT Nukes however, it only uses the Static Stats of DoTs for calculation, and ignores Weapon Boosts/Crit Mod. So SSOT/NCM only have DoT Out and All Out for Chrono2 calculations.

### Damage Recording

When damage is recorded, the damage is converted to True Damage. So it ignores any modifiers except Crit Mod and Weapon Boosts.

In the case of DoTs, when a DoT is recorded, the Static Stats are factored in, but the dynamic stats are left out. Obviously Weapon Boosts and Crit Mod isn't counted either. So in a case of a DoT that is recorded, it uses All Out, and DoT Out for its calculation.

### Final Calculation

You pretty much multiply your Recorded Damage with the type modifiers associated with the nuke, then the coefficient, then the rift mod value. After that you get the big nuke value. You'll notice that Crit Mod and Weapon Boosts are utilised twice in calculation, so there's actually exponential scaling with Crit Mod and Weapon Boosts.

Similar case applies for DoT Nukes, there's big scaling from DoT Out and All Out stats, as a result you want to maximise those stats to improve your nuke the most.

### SSOT/SWOT

You might have seen [this video](https://www.youtube.com/watch?v=-RubTUC3Sa8) on youtube and wondered how to do this. Well I'll explain the weirdness of SSOT to you, and why I think it's like the 2nd best general chrono after CSS.

First thing is that you'll notice the Chrono2 coefficient is 0.2, the lowest of all chronos. This is intentional. The way SSOT works is that you can feed the previous nuke into your next nuke, because you can almost *always* apply a Temporal Rift before the nuke goes off. The nuke is a delayed DoT, Temporal Rifts apply from your auto attack which is pretty fast.

With this in mind, you might think we should be able to get infinite damage solo. But if you've actually used SSOT, you'll probably plateau around 200-300k. This is because of first order recurrence relations. I'll go over this part in a [later section](#combat-math), but the tldr is that the combined modifiers of SSOT are lower than 1.0.

Expressed via first-order recurrence relations:

$$D_{k+1} = \alpha D_k + B$$

To achieve infinite scaling, your combined multiplier ($\alpha$) must exceed $1.0$, requiring your **All Out** stat to exceed 234% ($3.34$) through enhancements and potions.

0.2 Coefficient

1.5 Rift Modifier

2.12 All Out (212%)

If the final output multiplier of the nuke exceeds 1.0 of the damage recorded during that window, the nuke feeds back into itself at a larger value every cycle. With the current setup, we actually have the final nuke decay every time. Which is why our damage is capped.

So to make this scale infinitely, we have to buff our All Out using specific enhancements, pots, and buffs.

* Vainglory (15%)

* Potent Honor Potion (75%)

* Elysium (10%)

* Legion Revenant (30%)

This should all be enough to tip the scales so that you can infinitely scale with SSOT. Classes like Arach or VDK do contribute to the overall damage you deal, but don't contribute to scaling. VDK is worse than Arach because it debuffs Mag In/Phy In which DoT Nukes don't use.

### Boss Shields vs Chrono2

So now you know how to get big damage, but someone might tell you that you can't "nuke" ultras because of boss shields. Well they misunderstand how boss shields, damage caps, and Chrono2 functions.

In a non-boss shield scenario, Chrono2 holds an internal counter of the actual nuke you're meant to deal (billions of damage or whatever), then checks if it's higher than the 100m damage cap. If it is, the nuke is then just capped at 100m. Pretty simple.

In a boss shield scenario, Chrono2 uses that internal counter of the nuke and passes it into the boss shield. Then the boss shield is checked against the damage cap. Basically this means you can pass quintillions of damage into a boss shield, and theoretically one shot any boss with SSOT.

### Boss Shield Calculation

(Damage - Shield)^exponent

Read wiki fr

### Timeless / Corrupted Chronomancer DoT Inversion (Transience)

So Transience on TCM/CCM applies a self-DoT, making you a ticking time bomb before blowing up. Well through the magical power of squaring, you can invert the HoT. This happens through PVP, alt needs to have Archpaladin. Here are the steps or [watch it here](https://youtu.be/FxXDEF7o4CY?si=dxWZHqnyr7UM0kVW).

1. Have AP reduce your all out below 100%, so max Commandment stacks and Seal should work.

2. Have TCM then apply Transience Hourglass, then apply the self-DoT by using the 4th Skill

3. Wait for debuffs from AP to expire

4. You now have a stacking HoT, ggs.

---

<h2 id="sources">8. Sources & Enemy Stat Sheets</h2>

### Sources

People asked me to list my sources so yes I will.

* Mana Regen Models: [https://sites.google.com/view/aqwbook/secondary-stats/mana?authuser=0](https://sites.google.com/view/aqwbook/secondary-stats/mana?authuser=0) - TDNQ

* Primary Stats & Secondary Stats: Danzon's site in general was used throughout this guide.

  * [https://sites.google.com/view/aqwadvancedmechanics/home/primarysecondary-stat-conversions/primary-stats?authuser=0](https://sites.google.com/view/aqwadvancedmechanics/home/primarysecondary-stat-conversions/primary-stats?authuser=0)

  * [https://sites.google.com/view/aqwadvancedmechanics/home/primarysecondary-stat-conversions/secondary-stats?authuser=0](https://sites.google.com/view/aqwadvancedmechanics/home/primarysecondary-stat-conversions/secondary-stats?authuser=0)

### Enemy Stat Sections

### **/naoisegrave Warden Iseul**

The range is incorrect.

520 \- 636

 **/naoisegrave Warden Iseul**

The range is incorrect.

515 \- 629

### **Star Captain**

### **Troll Spellsmith**

### **/fiendshard Adiomonde**

The range is incorrect.

2410715 \- 2946429

Don't remember anymore instances of incorrect values, but just saying should probably double check what wiki says *just in case.* Though most information is verified thanks to the nerd community helping out.

</div>
