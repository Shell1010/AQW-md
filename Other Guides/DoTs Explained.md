---
dg-publish: true
dg-metatags:
  og:site_name: AQW Hub
  og:title: DoTs Explained
  og:description: Comprehensive explanation to DoTs/HoTs
  description: Comprehensive explanation to DoTs/HoTs
  og:image: https://bigrat.monster/media/bigrat.jpg
---
DoTs/HoTs are probably one of the most complicated yet least discussed parts of the game. General pubs have basically no idea how DoTs work, and it’s not something that’s elaborated by the game or developers. I’ll try make this comprehensive.

[Referencing some data stated here](https://sites.google.com/view/aqwadvancedmechanics/creditsreferences?authuser=0)
## “Pseudo-Magical” Type

All damage in AQW has a specific damage type, this dictates what modifiers are used during calculation. But unlike regular forms of damage, DoTs and HoTs are calculated at two distinct points: 
- First at aura application, where they use your secondary stats and “store” that value (known as static)
- Secondly right before each tick, where they use your current stats (known as dynamic). 

Here’s a list of stats that the DoT/HoT uses, anything with an “x” indicates that the stat is not used:
- All Out - dynamic & static
- All In - dynamic 
- Mag Out - dynamic
- Mag In - x
- Phys Out - x
- Phys In - x
- Dot Out - static
- Dot In - dynamic
- Heal In - dynamic (if HoT)
- Heal Out - dynamic (if HoT)

It’s called “pseudo-magical” by the community because it uses Mag Out, but doesn’t use Mag In.

An important thing to note is that All Out (Damage Boost) stat is used twice when calculating DoTs. This is important for understanding squaring.

*They’re unaffected by weapon boosts too, but doesn’t matter because squaring is broken.*
## Squaring

Squaring is using the static All Out stat to maximise the HoT/DoT. The idea is to make your All Out as large as possible right before applying the DoT/HoT.

One simple trick is equipping Vainglory then applying the HoT, before equipping absolution. This will improve your HoT considerably. Here’s an example with Stonecrusher. Probably need to zoom in.

[Squaring Video demonstration](https://www.reddit.com/r/AQW/comments/1iiitgx/squaring_demonstration/)

![[Pasted image 20251208044200.png]]

The idea is that by equipping vainglory and then applying the HoT, the static (or stored) All Out is then used during calculation. This not only applies to equipped items, it also applies to buffs too.
Examples:
- Lord of Order (30% All Out)
- Legion Revenant (30% All Out)
- Potent Honor Potion (75% All Out)

If LOO and LR buff you before you apply your HoT, it will multiply your healing, bringing it from 155, to 712 per tick.

General tldr:
- Maximise your all out before beginning a fight, if your heals are HoT dependent, or damage is DoT dependent
- While not mentioned, damage functions are also static (so you can “square” valiance)
- DoT Out is also static, so on classes that boost DoT Out (Dragon of Time for example), you can use it to maxmise your own HoTs/DoTs
## Making DoTs into HoTs

All heals in this game are just negative damage. With abusing stat interactions, you can make damage go negative, in this instance we’ll talk about making DoTs negative (into HoTs).

[Watch this video for a demonstration](https://youtu.be/QQ0KXCy1X3g)

Now let’s answer the Veni,Vidi,Vici part. Why do the DoTs on Veni and Vidi become HoTs? Take note that all the stat interactions that apply to players also apply to monsters. Let’s analyse the video carefully.

*I just realised it’s pixelated, so you’re just gonna have to believe me when I say these numbers*

When he applies Veni on us, we have accumulated 5 stacks of Eminent (from AP 2 skill). This reduces his outgoing damage by 25%. This is considered our static all out value, it’s what was there when he applied Veni on us initially.
![[Pasted image 20251208091232.png]]

After we see Veni appear, we apply Seal (AP 4 skill) immediately, this reduces his outgoing damage by an additional 90%. So we have effectively -25% outgoing damage reduction on him (0.75 - 0.9 = -0.15).  This is our dynamic all out value, which is the value *right before* the DoT ticks.

The game applies both the static and dynamic stat in calculation of the DoT. Basically in this scenario we’re multiplying a negative by a positive which equals a negative.

![[Pasted image 20251208095421.png]]

I use Na’al as a simple example since it’s basically designed around this concept. But there’s a few other bosses in the game you can be creative with and would work the same. For example, Ultradage. 

## Damage Functions

This is a lot more math focused, [[Stats & Misc]] references a spreadsheet which goes over them. Tldr damage functions are what your skills scale off, they are not secondary stats but are often linked to primary stats like Attack power, Spell power, or HP. A skill can scale off Attack Power, but still use a Magical damage type. It’s important you know that Function != Damage Type, because your enhancement builds could effect how much damage you do.

Functions are also considered *static* for DoTs. This means you can apply something like Valiance before starting your fight, giving you a stat buff and permanently boosting your DoT/HoT.

The next section will tell you how some of these are calculated, but I’ll list some important variables for now.

- Base HP = 360 + (((Weapon Enhancement Level-1)/(level cap-1))^0.66) * 1640.
- WDPS = (Base HP/2000) * 0.85 * 100
	- For the sake of simplicity, at level 100, WDPS is always 85.
- Simple Base Functions
	- AP1 = WDPS + 0.1(Attack Power)
	- SP1 = WDPS + 0.1(Spell Power)
	- AP2 = Weapon Range * 2(AP1)
	- SP2 = Weapon Range * 2(SP1)
		- These functions are based on your weapon range, static weapons are 1.0, stable are between 0.9-1.1, basically these are damage rolls. 

Tldr all forms of damage in the game use some sort of combination or derivative of these functions, they may add extra scaling, or additional mechanics like lifesteal healing. These functions are multiplied by a coefficient which determines their damage/heal value (before modifiers).

## Calculating DoTs

This part more irrelevant to gameplay and more just an additional knowledge that you may find interesting. Usually in the design notes or skill descriptions you’ll get something like this.

>You focus the power of the entire sun on a single point. Does a large amount of damage on hit then deals 700% damage over 10 seconds.  

This is Lightcaster’s Skill 5, it states the DoT deals 700% damage over 10s. But how do we get this value?

First thing we determine in-game is if the function is dependent on weapon range. This determines whether it will be an AP2/SP2 function since these two functions are dependent on ranges. AP1/SP1 functions do not use weapon range in their calculation, therefore the damage won’t change if you use the same skill over and over again.

We use a weapon like this with a variable weapon range to test. We just use 5 against a target and then let it fade and try again. If the DoT damage changes between each use of 5, it means it’s either AP2 or SP2. In this case, it does not change, so therefore it’s either SP1 or AP1.
![[Pasted image 20251208104129.png]]

Now we determine if the function AP1 or SP1. We can use either might tonic or sage tonic and then use our 5 skill. If the value changes when using Might tonic, that means it’s AP1. If it doesn’t then it’s SP1. Similary we can do the same with Sage tonic, but in reverse.

![[Pasted image 20251208104808.png]]

So through these steps, you should have determined that the function is SP1. Now math begins. We get our in-game values. Here’s my stats and the DoT tick.

![[Pasted image 20251208105704.png]]

To determine the true value of our DoT, we first calculate our SP1 value using our stats. So that’s WDPS + 0.1 (Spell Power) => 85 + 0.1 (Spell Power) => 85 + 0.1(1560) = 241.

Next we divide our in-game damage by the modifiers to reach the “base” or initial value once again. So we have a 15% Damage boost passive, this means it’s squared and we have to divide by 1.15^2. After that, we divide again by the mag out 85.46 => 1.8546. 

After these two operations, our value is 168.79. We then divide 168.79 by our SP1 value, this gives us 0.7. This is our coefficient.

We know that the DoT lasts 10 seconds. We also know that it ticks once every 2 seconds. 10/2 = 5. So there’s 5 ticks.

Next we multiply the amount of ticks by the coefficient, 
5 * 0.7 = 3.5 => 350%

So our DoT is actually 350% not 700%, and this is actually true since it’s specified in the [wiki page](http://aqwwiki.wikidot.com/lightcaster-class). Tldr don’t believe your skill descriptions, they lie!

*Smol disclaimer, there’s hybrid functions in this game too. That use both AP and SP, still you can do similar tests to determine these. I just didn’t bother explaining since this is a DoT explanation not functions.*

## Calculating Physical functions with Pseudo-Magical type

This is also irrelevant to actual gameplay, again just if you’re interested. If you noticed by SC build, I’m using Fighter enhancement, Anima helm, and you may think this is counter-intuitive because we’ve established that DoTs are of pseudo-magical type. But this does not mean they can’t use Attack power in their functions. SC is one of those cases.

Using steps previously, I managed to establish that SC’s 4 HoT is not based on weapon range. I also know that it scales off Attack Power since I used Sage Tonic and it did not do a thing.

![[Pasted image 20251208112142.png]]

So my function is AP1. Which is 85 + 0.1(822) = 167.2. I then divide the in-game value by my modifiers to get the base. Which is 155/1.4229 = 108.93, despite the function being physical, it still uses mag out in calculation. I then do 108.93/167.2 to get my coefficient which is 0.65.

SC’s land embrace lasts 8s, and ticks every 2s. Meaning it ticks 4 times total. 4 * 0.65 = 2.6 => 260% Damage healed over 8s. Anyway yes, very cool.