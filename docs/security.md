# Security and privacy

SFellow is a closed-source commercial plugin distributed outside JetBrains Marketplace. There is no marketplace
badge to lean on, so this page says what the plugin does — and, more usefully, how you can check it yourself
instead of taking our word for it.

## What leaves your machine: nothing

The plugin contains no network client code. No telemetry, no analytics, no usage reporting, no licence call-home.
The only outbound traffic from your machine is whatever **your own `sf` CLI** makes when you ask the plugin to
deploy, retrieve, run tests or fetch logs.

**Check it yourself.** Point a network monitor at your IDE and use the plugin. Five minutes, no trust required —
which is the point of saying it this way round.

## Credentials

The plugin never reads, stores or transmits your org credentials. Authentication lives in the `sf` CLI, where you
set it up yourself; the plugin runs CLI commands and parses their output. Connecting an org opens the same browser
login you would get from a terminal, and the result is stored in the same place.

It also goes one step further than abstaining: every CLI invocation is launched with `SF_DISABLE_TELEMETRY=true`,
so the plugin suppresses the CLI's own telemetry rather than merely declining to add its own.

## What it writes to your disk

Inside your project, under `.sfellow/`:

- the deploy baseline, so Changed Files can tell a reverted file from a modified one;
- anonymous Apex scripts you create;
- a marker recording which org the local schema was generated from.

Plugin settings live in the IDE's own configuration, like any plugin's. Nothing is written outside your project and
your IDE configuration.

## Third-party components

One: the Apex compiler core from Salesforce (`apex-jorje-core.jar`), under BSD-3-Clause. Its copyright notice and
disclaimer ship inside the plugin archive, as that licence requires.

## What is inside the archive

Two jars in `SFellow/lib/` — the plugin itself and the compiler core — and nothing else. `unzip -l` on the file you
downloaded should match that exactly.

Each build is published with the SHA-256 checksum of its archive in the release notes. Compare against the
checksum published **for that build** — builds are not byte-reproducible, so rebuilding the same version
elsewhere yields a different checksum over identical contents.

## Antivirus scanning

A release archive can be looked up on [VirusTotal](https://www.virustotal.com/) by its SHA-256 — the same
checksum published with the build. Where a report exists, the release notes link to it directly.

Worth knowing before you read one: release builds are obfuscated, and heuristics occasionally read obfuscated
bytecode as "packed". A lone heuristic hit from one engine out of seventy is that, not a finding. If you see
something that looks real, tell us — **karpes.dev@gmail.com** — rather than assume.

## The archive is signed

Release builds are signed with our own certificate, which protects the archive against being altered or substituted
after we published it.

Be clear about what that does and does not buy you: your IDE validates plugin signatures against JetBrains' own
certificate authority or a key you have added yourself, so a signature from us is not something the IDE can vouch
for on its own. It is an integrity measure, not a badge.

## The code is obfuscated, and why we say so

Member names in release builds are obfuscated. We state that up front rather than let a reviewer discover it and
wonder what is being hidden: SFellow is a commercial product distributed as a file, and obfuscation raises the cost
of lifting it wholesale. Class names and line numbers are deliberately preserved, so crash reports stay
diagnosable — send them even if the method names look scrambled, we can translate them back.

Obfuscation is a speed bump, not a security measure, and it is not a reason to trust us less. If your organisation
needs to read the code before adopting it, **we will arrange a source review under NDA** — ask.

## Compatibility verification

Each release is checked with the JetBrains Plugin Verifier against IntelliJ IDEA 2026.1, 2026.2 and 2026.3, and the
report is published with it: no compatibility problems, no internal-API usage.

To be precise about what that is: the Plugin Verifier checks **compatibility**, not security, and this is **not** a
JetBrains Marketplace approval — SFellow is not distributed through Marketplace.

## Questions

Anything unclear or anything you want to verify and cannot — email **karpes.dev@gmail.com**.
