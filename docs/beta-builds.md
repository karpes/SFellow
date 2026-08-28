# Beta builds and why they expire

Short version: **each beta stops working about six weeks after it was built.** Ask for a newer one and carry on.

The longer version is below, because a build that switches itself off deserves an explanation rather than a
surprise.

## Why there is an expiry at all

Without an expiry, the beta you install today is a free copy of the product, forever, running code that was
current in a week nobody remembers. Two problems in one: bug reports against builds that are months old, and a free
edition that was never meant to exist.

## What actually expires

The date lives in the build, not on your machine. There is no counter that starts on first launch, no hidden file
to delete, no state to reset — and correspondingly nothing you can break by accident.

**Moving your clock back does not help.** The check remembers the furthest date it has ever seen. Nor does editing
the plugin's files: the dates are signed, and an altered build reads as expired rather than as extended.

If the check cannot make up its mind, it decides the build has expired. A licence check that fails open is not a
check.

## What stops, and what does not

When a build expires, the Salesforce features stop — all of them, not a crippled subset:

- the Apex engine: errors, navigation, usages, hover, completion, structure;
- Apex, LWC, Aura and Visualforce highlighting;
- everything that runs `sf`: orgs, retrieve, deploy, anonymous Apex, schema;
- both tool windows and the menu actions.

Your files are untouched, and your project opens normally. What is left is a message saying the build expired, the
file-type icons in the project tree, and the `-meta.xml` nesting.

Notably, **highlighting goes too**. An expired build showing you coloured Apex would be a smaller product than the
real one, given away — so the answer is no rather than nearly.

## Getting a working build again

Request the newest build — email **karpes.dev@gmail.com** — and install it over the old one. Builds are handed
out directly for now, so asking is the whole procedure. Every new beta carries a fresh expiry date, and the practical effect of all this is that you stay on
a recent build.

There is no way to extend a build you already have, and that is on purpose.
