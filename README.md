# limb
Limb counter for Achaea, on Mudlet. Please see [the releases page](https://github.com/27theo/limb/releases) for the download.

## Apparently I chose an awful namespace. I thought I could get away with it, but it seems not. Re-releasing the package with a different namespace in the next few hours or so!

## Setup

 1) Install the latest release from the releases section (see to the right of this on desktop website).
 2) Ensure that your target alias meets the following requirements:
     - Sends "settarget \<target\>" to the game.
     - Sets the `target` variable to the target's name, capitalised appropriately. (E.g. "Romaen" as opposed to "romaen".)

Optional 3) Add highlights and echoes to your taste. Something like 

```lua
if limb[name].hits[ltar] > 100 then
  echo("\n                   <red>--- " .. ltar:upper() .. " BROKE! " .. ltar:upper() .. " BROKE! ---\n")
end
```

at the end of the `limb.addHit()` function should do the trick for those of you who like big red text etc.

Note: Without editing, limb damage will only register when the limb attack is queued and runs. This ensures that nobody can illusion the "your blow lands with a crunch" line without also illusioning a system queue message, which is an illegal illusion. You can tweak the trigger however you'd like, but the existing method is what I and others recommend.

Hopefully, the functions provided make it easy to add something like "target hits rebounding", if you've got data for that kind of thing. 

## Functions

These are all already handled by existing triggers.

#### `limb.addHit(name, hit_limb, amount)`

 - Add a given number amount to the hits table for name, on the hit_limb.
 - E.g. `limb.addHit("Romaen", "left leg", 16.42)`

#### `limb.resetLimb(name, hit_limb)`

 - Reset a limb prematurely.
 - E.g. `limb.resetLimb("Romaen", "left leg")`

#### `limb.salve(name, area)`

 - Handle a salve appropriately. Area can be any of "head", "torso", "arms", and "legs".
 - Assumes left limb before right, for arms and legs.
 - E.g. `limb.salve("Romaen", "legs")`

#### `limb.resetAll(name)`

 - Reset all limbs on name.
 - E.g. `limb.resetAll("Romaen")`
