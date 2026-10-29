---
status: approved
---

# Design brief: CircuitLens — a fault-finding trainer for electronics

## Who it's for
First-year electronics students and self-taught hobbyists who can read a schematic but have never systematically debugged a dead circuit on a bench.

## The one spatial moment
I'm leaning over a table. A circuit is laid out in front of me, 40 cm wide and scaled up about 2.5x from a real breadboard, a little below eye level. Current is drawn as moving arrows along the traces. Two branches run off the battery: one flows and lights its LED, the other is dead along its whole length. I lean in, pinch components one at a time to read their voltages and current, and work out myself which part in the dead branch failed — the three parts look identical, so the readings are the only evidence.

## Why it belongs on glasses
- Uses: draws in the world; leaves your body free
- Why it's better than the phone or laptop version: the circuit sits on the table at a size you can lean over and reach into, and you diagnose it by walking around it and probing it with your hands, the way you would a real board on a bench — not by clicking a schematic on a screen.

## Product or overlay
- Type: product — the circuit is virtual and is the experience
- What the real version would sense: nothing
- Stand-in for the preview: none needed

## The circuit
- **Topology**: one battery feeding two parallel branches. A single series loop won't do — an open circuit stops current everywhere, so the arrows would either vanish entirely or stop exactly at the culprit and give the answer away.
- **Live branch**: current flows along it and its LED is lit.
- **Dead branch**: no current along any of its three components, so the arrows say which branch failed but not which part. Probing voltage along the dead branch is the only way to localize the fault.
- **The fault**: a burnt-out, open resistor. All three components in the dead branch look identical, so there is no visual clue at all. The only way to find the fault is the voltage reading: the open resistor reads battery voltage in and zero out, while the other two read the same voltage on both sides. The scorch is on its underside and only becomes visible when the component is lifted out — confirmation that the diagnosis was right, not the clue that leads to it.

## Where things live
- Where the user is looking during the main task: down and forward at the board on the table, arms low
- **Circuit board**: flat on a virtual table, roughly 70 cm away, a little below eye level. 40 cm wide by 25 cm deep — about 2.5x a real breadboard, chosen on purpose so each component is a big, forgiving pinch target with a readable label, while the whole board still sits inside the display's usable area.
- **Current arrows**: along the traces on the board surface, always visible
- **Probe readout card**: right at the component being pinched, not in a side panel. Small, one at a time. (default) about 10 cm wide, floating a few cm above the board next to that component so it doesn't cover it.
- **Parts tray**: slides in at the near edge of the table, within arm's reach and still in view, holding three candidate replacements. (default) about 25 cm wide.
- **LEDs**: one per branch, on the board and in view. The live branch's LED is lit from the start; the dead branch's LED lights when the repair is correct.

## Hands and input
- Probe a component: pinch (tap) on the component
- Commit to a diagnosis: pinch and hold the component — it lifts out of the board and leaves a visible empty slot
- Fit a replacement: grab a part from the tray and drag it into the empty slot
- Undo a wrong part: pull it back out of the slot
- Targets are big and highlight when aimed at.
- Voice: none

## When things show
- **Current arrows**: always on. They're the problem statement, so they stay — flowing in the live branch, absent in the dead one.
- **Probe card**: appears only while pinching a component, fades about a second after release. Only one exists at a time — pinching a new component dismisses the last one. No wall of panels piling up over the board.
- **Parts tray**: doesn't exist until a diagnosis is committed. Slides in with a soft chime so its arrival is noticed, and slides away the moment the slot is filled.
- **On success**: everything clears — no cards, no tray. Just the arrows flowing in both branches and both LEDs lit, so the repaired circuit is what you see.
- If something needs attention out of view: nothing is out of view; the soft chime marks the tray's arrival.

## Done criteria
Each one can be checked in Lens Studio's preview.
1. I can walk around the table with the keyboard and mouse and the board stays anchored in place and readable from any angle.
2. Current arrows animate along the live branch and are absent along the whole dead branch, leaving all three of its components unaccounted for, so the fault isn't obvious from looking.
3. Pinching any component shows one readout card at that component with voltage in, voltage out and current through it. Pinching a different component dismisses the first card.
4. Pinch-and-hold lifts a component out, leaves a visible empty slot, and the parts tray slides in with a chime. If the lifted component is the faulty one, the scorch is visible on its underside once it's out.
5. Dragging the correct replacement into the slot makes current flow through the repaired branch, lights its LED and clears all UI. Dragging a wrong part refuses to seat and the branch stays unpowered.

## Out of scope
- Recognizing a real circuit board, real components, or real meter readings.
- More than one fault scenario. (default) One hard-coded two-branch circuit with one burnt-out resistor and three candidate replacements, of which one is correct.
- Multiple simultaneous probe cards, a schematic view, or a parts catalogue.
- Saving progress between sessions; scoring or levels.
- Real circuit simulation. (default) Voltage and current values are hard-coded per component for the healthy and faulty states.

## Risks and open questions
- The unpowered branch: the SPECS display is additive, so black renders as transparent. The dead branch must read as *visibly unpowered* using dimmed-but-still-light traces and absent arrows, not as black geometry.
- Whether the readout card at 70 cm reads easily while leaning over the board is a comfort question only real glasses can settle. Feel unproven.
- The three components in the dead branch must be visually indistinguishable while seated, or the puzzle collapses into spotting the odd one out. Worth checking in the preview from several angles and distances, including whether the scorched underside is hidden while the part is in the board.
- Whether the voltage readings are legible enough to compare across three components from where the user stands may need tuning in the preview.

## Build notes for CLAD
- Build for SPECS so it runs and can be demonstrated in Lens Studio's preview. No SPECS device is available.
- Use Spectacles Interaction Kit (SIK) and UI Kit for all interactions, so they work with the mouse in Interactive Preview and with LEAF.
- Build any stand-in exactly as described above, and keep it obvious in the scene.
- Use real-world scale in centimeters. Keep content inside the user's view during the main task.
- The display is additive: black renders as transparent. Don't rely on black or very dark content to be seen; keep text light and readable from where the user stands.
- Get the basic flow working first, then add detail.
- Write LEAF scenarios for each done criterion, run them in preview, and report which pass. Say which criteria have no test.
- Don't record, identify, or follow people.

## After the build: judge it
This part is for you, after CLAD finishes.

1. **Does it work?** Ask your agent which LEAF tests passed and which done criteria have no test.
2. **Walk around it.** Open the preview in Interactive Preview. Use WASD to move, Q and E to go down and up, and right-drag (or hold Shift) to look around. Clicking acts as a pinch. Stand where a user would and look at the task.
3. **Ask the three questions.**
   - Does it use what I'm looking at?
   - Does it put something in my space, where it belongs?
   - Does it free my hands or let me keep my eyes up?
   - Would it be just as good on a phone? If so, what would make it need the glasses?
4. **Check comfort.**
   - Everything I need is in view while I do the task. Nothing sits at the edges, behind me, or stuck to my face.
   - Every control is within reach of someone standing there.
   - Text reads easily from where I stand. No dark UI disappearing.
   - Things show when needed and get out of the way.
5. **Label what you know.** Write "logic proven" next to anything the tests and preview show working, and "feel unproven" next to anything only real glasses could tell you (comfort over time, real hand tracking, real recognition).
6. **Fix with design notes, not code.** Tell your agent what to change in design terms, for example: "Move the step card 15 cm lower and next to the pan. Make the Next button twice as big. Re-run the tests." If a fix takes under a minute, like nudging a panel, do it yourself in the scene.
7. **Submit.** Record a video under 3 minutes of your Lens in the preview, public on YouTube. Make your repo public with your Lens Studio project and this `devpost/` folder. Details are on the hackathon site: https://learn-specs.devpost.com/resources
