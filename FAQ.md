# ❓ High-Low Game — FAQ

## 🛠️ Setup

### Do I have to run `!highlowsetup`?

No. Each platform has its number from the first start on, and it is kept, also when Streamer.bot restarts.
`!highlowsetup` draws a new one and announces it in chat, for when you want to show viewers where the game stands.

### The settings window does not open.

Run the **Test** trigger of `[HLG] - .Settings` and check the Streamer.bot log. On the first run it asks to
download `UIFramework.dll`; if you chose *No*, it opened `UIFramework\lib`. Put the DLL into a folder named after
its version there (`UIFramework\lib\<version>\UIFramework.dll`) and run the trigger again. *Cancel* leaves a warning in the log and nothing else.

### Nobody can play.

The commands are imported disabled. Enable them under **Commands**, group `[HLG] High-Low Game`: nine in all,
the seven to play and to show the scoreboards, and `!SetFreeHighLow` / `!EndFreeHighLow` for moderators.

### Can I rename a command or give it an alias?

Yes. The game knows its commands by their ID, so `!high` can become `!hoch`, or get `!h` beside it, in
Streamer.bot's **Commands** and still plays.

### I came from version 1. Are my settings gone?

No. The game reads `HLG-Settings.json` with the old setting names until the window saves it again. Two things
are reset: the per-platform "include bot/broadcaster" switches became two switches that leave both out, and the
platform switches are gone (untick a command's source instead). Trovo is no longer supported.

## 💰 Points

### Where do the points come from?

From the user variable named under **Points variable** (default `points`), the same one
[Currency Core](https://streamup.tips/product/currency-core) uses. With Currency Core or
[LOYALTY POINTS](https://tawmae.xyz/loyalty-points) installed, its settings win; the Game page shows which one.

### Can a viewer lose points with `!high` or `!low`?

Not in chat. Only a wrong `!equal` costs points, the win amount. A balance never goes below zero.

### Can I play without points?

Turn off **Award points** on the Game page. Guesses still count for the scoreboards.

### Can a moderator make the game free for a while?

Yes: `!SetFreeHighLow` turns Free mode on and `!EndFreeHighLow` turns it off. The two commands come with the
import, disabled and for Moderators. The switch is written into the settings file, so the window's pill shows it,
chat gets the **Started** or **Ended** message, and your own actions can listen to `HLG: Free Game Start` and
`HLG: Free Game End`. An action of your own can do the same with an Execute C# Method on `StartFreeGame` or
`EndFreeGame` of the game action.

### Can my own actions react to a guess?

Every settled guess fires `HLG: Guess Won` or `HLG: Guess Lost`, and `HLG: Guess Settled` always (Custom > Chat
Game > High-Low Game), with the guess as arguments (`guessOutcome`, `guessUser`, `guessGuess`, `guessNewNumber`,
`guessAmount`, `guessNewPoints`, ...). `GetLastGuessResult`, run with an Execute C# Method sub-action on the game
action, hands the same arguments to any other action; `HLG: New Number` fires when `!highlowsetup` draws one.

## 💜 Channel points

### A redemption was not refunded.

Twitch only refunds a redemption while it waits in the reward request queue. Turn **Skip Reward Requests Queue**
off on the three rewards. The log says "Twitch refused to refund" when this is the cause.

### Other rewards stopped working.

They should not be touched: the game listens to every redemption but plays only the three reward IDs in its
settings and leaves the rest alone. If one of yours was refunded, check that its ID is not pasted into the window.

### The chat commands do nothing on Twitch.

**Guess with channel points** is on. Twitch guesses then come from the rewards only; YouTube and Kick keep the
chat commands.

## 🏆 Scoreboards

### My old scoreboard is empty.

Version 1 never recorded wins. Guesses from before still count; wins are counted from version 2 on.

### What is a session?

Everything since Streamer.bot last started. Session stats are not saved; all-time stats are.

### Two players have the same number of wins. Who is first?

The one who needed fewer guesses. The same wins in the same number of guesses share a place.

## 💬 Messages

### Can the outcome message be in my language?

Yes, all of it. The message itself is on the Messages page, and so are its **Outcome words**: what `{result}`,
`{emoji}`, `{sign}` and `{pointsSection}` say (*correct*, *incorrect*, *won*, *lost*, ...).

### A long message is cut into two.

On purpose: YouTube takes 200 characters per message, Twitch and Kick 500. A longer message goes out in pieces,
cut between words.
