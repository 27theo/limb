# limb
Limb counter for Achaea, on Mudlet. Please see [the releases page](https://github.com/27theo/limb/releases) for the download.

## Setup

 1) Install the latest release from the releases section (see to the right of this on desktop website).
 2) Ensure that your target alias meets the following requirements:
     - Sends "settarget \<target\>" to the game.
     - Sets the `target` variable to the target's name, capitalised appropriately. (E.g. "Romaen" as opposed to "romaen")
 3) Ensure that your limb attacks are queued. See the queueing example below.

Optional 3) Add highlights and echoes to your taste. Something like 

```lua
if lb[name].hits[ltar] > 100 then
  echo("\n                   <red>--- " .. ltar:upper() .. " BROKE! " .. ltar:upper() .. " BROKE! ---\n")
end
```

at the end of the `lb.addHit()` function should do the trick for those of you who like big red text etc.*

**Important note: You must serverside queue your limb attacks, and have CONFIG SHOWQUEUEALERTS ON. Without editing, limb damage will only register when the limb attack is queued and runs.** This ensures that nobody can illusion the "your blow lands with a crunch" line without also illusioning a system queue message, which is an illegal illusion. You can tweak the trigger however you'd like, but the existing method is what I and others recommend.

Queueing example: `queue addclear eqbal stand|wield mace|smite Romaen right leg`

## Adding limb status to the end of your prompt

The function `lb.prompt()` returns a string displaying the values of the head, torso, left arm, right arm, left leg, right leg. You can change this order, if you navigate to the script declaring the function.

The string might look like `[98|0|0|0|105|105]`, for example.

### Svof

![image](https://user-images.githubusercontent.com/76885241/137488080-0e16bd2e-c21d-4cec-907d-9cb877da34e4.png)
Thank you [Xanton](https://forums.achaea.com/profile/Xanton).

### Other systems/custom profile

![image](https://user-images.githubusercontent.com/76885241/137489978-63c82c56-4f54-4b3e-affb-3a53fcfa7ef6.png)

## Functions

These are all already handled by existing triggers.

#### `lb.addHit(name, hit_limb, amount)`

 - Add a given number amount to the hits table for name, on the hit_limb.
 - E.g. `lb.addHit("Romaen", "left leg", 16.42)`

#### `lb.resetLimb(name, hit_limb)`

 - Reset a limb prematurely.
 - E.g. `lb.resetLimb("Romaen", "left leg")`

#### `lb.salve(name, area)`

 - Handle a salve appropriately. Area can be any of "head", "torso", "arms", and "legs".
 - Assumes left limb before right, for arms and legs.
 - E.g. `lb.salve("Romaen", "legs")`

#### `lb.resetAll(name)`

 - Reset all limbs on name.
 - E.g. `lb.resetAll("Romaen")`

## Checking if a target is prepped

This is something pretty class-dependent, so I thought I'd leave it up to the individual. 

The easiest method, which works for a few classes (classes that only have one limb damage attack: priest, psion etc):
 1) Upon hitting a limb, set a variable X to the amount of damage that hit did. I use `lb.lastHit`.
 2) To check if a limb is prepped: `if lb[target].hits["right leg"] + lb.lastHit >= 100 then`

Otherwise, if you're playing a blademaster or a tekura monk, you're going to have to get more creative.

## Mangles

The package doesn't handle mangles out of the box yet.

![image](https://user-images.githubusercontent.com/76885241/137416758-038922a7-7b4d-45b7-8744-a02718a02545.png)
