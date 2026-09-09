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
line, in the right file. A path that does not open anything here — the org sometimes reports a problem against a
file that exists only inside its own response — is printed as plain text rather than as a link that goes nowhere.

## When something fails

The card says what happened in words, not just that it failed: the CLI's own message, or the org's. A lost
connection is called that — "could not reach the org… try again" — with the original text kept in brackets, because
`TypeError: fetch failed` explains nothing to the person reading it.

## Stopping a command

The toolbar has a **Stop** next to **Clear**; it lights up while something is running. Long operations also run as
regular IDE background tasks, so the status bar can stop them too, and the Apex test tree has its own Stop.

However you stop it, the command's card closes as **⊘ Stopped** — grey, not a red failure. A command you withdrew is
not an error, and reporting it as one would blame the org for your own decision.

## What it deliberately does not show

**Raw `sf` output.** The `--json` payloads that SFellow parses do not go to the console. They are large, they are not
written for a human, and the useful parts are already in the card.

**Commands you did not cause.** Everything printed here came from a button in the panel or from a background task
SFellow started for you.

## Clearing

The toolbar has a **Clear**. Cards are not persisted between IDE sessions.
