# Bloodborne on YouGame: private test, guide for testers

**This is a private test build, for invited testers only.** We own none of it: Bloodborne belongs to
Sony Interactive Entertainment and FromSoftware, and the port, libraries and mods this build runs
belong to their authors (the game page and `CREDITS.md` in the build credit each of them). We claim
no rights to any of it. It is listed on YouGame as "a game of your own" only because YouGame's
catalog cannot list the PlayStation 4 game yet.

**Bring your own legally obtained copy.** No game files are included, hosted or linked, by us or by
YouGame. You need a dump you made yourself from a copy of Bloodborne you own. Please do not ask
anyone in the test where to get one.

## What you need

- Windows 10 (1903 or later) or 11, 64-bit; a Vulkan 1.3 graphics card with a current driver; about
  6 GB of free memory (10 GB for 1440p or 4K).
- The YouGame desktop app, signed in.
- Your own dump of **Bloodborne for PS4, game version 1.09**: the folder that holds `eboot.bin`,
  `sce_module`, `sce_sys` and `dvdroot_ps4` (about 31 GB).

## Getting in

1. Open the invite link you were sent, signed in to YouGame. You become a tester and the game appears
   under **Saved**.
2. Open it in the desktop app and press **Play native**. YouGame warns that the program is the
   creator's, not YouGame's; accept to download it (119 MB) and run it.
3. The first time, the game shows a message with the folder it reads your copy from (inside the
   app's data folder for this game, ending in `\game`). Copy your dump's folder there, so that
   `...\game\eboot.bin` exists, and press Play again.
4. From the title screen on it is the game you know. The first start takes a little longer while it
   prepares.

## Seamless Co-op (optional)

Seamless Co-op (BBSC, by CLS_AMG) keeps a co-op session alive through deaths, lamps, bosses and area
changes, for up to five hunters. It is **off** until you turn it on, and only hunters who turned it on
are matched with each other. Either:

- on the game's web page (open the game in a browser and use the Seamless Co-op switch), or
- put a file named `bbsc.json` next to the `game` folder from step 3, containing
  `{"enabled": true}`, and start the game again.

## Online

- **Until YouGame approves this build for online play, it plays offline** (solo works fully). We will
  tell you when online is on.
- Then: ring the Beckoning Bell to call for help or the Small Resonant Bell to answer one; press
  **F8** in the game to invite a YouGame friend; YouGame lobbies are coming (host one, friends or the
  public search fill it, and you can talk in it).

## The online self-test (works before online is approved)

The game's page links an **online self-test** (`diag/index.html`, also reachable from the game's
web page in a browser). It plays one hunter's short session against this game's own world server
on YouGame, without the game: joining, matchmaking, summon signs, notes and bloodstains, moving
between shards, and the round-trip time. It ends with one line, `WORLD CHECK PASS` or `FAIL`, and a
report to copy and send us.

**Lobby test with a friend:** both open the self-test with the same code at the end of the address
(`diag/index.html#lobby=yourcode`, 4 to 64 letters, digits, `-` or `_`). One of you must come out as
the lobby's **host** and the other as a **guest** of that host. Keep the code to yourselves: it is the
way into your lobby.

## Your data

Game files never leave your PC. Your save files go to your own YouGame account's cloud saves. When
you play online, what the game itself shares goes to this build's world on YouGame, where the other
testers (and the build's operator) can see it: your hunter name (your YouGame name), notes you write
(kept 30 days), bloodstains (7 days), a short wandering-ghost recording (1 day), your messenger look
and chalice glyphs you share (90 days), and an anonymous count of lamp visits (30 days).

## When something goes wrong

Send the two log files from the game's data folder, `logs\ygboot.log` and `logs\last_run.log`, and
say what you did. They hold no game data; they do hold your PC's folder names.
