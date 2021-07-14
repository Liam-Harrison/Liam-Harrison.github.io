---
layout: default
---

# QuestLike
QuestLike is a text based game in which you embark on a journey alone into a dangerous realm of monsters and magic. The game has an incredibly deep simulation where the entire world is concurrently simulated - not just the space you're immediatley inside of. Intuitive text commands allow the player to easily communicate intent to the game to get the results they were expecting. You can check it out for yourself on my [GitHub page](https://github.com/Liam-Harrison/QuestLike).

![Demonstration](https://raw.githubusercontent.com/Liam-Harrison/Liam-Harrison.github.io/master/Showoff.gif)

## Giving the game commands.
Players can communicate to the game very easily, after reading the player input the command system automatically finds a command that matches what the player inputed and executes that command.

For example the player can write ```> place apple in my bag``` which will find something called "apple" and put it in something called "bag". If their is more than 1 bag in a space the game will ask which one you are refering too, for example the player might see this output:

```
Found 2 items with the tag "bag", please select one:
  [1] - Satchel  - A small bag - On your right leg.
  [2] - Backpack - A large backpack - On your back.
Enter a number from [1 - 2] > 
```

## Designing commands.
Commands can be quickly and easily designed by allowing the designed to get straight to the chase and write real behaviour. You can quickly create a command with the following straight forward code:

```cpp
MoveCommand() {
  keywords = new string[] { "grab", "hold" }
  usecases = new string[] {
    "_ $",
    "place $ in $"
    // The '_' character means any word in the the keywords list.
    // The '$' character signifies a player inputed argument.
  }
}

void Execute() {
  if (!Game.Locate<Item>(GetArgument(0), out Item item)) return;
  
  switch (Usecase) {
    case 0:
      Game.Player.GetCollection<IInventory>().Add(item);
      break;
    case 1:
      if (Game.Locate<Item>(GetArgument(1), out Item location))
        location.GetCollection<IInventory>().Add(item);
      break;
  }
}
```

## The BodyParts.
The game simulation includes a very deep Entity system, where entities can contain many interconnected bodyparts (but not required to be - Entities could be intangable, like Ghosts). The bodyparts include everything from major organs to extremities, the Heart provides blood pressure allowing for bloodflow and is connected to the Lungs with pulmonary arteries, the Lungs in-turn convert some deoxygenated blood back to oxygenated blood at the cost of oxygen in the air and send the oxygenated blood back to the heart with arteries.

```
> look at my Lung with my cyber eye

Found 2 objects with the tag "lung", please select one:
  [1] - Left Cybernetic Lung  - Creates oxygenated blood.
  [2] - Right Lung            - Creates oxygenated blood.
Enter a number from [1 - 2] > 2

> Right Lung - Creates oxygenated blood.
A critical organ which converts deoxygenated blood into 
oxygenated blood.

Total blood..............: 52.3mL (hypertense)
Oxgeynated blood.........: 15.3mL
Deoxygenated blood.......: 37.0mL
Blood pressure...........: Strong
Health...................: Perfect
Converting...............: 5.1mL/turn
Connect to nervous system: Yes (via nerve)

The Left Lung is attatched to the Chest.
3 parts are attatched to the Left Lung:
  - "Upper Lobe"
  - "Middle Lobe"
  - "Lower Lobe"

The Left Lung has these blood vessels:
  - to Heart          (large artery)
  - from Heart        (large pulmonary artery)
  
  - to Upper Lobe     (pulmonary artery)
  - from Upper Lobe   (artery)
  
  - to Middle Lobe    (pulmonary artery)
  - from Middle Lobe  (artery)
  
  - to Lower Lobe     (pulmonary artery)
  - from Lower Lobe   (artery)
```

Attatching bodyparts and connecting blood vessels are different systems - attatchment shows where bodyparts are physically in an entity whereas blood vessels are for blood flow. On top of this bodyparts also are connected by **nerves** or **cybernetic connections** - Bodyparts must have a pathway to a signal sender which is usually either a **brain** or **cybernetic signal generator** and bodyparts can check if they're connected to these to do certain tasks (i.e. a hand could check for a nervous connection when the player attempts to hold something). Because of the nature of the nervous systems implementation you don't necessarily need nerves at all - parts could be connected with cybernetic cables, by magic or remotely.

## Blood Simulation

From the Heart blood flows to the chest and from the chest to the other extremities of the body such as the head, arms and legs. Blood pressure from the heart is strong but varies, every game update the hearts blood pressure rises and falls to simulate the beating of the heart. As blood travels throughout the body it loses pressure, as blood pressure drops so does the bodyparts ability to move blood, if the oxygenated blood in a bodypart drops too low it will begin to take damage which further reduces its ability to move blood and decreases its other functions.

The depth of the bodypart system means they can be built up of other bodyparts or hold items. The designer in theory could go on designing the parts of a creature and instead of just a heart object you could make that be built up of chambers and the lungs could be built up of lobes which are interconnected. The designer could make a fantasy monster with 3 hearts and 2 heads if they design it carefully enough.

The bodypart system is however optional and you don't need to spend your time designing blueprints for humanoids, quadrupeds or fantasy monsters. However the deeper the system the more player freedom.

## Items, Combat & Magic
The combat in QuestLike is as deep as the Entity system, items can be used on yourself, enemies or their individual bodyparts with a command like ```> hit elder goblin in the arm with the sword in my right hand```. Sometimes it's benifical to use a potion on an enemy as holy damage negativley affects undead opponents with a command like ```> throw healing potion on zombie```

Items can be consumables which disappear or change after a certain amount of uses, as well as used to cast magic on a target. However items aren't the only way to cast magic, if you have the mana and the skills you can cast certain spells on opponents to get an advantage, an example of that would be:

```
> cast magic on elder goblin

Found 2 spells you can use on the Elder Goblin, please select one:
  [1] - Steal - Chance to take a target object
  [2] - Force of Change - Switches properties.
Enter a number from [1 - 2] > 2

Found 3 things you can use "Force of Change" on, please select one:
  [1] - Head - Not much happens here in a goblin.
  [2] - Left Lung - Creates oxygenated blood.
  [3] - Right Lung - Creates oxygenated blood.
Enter a number from [1 - 3] > 2

You used "Force of Change" on the "Elder Goblins Left Lung".
For a short time the Lung will convert oxygenated blood into 
deoxygenated blood.
```

### [Public GitHub Repository](https://github.com/Liam-Harrison/QuestLike)

### [Return to the homepage](./)
