# Weapon Burst Fire Toggle

This script lets players toggle a weapon between a **Burst-Fire Mode** and a secondary **Non-Burst Mode** (which can be set to either **Semi-Auto** or **Full-Auto**).

## Step 1: Component Setup

1. Select the main (root) GameObject of your weapon in Unity.
2. Add a **Scripted Behaviour** component to it.
3. Add a **Data Container** component to the same object.
4. Set the **Source** of the Scripted Behaviour to your script file.  
   The file must be named exactly `SimpleBurstFire.lua`.
5. Enable **Keep Scripts On Third Person** in the Weapon script.
6. Use the latest Weapon script from `weapon-script`.
7. Choose **One Shot** in **Audio Mode**.

## Step 2: Data Container Setup

Open your **Data Container** and add these 10 keys exactly as written:

| Key | Type | Description |
|---|---|---|
| `burstCount` | Int | The total number of bullets fired in a single trigger pull burst (for example, `3`). |
| `startNonBurst` | Bool | `True` (checked): Weapon spawns in Non-Burst mode. `False` (unchecked): Weapon spawns in Burst mode. |
| `nonBurstAuto` | Bool | `True` (checked): Non-Burst mode is Full-Auto. `False` (unchecked): Non-Burst mode is Semi-Auto. |
| `nonResetting` | Bool | `True`: M16A2 style. Releasing the trigger mid-burst saves the remaining shots for the next pull. `False`: The burst resets completely every time you let go of the trigger. |
| `botBurstCooldown` | Float | The pause time in seconds that AI bots must wait between firing bursts. |
| `switchCooldown` | Float | Time in seconds before the player can switch modes and fire again. Best if you match this to the animation length. |
| `switchKeybind` | String | The lowercase letter the player presses to change modes (for example, `t`). |
| `switchParameterName` | String | The exact name of the Trigger parameter you will make in your Animator (Step 3). |
| `selectorParameterName` | String | The exact name of the Int parameter you will make in your Animator (Step 3). |
| `selectorValues` | String | Two numbers separated by a single space (for example, `0 1`). The first number is for Burst (Mode 0), and the second number is for Non-Burst (Mode 1). |

## Step 3: Animator Setup

### Parameters

Open your Animator's **Parameters** tab and add two new entries:

- A **Trigger** parameter. Name it exactly what you typed in `switchParameterName`
- An **Int (Integer)** parameter. Name it exactly what you typed in `selectorParameterName`

### The Physical Selector Switch

1. Create a new Animator Layer for the gun's lever.
2. Click the layer's gear icon and set:
   - **Weight** to `1`
   - **Blending** to `Additive`
3. Create two states in this layer:
   - one static animation clip for the **Burst** position
   - one for the **Non-Burst** position
4. Make transition arrows connecting the two states to each other.
5. Click the transition arrow going to the **Burst** state.
   - Under **Conditions**, set your Int parameter to **Equals** your first number (for example, `0`)
6. Click the transition arrow going to the **Non-Burst** state.
   - Set the condition to **Equals** your second number (for example, `1`)

### The Hand Animation

1. In your main animation layer, create a state for the hand reaching out to flip the switch.
2. Create a transition line from **Any State** into this hand-switching state.
3. Under **Conditions**, add your Trigger parameter.
4. Create a transition line from the hand-switching state back to your **Hip State**.

## Credits

Huge thanks to **ProfessionalDebil** for the massive help, and for letting me use his script as a reference for this.
