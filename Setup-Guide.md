# Import

1. Copy the whole string from [Import-String.md](Import-String.md), or take `HighLowGame.sb` from the
   [latest release](https://github.com/aaskjer/High-Low-Game/releases).
2. In Streamer.bot click **Import**, paste the string (or drop the file) and import everything.

You get three actions in the group `[HLG] High-Low Game`:

| Action | What it does |
| --- | --- |
| `[HLG] - High-Low Game` | The game: `!high`, `!low`, `!equal`, `!highlowsetup`, `!SetFreeHighLow`, `!EndFreeHighLow` and the channel point rewards |
| `[HLG] - Scoreboard` | `!hlgsession`, `!hlgalltime`, `!hlgpersonal` |
| `[HLG] - .Settings` | Opens the settings window from its Test trigger |

Coming from 1.x: import over the old actions. `HLG-Settings.json` stays where it is and is read as before.
Tested with Streamer.bot 1.0.7.

## Enable Commands

Commands arrive disabled. Open **Commands**, group `[HLG] High-Low Game`. There are nine: `!high`, `!low`,
`!equal`, `!highlowsetup`, the three scoreboard commands and the two for Free mode. Enable the ones you play with.
While you are there:

- `!highlowsetup` is limited to the **Moderators** group. It is optional; the game runs without it.
- `!SetFreeHighLow` and `!EndFreeHighLow` (Moderators too) switch Free mode from chat. Optional as well; enable
  them if you want them.
- Every command listens on Twitch, YouTube and Kick. To leave a platform out, untick its source on the commands.
- A command may be renamed or get aliases; the game knows its commands by their ID.

# Setup

Open `[HLG] - .Settings`, right-click its **Test** trigger and choose **Test Trigger**.

The first time, a dialog asks whether to download `UIFramework.dll` from GitHub (checked against its published
SHA-256) or to show the folder it belongs in, `UIFramework\lib\<version>\` next to Streamer.bot. Nothing is
downloaded without your click. When a newer UIFramework comes out, opening the window offers it and says whether
Streamer.bot has to be restarted for it.

Everything is saved to `Chat Games\High-Low Game\HLG-Settings.json` in the Streamer.bot folder.

## Game

![Game page](Assets/setup-guide/game.png)

- **Award points**: off, and nobody wins or loses points. Guesses still count for the scoreboards.
- **Free mode**: the same, but meant to be switched for a while: `!SetFreeHighLow` and `!EndFreeHighLow` turn it
  on and off from chat, with the Started and Ended messages, and the window's pill shows it.
- **Win amount**: paid for a correct `!high` or `!low`. A correct `!equal` pays double, a wrong `!equal` costs the
  win amount. A wrong `!high` or `!low` costs nothing.
- **Equal chance**: how often an `!equal` guess draws the same number again. Every other draw is a free pick from
  1 to 100.
- **Points variable** and **Points name**: where points are kept and what they are called in chat. With
  [Currency Core](https://streamup.tips/product/currency-core) or [LOYALTY POINTS](https://tawmae.xyz/loyalty-points)
  installed, its own settings are used instead.

## Channel points

![Channel points page](Assets/setup-guide/channel-points.png)

Twitch only. YouTube and Kick always play with the chat commands.

1. On Twitch, create one custom reward each for high, low and equal. Leave **Skip Reward Requests Queue** off,
   or Twitch cannot refund a redemption that does not play.
2. Paste the three reward IDs here and turn on **Guess with channel points**. From then on `!high`, `!low` and
   `!equal` do nothing in Twitch chat.
3. Pick the **Stake**:

| Stake | What is bet | Correct guess | Wrong guess |
| --- | --- | --- | --- |
| Cost of the reward | the channel points spent | the reward's cost in points, double on equal | nothing more |
| Fixed bet | the channel points spent | the **Fixed bet** in points, double on equal | nothing more |
| Viewer types a bet | the viewer's own points, typed into the redemption | the bet, double on equal | `!equal` costs the bet, `!high`/`!low` nothing |
| Free, like chat | the channel points spent | the win amount, double on equal | `!equal` costs the win amount |

For a typed bet the reward needs **Require Viewer to Enter Text**. Viewers can type a number, `all`, `half`,
`third`, `quarter`, `random`, a percentage like `25%` or a short form like `2k`. A plain number is a whole number of
points, with or without thousands separators (`1500`, `1.500`, `1,500`); `1.5` is refused. A bet they cannot afford
is refused. **Minimum bet** and **Maximum bet** apply to typed and fixed bets; 0 turns them off.

**Refund redemptions that don't play** gives the channel points back whenever a redemption ends without a
guess: blocked viewer, cooldown, refused bet, an error, or one of the three rewards redeemed while **Guess with
channel points** is off. Played redemptions are marked as fulfilled.

## Cooldowns

![Cooldowns page](Assets/setup-guide/cooldowns.png)

One global and one per-viewer cooldown each for `!high`, `!low`, `!equal` and the three scoreboard commands, in
seconds. Saving writes them onto the commands. The three guess cooldowns also cover the matching rewards; a
redemption that comes in during one is refunded. `!highlowsetup` and the Free mode commands have no cooldown here;
set one on the command itself if you want it.

## Access

![Access page](Assets/setup-guide/access.png)

**Blocked users** and everyone in the **Blocked groups** (Streamer.bot's Settings > Groups) are ignored when they
guess or run `!highlowsetup`, with no reply in chat, not even a cooldown message. Their redemptions are refunded.
The scoreboard commands stay open to them.

## Scoreboard

![Scoreboard page](Assets/setup-guide/scoreboard.png)

How many places `!hlgsession` and `!hlgalltime` list, and whether the broadcaster and the bot account are left
out. They still play; they are just not ranked, and asking for a board shows them their own stats. Most wins come
first; with as many wins, fewer guesses. The same wins in the same number of guesses share a place.

## Messages

![Messages page](Assets/setup-guide/messages.png)

Every chat message with its placeholders and a live preview, plus the sender switches: bot account or
broadcaster, and `/me` on Twitch. An empty message is not sent.

Under **Outcome words** are the words the outcome message is built from: what `{result}` says after a right and
a wrong guess, what `{emoji}` shows, `{sign}` for won and lost points, and the **Points part** that
`{pointsSection}` reads. Translate them along with the message.

A message longer than the platform takes goes out in pieces, cut between words: 200 characters on YouTube, 500 on
Twitch and Kick.

## Log

![Log page](Assets/setup-guide/log.png)

Every settled guess, every new number from `!highlowsetup` and every refunded redemption, one file per day in
`Chat Games\Logs\HLG-log-yyyy-MM-dd.txt`. Filter by result, platform and day, or search; a row shows its whole line
below the table. **Write a log file per day** turns the file off.

## How to play

![How to play page](Assets/setup-guide/how-to-play.png)

## About

![About page](Assets/setup-guide/about.png)
