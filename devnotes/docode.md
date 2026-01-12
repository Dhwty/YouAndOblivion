==HOW TO DO TWEE/TWINE==
-------------------------


**DOCUMENTATION:**  
[DE Twine Macros](https://github.com/apepers/DiscoElysiumTwineMacros/blob/master/README.md#using-the-macros)  
[SugarCube Macros](https://www.motoslave.net/sugarcube/2/docs/#macros)  


### SKILL CHECKS
We're using a simplified system, where skill checks are just going to roll with attribute bonuses, for now, rather than actual skill bonuses, because I don't really want to deal with that many variables. At the moment, there is only one build for Harry: the Basic Bitch, 3/3/3/3, but that's gonna change at some point. Here's which attributes to roll for which skills:  
$MOT: "composure", "hand/eye coordination", "interfacing", "reaction speed", "savoir faire", "perception", "perception (smell)", "perception (sight)", "perception (taste)", "perception (touch)", "perception (hearing)"  
$INT: "conceptualization", "drama", "encyclopedia", "logic", "rhetoric", "visual calculus"  
$FYS: "electrochemistry", "endurance", "half light", "pain threshold", "physical instrument", "shivers"  
$PSY: "authority", "empathy", "esprit de corps", "inland empire", "suggestion", "volition"  

\>> The basic bitch build needs to be addressed, because it's not \*possible\* to roll higher than 15. If we're not using skill points, it may be worth making it higher. The highest canonical checks are 20.  

*   Easy: 5-8
*   Medium: 9-11
*   Hard: 12-15
*   Legendary: 15-19
*   Impossible: 20


**Pass Chance for Basic Bitch Cop:**  
 5   36/36 (100%)  
 6   35/36 (97%)  
 7   33/36 (92%)  
 8   30/36 (83%)  
 9   26/36 (72%)  
10   21/36 (58%)  
11   15/36 (42%)  
12   10/36 (28%)  
13   6/36 (17%)  
14    3/36 (8%)  
15   1/36 (2.8%)  

**HOW TO SKILL CHECK:**  
<<set \_roll to rollDice() + $MOT>>  
You got: \_roll  
<<if \_roll >= 8>>  
    <<SkillSuccess>>  
    <<PassiveSkill Perception>>  
    <<AddParagraph "He has definitely been smoking, and from the smell wafting off his jacket, it's more than just one.">>  
<<else>>  
    <<SkillFailure>>  
    <<PassiveSkill Perception>>  
    <<AddParagraph "No, it's gone now. It's probably just the smell of last night's clinging to his jacket.">>  
<</if>>  


### Macros You Need
*   <<SkillSuccess>>: shows the green flashy and the success message
*   <<SkillFailure>>: shows the red flashy and the failure message
*   <<PassiveSkill "Skill Name">>: Sets the speaker to the correctly coloured skill name
*   <<SetSpeaker "Character Name">>: Sets the speaker to the character name, no fancy colouring.
*   <<BlankSpeaker>>: Leaves the speaker off the following paragraph, if you don't want to repeat the one from the previous paragraph or change it.
*   <<AddParagraph "Text goes in here">>: Adds a paragraph of text, followed by a 'Continue' prompt. These don't change the node, they just advance down it.
*   <<AddOption "Option Text" NodeName>>\[\[|NodeName\]\]: This adds choices for the player to make. Each choice will take you to a new node. Remember to include an option to proceed or return from the new node.
*   <<KimfluenceGained NUMBER>>: Displays green text saying your influence with Kim has increased, and increments the variable by NUMBER
*   <<KimfluenceLost NUMBER>>: Displays green text saying your influence with Kim has decreased, and decrements the variable by NUMBER
*   <<ItemGained "Item name">>: Displays green text saying you've gained the item. You \*may\* want to use this with a variable to track that you really did pick up the item.
*   <<ItemLost "Item name">>: Displays green text saying you've lost the item. If there was a variable saying you picked it up, remember to set the variable back to zero.
*   <<NewTask "Quest name">> Displays green text saying you have a new task. Set the task variable to 1. If it's a multi-stage task and what stage you're at matters, continue incrementing the variable along the way.
*   <<TaskComplete "Quest Name">> Displays green text saying you've completed the task. Set the task variable to 100. Ain't no quest gonna have 100 steps, so 100 is a good 'quest done' marker for any task variable.
*   <<SecretTaskComplete "Quest Name">>: You didn't know this quest existed, but you sure did finish it. Set the task variable to 100.
*   <<ThoughtGained "Name of thought">>: Green text saying you've gained a thought. Set the thought variable to 1.
*   <<ThoughtComplete "Name of thought">>: Green text saying you've completed a thought. Set the thought variable to 2.
*   <<LevelUp>>: Green text saying "Level up!" Not a whole lot of use for this, tbh.
*   <<set \_roll to rollDice() + $ATT>>: performs a skill check with the attribute. Change ATT to PSY, FYS, INT, or MOT, depending on the skill. See above for a whole-ass skill check example.



### Naming Variables
Global variables, that is, variables used in multiple nodes, all start with $. The vast majority of variables you use should be global.  
Local variables go away when you change nodes, so they should be used for things like rolling dice. They all start with \_.  


#### Attribute Variables | Global
Copotypes are in!  
*   $copotype
*   $INT
*   $PSY
*   $FYS
*   $MOT



#### Reputation Variables | Global
*   $Kimfluence: how badass Kim thinks you are. Increment and decrement this as needed, with choices.
*   $StationRep: how well Harry is thought of by his co-workers and/or boss. Increment and decrement as needed, with choices.



#### Location Variables | Global
These track whether you have visited or are aware of certain locations. They can be used to change the descriptions of nodes or to add exits to nodes. Use 'vis' for visited places and 'seen' for opened exits.  

*   $Day: What day is it? Use this to set blocks for different days in parts of the scene. Day can be 1, 2, or 3.
*   $visCrimeScene: have you clicked through the epic description of the crime scene once? Great, now you don't have to do it again.
*   $visMainRoom
*   $visStreet: you've arrived at the scene. Further visits to the street should not trigger a repeat of the intro.
*   $seenAlley: you've seen the alley out the window, and now you can go there from the street.



#### Clue Variables | Global
These track whether you've gotten certain clues, yet. These \*should\* play into day-change mechanics. If you haven't done certain things, you shouldn't be able to advance the day. "You feel like you're missing something." Use 'got' for items and 'know' for observations or stuff from processing's reports.  

*   $gotPrybar: you've picked up the prybar at the crime scene.
*   $knowKimsPrybar: you've established that this is Kim's prybar.
*   $knowKimjury: you saw the bruises on Kim's wrist
*   $knowKimsCorpseClue: you know Kim knew this guy. As the number gets higher, it opens more options and insights.
*   $knowAutopsy: you've finished the autopsy
*   $knowJizz: you know what's on the corpse's chest.
*   $knowKiller: As this goes up, you become more certain who killed Poulin
*   $knowPoisoner: As this goes up, you become more certain that a) Poulin was being poisoned, and b) that it was Geroux
*   $GarteKnowsDead: You told Garte that his neighbour is dead. Without this, he will probably find out through other means by Day 2, which will likely colour his interactions.
*   $SpokeToGarte: You talked to Garte on Day 1 and likely traumatised him! Good job!



#### Autopsy Variables | Global
Variables that affect what you see looking back at the autopsy report.  

*   $autVKnockoffs: Set to 1 if Harry notices Poulin's jeans are knockoffs
*   $autVSkin:
*   $autVNoSkin:
*   $autVJizz:
*   $autVDrugs:
*   $autVSkipInternal: Set to 1 if internal autopsy was skipped
*   $autVPetechia: Set to 1 if 'petechial haemorrhaging' in report
*   $autVBite:
*   $knowKimBite: you've figured out that a) the dead guy was bitten and b) probably by Kim. Probably opens dialogue options later
*   $autVJaundice:
*   $autVClotting:
*   $autVSlowBar:
*   $autVWeakBar:
*   $autVShortBar:



#### Thought Variables | Global
These are thoughts. When the thought is gained, set them to 1. When the thought is complete, set them to 2. They should start with 'thought'.  

*   $thoughtKimsAss: THIS MAN HAS NO ASS!
*   $thoughtCunoDoesntCare: MAYBE CUNO FUCKIN' CARES!


**Misc**
<<set $cumsicle to 0>>  
<<set $seenMedCab to 0>>  


#### Dice Variables | Local
*   \_roll: the final total of rolling 2d6, plus the attribute, plus any bonus
*   \_bonus: for a temporary bonus based on whether another variable is set.


\### Notes for Pen  
\# Paste code at YouAndOblivion.twee line 431, then compile. Above 431 is the template.  
\# Compile with: tweego -o YouAndOblivion.html YouAndOblivion.twee  
\# Decompile with: tweego -d -o YouAndOblivion.twee YouAndOblivion.html  
###  
