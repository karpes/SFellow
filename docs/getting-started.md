# Getting started

Half an hour, start to finish: install the plugin, connect an org, pull some metadata down, change a class, push it
back. If you have used the Salesforce CLI before, none of this will surprise you — that is the point.

## 1. Install

Ask for the current build — email **karpes.dev@gmail.com** — then **Settings → Plugins → ⚙ → Install Plugin from Disk…**
and restart the IDE.

You also need the **Salesforce CLI** on your `PATH`. Check it in any terminal:

```
sf --version
```

If that prints a version, SFellow will find it. If it does not, install the CLI first — the plugin runs `sf` for
everything that touches an org, and it will not invent a connection of its own.

## 2. Open a project

**File → Open…** and pick a folder containing `sfdx-project.json`. That file is what makes a folder a Salesforce
project — SFellow looks for it, not for a folder name.

No project yet? **File → New → Project → Salesforce** runs `sf project generate` for you and offers to connect an org
and retrieve straight after. See [Project and tree](project.md).

The **SFellow** tool window appears on the right edge. Everything below happens in it.

![Connecting an org](img/orgs-login.png)

## 3. Connect an org

Open the **Orgs** section of the panel and press **Connect**. Pick where the org lives:

- **Production / Developer** — `login.salesforce.com`;
- **Sandbox** — `test.salesforce.com`;
- **Custom URL** — your My Domain, for orgs that do not answer on either of the two.

A browser opens, you log in as usual, and the org appears in the list. Behind the scenes this is
`sf org login web` — the same auth you would get from a terminal, stored in the same place, usable from both.

Now mark one org as the **default target org** (right-click → *Set as Default Org*). Nearly everything else —
retrieve, deploy, schema, anonymous Apex — runs against that one.

## 4. Retrieve some metadata

Open the **Retrieve** section. It lists the metadata types in your org; expand one and you get its components.

Type in the filter box to narrow ~200 types down to the one you want. Tick a few components, press **Retrieve**, and
they land in your project's package directory.

First expand of a type takes a round trip to the org. After that it comes from a local inventory cache, so browsing
stays quick — [Retrieve](retrieve.md) explains when that cache is dropped.

## 5. Let the editor learn your org

Press **Refresh Schema** in the panel.

This asks the org what its objects and fields are and writes a set of **faux classes** — generated Apex stand-ins for
your SObjects, the thing that lets `Account.Industry` resolve and complete. Until you run it, a fresh project's `.cls`
files do not know your SObjects exist and will flag them.

It runs itself when you open the project and when you switch default org, so most days you never press it.
[Schema](schema.md) has the details.

## 6. Edit an Apex class

Open any `.cls`. What you should get:

- errors underlined as you type, from the real Apex compiler core running inside the IDE;
- `Ctrl+B` / `Ctrl+Click` to jump to a declaration, including into Salesforce's own types;
- `Alt+F7` to find usages of a method, field or type;
- `Ctrl+Q`-style hover for signatures and types;
- `Ctrl+Space` completion for members, types, SObject fields and SOQL.

[Apex](apex.md) goes through each of these and says where each one stops.

## 7. Deploy it back

With the file open, **Deploy Current File** in the panel — or turn on **Deploy on save** and let `Ctrl+S` do it.

Deploy on save fires when you press `Ctrl+S`, and only then. Pick a test level in the same section, and read failed
tests straight from the console — see [Deploy](deploy.md).

Everything that runs shows up in the **Console** section as a card: the command that ran, how long it took, what came
back. A compilation error in there is a link — click it and you land on the line.

## 8. Run its tests

Deploying a class is half the answer; the other half is whether its tests still pass. Click the run arrow in the
gutter next to an `@IsTest` class, and the results come back into a **Tests** tab beside the console — failures with
their stack traces, each frame a link into your code.

If the class has edits you have not deployed, SFellow offers to deploy them first: a test run executes what is in
the org. Coverage and the per-test debug log are a click away — see [Apex tests](tests.md).

## Where to go next

- Working against several orgs a day → [Orgs](orgs.md)
- Pulling down a large package → [Retrieve](retrieve.md)
- Writing LWC → [LWC, Aura, Visualforce](lwc-aura-visualforce.md)
- Chasing a bug through a debug log → [Debug logs](logs.md)
- Something is not working → [Troubleshooting](troubleshooting.md)
