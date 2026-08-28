# Deploy

Getting your changes into the org, and finding out quickly when they do not go in.

![Deploy with a failing test](img/deploy-failed-test.png)

## Deploying

Three ways, all running `sf project deploy start` underneath:

- **Deploy Current File** — the file in the editor;
- right-click in the project tree → **Deploy** — whatever you selected, one file or a folder;
- **Changed Files** — everything you have edited since the last deploy.

**What it does not do.** It does not resolve conflicts. If somebody changed the same component in the org, the deploy
fails on a conflict and you decide what to do — SFellow will not pick a winner for you.

## Changed files

![Changed files](img/deploy-changed-files.png)

A plain list of the files you have changed — **any** change at all, a whole new method or one stray space. Nothing
is judged or grouped: if you touched it, it is in the list.

Tick what you want and press **Deploy**. A file drops off the list once it has been deployed.

**When it helps.** Ten minutes of edits across four classes and a trigger, one deploy.

**What it does not do.** It watches your edits in this IDE, not git and not the org. A file changed by another tool is
not in the list.

## Deploy on save

Turn it on and `Ctrl+S` deploys the file you just saved.

Only `Ctrl+S` counts. The IDE saves files by itself all the time — when you switch windows, when you run something —
and none of those deploy anything.

**All changes**, next to the checkbox, widens it: a save deploys everything you have changed, not only the file in
front of you.

**When it helps.** A tight edit-and-check loop against your own sandbox or scratch org.

**Worth knowing before you turn it on.** On a shared sandbox every save of yours is immediately everyone's, including
the half-written version. Check which org the panel is pointed at.

## Test levels

![Test levels](img/deploy-test-levels.png)

Pick one before you deploy:

| Level | What Salesforce runs |
|---|---|
| No test run | nothing |
| Run specified tests | the classes you name |
| Run local tests | every test in the org except managed-package ones |
| Run all tests in org | everything, managed packages included |
| Run relevant tests | the tests Salesforce judges relevant to what you are deploying |

Production deploys require a level with real coverage; sandboxes do not. This is a Salesforce rule, not ours.

## Validate

**Validate** runs the whole deployment without committing it — compilation, tests, coverage — so you find out whether
a release goes in before it goes in.

**When it helps.** Rehearsing a production release, or checking a large change against a sandbox without leaving it
there.

## When tests fail

The console prints each failing test with its message and stack trace, and the stack frames are **links** — click one
and you are on the line in your class.

**What it does not do.** It does not show coverage numbers per class, and it does not tell you which line was not
covered. Salesforce reports that in the deployment result; surfacing it is not built yet.

## Deleting from the org

Delete a component's file in the project tree and SFellow offers to delete it from the org too
(`sf project delete source`). Say no and only the local file goes.

**What it does not do.** It does not delete in bulk from the tree, and it does not build a `destructiveChanges.xml`.
