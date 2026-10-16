# Bloodborne on YouGame: message for the YouGame owner (14 Oct)

Hi Crunch, here is where we are after your 13 Oct reply.

## What we did with your answers

1. **Error 487 (F11).** `bb-probe.exe` was already linked without high-entropy ASLR
   (DllCharacteristics `0x8140`). In your unmodified launcher the process still gets
   high-entropy ASLR (flags `0xF`): your AppContainer turns it on, not your launcher. The
   main-thread stack (`0x5E_E880_0000`), the PEB and TEB, and four more 16 MB thread stacks land
   inside the window the port must reserve (`0x10_0000_0000`–`0xFC_0000_0000`), so it fails with
   487. The heap lands above the window and is not the problem. In the same AppContainer with
   only `PROCESS_CREATION_MITIGATION_POLICY_HIGH_ENTROPY_ASLR_ALWAYS_OFF` added, the window is
   empty and the full game runs. **Please add the opt-out you offered.** We have added no fields
   to `yougame-native.json`.
2. **Saves.** Each save goes up about 1 s after the game writes it: one upload per burst, never
   mid-write. We measured this on the real game. At start, the newer copy wins by the sync note.
   We no longer depend on quit.
3. **Server block.** `players: 50` and `tick: 1`. New players fill a world to 40, then move to
   the next shard. Our client sends at most 110 messages a second, pings included.
4. **Relay frames.** Text only, with P2P as base64 in JSON.
5. The listing stays private, and we test offline.

**F2 (base-game picker).**

- `eboot.bin` 1.09 (CUSA03173, Europe): **93,825,704 bytes**, SHA-1
  **`4b4a8ee8b7cbf852f89314a135293b0a38a06b0c`**.
- Dump tools wrap the executable differently, so the file hash can differ for the same game.
  The SHA-256 of the loaded image is the same whatever tool made the dump:
  `071df19c8880086d97182dbc057bc8cb37badaca57d9112683836b24a0444c0a`.
- The port needs read-only access to the whole folder holding `eboot.bin` and writes nothing
  there. From boot into the world it read 551 of the dump's 28,844 files, and more as the player
  reaches each area.

**Network-only plan.** We are ready for the bridge call that opens sockets. The game's notes,
bloodstains and ghosts used to need an outside server (The Hunter's Dream). The game now plays
online against our own Server Lite world's community server instead, with login, notices and the
lists working. Writing notes, bloodstains and ghosts is next.

## Questions

1. When can the ASLR opt-out ship? It is the only thing stopping the game inside your app.
2. Will you approve the build for online play (F0) once we upload it to the private listing?
3. Can you confirm a **privately** launched listing gets its Server Lite world (F4)?
4. Is an allow-listed HTTPS host per listing possible while we finish moving community data into
   the world? If not, we go world-only, which is our plan anyway.
5. When will the bridge call for room and world sockets, with its protocol and C client, be
   published? We would like to be its first user.
6. Is there a rough date for the PS4 base-game picker (F2)?
7. Content: is a listing that needs a player-owned decrypted PS4 dump acceptable when no game
   data ships? Is there a rule on titles whose trademark owner has issued takedowns over the
   name? Sony's 2025 notice targeted "Bloodborne".

## Blocks

| Block | Owner | Effect |
| --- | --- | --- |
| ASLR opt-out (F11) | YouGame | The game cannot start inside the YouGame app (error 487). Everything else is done |
| Online approval (F0) | YouGame | A new Windows build runs offline until approved |
| Bridge socket call | YouGame | Needed once builds lose direct internet |
| Base-game picker (F2) | YouGame | Until then, players copy their dump into the game's data folder |
| Community writes (notes, bloodstains, ghosts) | Us | One test session on our side; not blocking upload |

## What is needed to upload right now

Both files are built, verified and scanned (no game data). Neither has been uploaded.

1. **Native build:**
   `C:\Users\Johnn\Downloads\MELEE\J-LAY\HDR-Kazuya-Melee\ADOBE RUST TOOLS\BLOODBORNE-YOUGAME\dist\Bloodborne-YouGame-0.1.0.zip`
   (117.9 MB, SHA-256 `e15816af0b1a4c3a7ba1583944e4abc5f716a75cfd3f1d637993c58d0f2ea47e`).
   Upload it under the private listing's **Manage → Desktop builds**.
2. **Web build** (it carries the Server Lite world):
   `C:\Users\Johnn\Downloads\MELEE\J-LAY\HDR-Kazuya-Melee\ADOBE RUST TOOLS\BLOODBORNE-YOUGAME\dist\Bloodborne-YouGame-web-0.1.0.zip`.
   Upload it as the listing's game build.
3. **A private listing** on your YouGame account. Create it if it doesn't exist.
4. **Optional, for me to upload for you:** sign in to the YouGame MCP. In a terminal, run
   `claude`, then `/mcp`, choose yougame and sign in. Then tell me to go ahead.

What to expect after uploading: the build runs **offline** until YouGame approves it (F0). It
stops at error 487 until the ASLR opt-out ships (F11). Uploading now gets the listing and the
world in place, so both fixes take effect the moment YouGame ships them.
