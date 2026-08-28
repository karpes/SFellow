# Troubleshooting

## "Salesforce CLI not found"

SFellow looks for `sf` on your `PATH` and in the usual install locations. When it cannot find one, the panel says so
and opens its **Salesforce CLI** section, where you can point at the executable yourself — type the path or use
**Browse** (a file or a folder both work).

Check the obvious first:

```
sf --version
```

in a terminal *started the same way you start your IDE*. A `PATH` set in `~/.zshrc` is not necessarily a `PATH` your
IDE inherits when launched from a desktop icon.

After you set a path by hand, SFellow verifies the version and restarts the panel flow — no IDE restart needed.

## The panel is empty, or there is no SFellow tool window

The project needs an `sfdx-project.json` at its root. That file, not the folder name, is what makes it a Salesforce
project.

## My SObjects are all flagged as unknown

The schema has not been generated for this org. Press **Refresh Schema** in the panel and wait for it to finish; a
large org takes about a minute. See [Schema](schema.md).

If it has been generated and a *particular* field is still unknown, it is a field added to the org after the last
refresh. Refresh again.

## Apex features do nothing at all

The Apex engine needs a component that the plugin downloads on first use (Salesforce's compiler core; the licence
lets us download it, not ship it). If that download failed — offline, proxy, firewall — the panel says so and offers
**Retry**.

## Another Salesforce plugin is installed

Disable one of them. An extension belongs to exactly one file type in the IDE, so if another Apex plugin is
installed, one of the two claims `.cls` and the other goes inert — and which one wins is not something you get to
choose. The editor you end up with may not be the one you think you are using.

## Highlighting is plain text and nothing works

Check the build has not expired: **Settings → Plugins → SFellow** shows the version, and an expired build says so on
startup. See [Beta builds](beta-builds.md).

## Completion offers nothing in one particular file

Look at the top of the editor. If SFellow says completion in this file is limited, that is deliberate and the notice
names the measured cost of analysing the file. It happens in files that are expensive to analyse — usually because of
how much they reference rather than their length. Diagnostics, go to declaration, hover and find usages still work in
that file, and other files are unaffected.

## Deploy fails with a conflict

Somebody changed that component in the org after you last retrieved it. Either retrieve their version and merge, or
tick **Ignore conflicts** if you are certain yours should win. SFellow will not choose for you.

## Where the log is

**Help → Show Log in Explorer / Finder / File Manager** — the item is named after your file manager — opens the
folder with `idea.log`. To send it, **Help → Collect Logs and Diagnostic Data** packs the logs into a zip.

Lines from SFellow carry `dev.karpes.sfellow`. When reporting a bug, that file plus your IDE version and the SFellow
build number is usually enough to work with.

Lines that name another plugin as the culprit — `Plugin to blame: …` — are that plugin's, not ours, even when they
show up while you are using SFellow.

## Reporting

[Open an issue](https://github.com/karpes/SFellow/issues). Include:

- IDE and version (**Help → About**);
- SFellow build number (**Settings → Plugins**);
- what you did, what you expected, what happened;
- the relevant part of `idea.log`.
