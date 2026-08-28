# Console

Everything SFellow does shows up here as it happens — every command it runs for you and every background job it
starts.

![A console card](img/console-card.png)

## Cards

**What it does.** One operation, one card: a header with the operation name, the org and the time; a rail down the
left; the steps as they happen; and a duration at the bottom.

Inside a card you see the actual command — `$ sf data query -q … -o SFellowDemo --json` — before it runs, not after.
Long paths are shortened so the line stays readable.

**When it helps.** Two of them, really. First, a long operation stops being a spinner with no explanation: you can
see which step it is on. Second, when something fails you have the exact command, and you can paste it into a
terminal and take it apart yourself.

**Overlapping operations.** A background refresh and a save-triggered deploy can start at the same time. They get two
separate cards: the second one buffers and prints whole, rather than interleaving its lines into the first.

## Clickable errors

Deployment errors, failed test frames, and anonymous-Apex compile errors are links. Click one and you land on the
line, in the right file.

## What it deliberately does not show

**Raw `sf` output.** The `--json` payloads that SFellow parses do not go to the console. They are large, they are not
written for a human, and the useful parts are already in the card.

**Commands you did not cause.** Everything printed here came from a button in the panel or from a background task
SFellow started for you.

## Clearing

The toolbar has a **Clear**. Cards are not persisted between IDE sessions.
