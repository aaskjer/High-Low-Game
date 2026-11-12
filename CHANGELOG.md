# Changelog

Releases are in the [release notes](https://github.com/aaskjer/High-Low-Game/releases).
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [2.3.2] - 2026-11-12

### Added

- **aaskjer on Twitch** is back among the links of the About page.

### Changed

- **The update question says when Streamer.bot needs a restart.** A newer UIFramework can be used at once only
  while none is running in your Streamer.bot; otherwise it takes effect after a restart. The dialog now says which
  of the two it is, and after such a download a note says it again: restart when it suits you, everything goes on
  as before until then.
- **Closing the update question means "not now".** *Yes* takes the new UIFramework, *No* skips that version, and
  *Cancel*, the X and Esc ask again at the next open. Closing the dialog used to skip the version for good.
- **A skipped version is skipped in every game.** It is kept once, in `UIFramework\loader.json` beside
  Streamer.bot, and so is `"autoUpdate": false`. What a game's `uiframework.layout.json` holds is still read.
- The settings action is 0.3.1, the host block UIFramework 1.9.0's. Nothing in your settings changes.

### Fixed

- **A download GitHub does not deliver is tried three times** before the settings action gives up.
- **No answer from the game shows as no answer.** A Try button said "done" and a table showed as empty when the
  game action did not answer.
- **A late answer is not taken for the next one.** Every request to the game has a variable of its own.

## [2.3.1] - 2026-11-12

### Fixed

- **The settings action passes over a UIFramework it is too old for.** Every game in a Streamer.bot shares the
  installed UIFramework.dll. Should a later one need a newer settings action than this game's, the action now
  leaves that file alone and opens the window with an older one that fits, with a line in the log; it used to
  load whatever was newest. (Settings action 0.2.1.)
- **The update notice works with a UIFramework.dll you put in by hand.** A file saved from the browser carries
  Windows' "downloaded from the internet" mark, and the game did not load it: the notice at Streamer.bot's start
  never came. A file damaged since its download is no longer loaded for it.

### Changed

- The host block is UIFramework 1.8.4's. Nothing in your settings changes.

## [2.3.0] - 2026-11-08

### Added

- **Tells you about updates.** Once per Streamer.bot start, about 20 seconds in, one notice names new releases of
  this game, of the other UIFramework games and of UIFramework: in every chat whose broadcaster account is
  connected (Twitch, YouTube, Kick), or as a Windows notification while none is. The links are in Streamer.bot's
  log. *Tell me about updates* on the About page turns it off for this game. The game action is precompiled on
  application start, so the notice starts with Streamer.bot.
- The host block is UIFramework 1.4.0's; the settings window offers the newest UIFramework on its next open.

## [2.2.0] - 2026-11-07

### Added

- **A Log page.** The game writes a log file per day, `Chat Games\Logs\HLG-log-yyyy-MM-dd.txt`: every settled guess
  with both numbers, the bet and the points that moved, every new number from `!highlowsetup` and every refunded
  redemption. The settings window's new Log page reads it, with filters by result, platform and day; *Write a log file
  per day* on that page turns it off.
- **A tour of the settings window.** The first time the window opens, a short tour rings one part after the other
  (the pages, saving, the customise mode) and says what it does; the **?** at the top right shows it again.
- **UIFramework 1.0.0.** Problems the window finds sit behind a red **i** in its header instead of on the About or
  Log page, and *How to play*, *Log* and *About* sit together at the foot of the page list. The settings action
  offers the new framework on its next open.

### Changed

- **The settings action is UIFramework's stub 0.2.0.** When the game action hangs, the settings window waits 30
  seconds for its answer, then carries on and can be closed; before, it waited for good. A game that has not
  described itself for a minute no longer locks the settings until Streamer.bot restarts: the next run opens the
  window.
- The host block is UIFramework's current one (1.0.0). It names every type in full, so it no longer depends on the
  action's `using` lines, and it can declare a tour of the window. Nothing changes in the window.

## [2.1.0] - 2026-11-07

### Added

- **Custom triggers.** Every settled guess fires `HLG: Guess Won` or `HLG: Guess Lost`, and `HLG: Guess Settled`
  always (Custom > Chat Game > High-Low Game), with the guess as arguments: `guessOutcome`, `guessUser`,
  `guessUserId`, `guessPlatform`, `guessGuess`, `guessPreviousNumber`, `guessNewNumber`, `guessMode`, `guessStake`,
  `guessAmount`, `guessPreviousPoints`, `guessNewPoints`, `guessCurrency`, `guessFree`, `guessSessionGuesses`,
  `guessAlltimeGuesses`. `GetLastGuessResult`, run with an Execute C# Method sub-action on the game action, hands
  the same arguments to any other action. `HLG: New Number` fires when `!highlowsetup` draws one.
- **Free mode.** A switch on the Game page: nobody wins or loses points, redemptions included, the guesses still
  count. `!SetFreeHighLow` turns it on and `!EndFreeHighLow` turns it off (moderators; two new commands in the
  import, disabled until you enable them). The switch is written into the settings file, so the window's pill
  shows it, chat gets the new Started and Ended messages (Messages page, Free mode), and `HLG: Free Game Start`
  and `HLG: Free Game End` fire. An action of your own can do the same with an Execute C# Method on
  `StartFreeGame` or `EndFreeGame`.

### Changed

- The host block in `High-Low Game` and `High-Low Scoreboard` is UIFramework's current one (0.9.11). Nothing changes in
  the window; the block can now declare fields that follow a dropdown, a locked layout and masked fields.

## [2.0.0] - 2026-11-07

The settings window moved into [UIFramework for streamer.bot](https://github.com/aaskjer/UIFramework-Streamer.bot),
channel points got their stakes and refunds, and the scoreboards work.

### Added

- **A number from the start.** The game action compiles when Streamer.bot starts and draws a number for Twitch,
  YouTube and Kick, so nobody has to run `!highlowsetup` first. The command still draws and announces a new one;
  it is now limited to the Moderators group.
- **Channel point stakes.** Cost, Fixed, Input and Free, set on the Channel points page. Cost and Fixed spend the
  channel points as the stake and pay a correct guess in points, double on equal. Input takes a bet in the
  viewer's own points (a number, `all`, `half`, `third`, `quarter`, `random`, `50%` or `2k`); only a wrong
  `!equal` costs it. Free plays like the chat commands. Minimum and maximum bet apply to Input and Fixed.
- **Refunds.** Redemptions that do not end in a guess are refunded, played ones are marked as fulfilled, and the
  guess cooldowns also cover redemptions.
- **Reward trigger included.** The game action listens to every redemption and plays only the three rewards
  set in the window, so no trigger has to be added by hand.
- Equal chance, scoreboard size and the blocked users list are settings now.
- **German.** With the window's language set to `de` every setting, section and page of the window reads in
  German; the game ships its own texts with the settings table, the shared ones come from UIFramework.

### Changed

- **The settings window runs on UIFramework.** `[HLG] - .Settings` opens it from its Test trigger. The first time
  it asks whether to download `UIFramework.dll` from GitHub or to show the folder it belongs in. The window is
  built from the game's own settings table and window declaration, so the two can never disagree; the settings
  action is UIFramework's generic stub, the same file in every game, and needs no references of its own.
- **Points systems.** Tawmae's LOYALTY POINTS is recognised beside StreamUP's Currency Core: whichever is
  installed names the points variable and the points name, the window shows which, and the Points settings are
  the fallback.
- **Settings are kept.** `HLG-Settings.json` stays where it was, and the game reads the old setting names until the
  window saves them under the new ones. Cooldown messages written with `{0}` and `{1}` still work; new ones use
  `{user}` and `{seconds}`.
- Every platform plays. Leave one out by unticking its source on the commands.
- The scoreboards leave the broadcaster and the bot account out with two switches instead of one per platform.
- Payouts in channel points mode are paid in points, so `{currency}` is always the points name.

### Fixed

- The scoreboard commands answered nothing, and wins were never recorded, so every scoreboard was empty.
- Blocked groups had no effect.
- With Award points off, the outcome message still said points were won; a lost `!equal` deducted points without
  saying so, and could take a balance below zero.
- Cooldown messages with `{user}` or `{timeLeft}` were never sent.
- The outcome message no longer shows a double space or a space before the full stop when no points changed.
- Opening the settings did nothing in `[HLG] - .Settings`, and every chat command rewrote the settings file.

### Removed

- Trovo support.
- The platform switches, and the Channel Points Name setting.

## [1.0.0]

- Initial release.
