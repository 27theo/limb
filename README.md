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

**Important note: Without editing, limb damage will only register when the limb attack is queued and runs.** This ensures that nobody can illusion the "your blow lands with a crunch" line without also illusioning a system queue message, which is an illegal illusion. You can tweak the trigger however you'd like, but the existing method is what I and others recommend.

Queueing example: `queue addclear eqbal stand|wield mace|smite Romaen right leg`

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

## Checking if a target is prepped.

This is something pretty class-dependent, so I thought I'd leave it up to the individual.

The easiest method, which works for a few classes:
 1) Upon hitting a limb, set a variable X to the amount of damage that hit did.
 2) To check if a limb is prepped: `if lb[target].hits["right leg"] + X >= 100 then`

## Mangles

The package doesn't handle mangles out of the box yet.

![image](https://user-images.githubusercontent.com/76885241/137416758-038922a7-7b4d-45b7-8744-a02718a02545.png)
