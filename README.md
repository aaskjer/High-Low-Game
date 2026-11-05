<h1 align="center">High-Low Game</h1>

<p align="center">
  <b>Higher, lower or the same? A quick guessing game for your chat on Twitch, YouTube and Kick.</b><br>
  Played with chat commands or Twitch channel points, with session and all-time scoreboards.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/platforms-Twitch%20%7C%20YouTube%20%7C%20Kick-9146FF" alt="Platforms">
  <img src="https://img.shields.io/badge/tool-streamer.bot-0b73ff" alt="Streamer.bot">
  <img src="https://img.shields.io/github/license/aaskjer/High-Low-Game" alt="License">
  <img src="https://img.shields.io/github/v/release/aaskjer/High-Low-Game" alt="Release">
  <img src="https://img.shields.io/github/downloads/aaskjer/High-Low-Game/total" alt="Downloads">
</p>

<p align="center">
  <a href="https://github.com/aaskjer/High-Low-Game/releases"><b>Download</b></a> &nbsp;·&nbsp;
  <a href="Setup-Guide.md"><b>Setup Guide</b></a> &nbsp;·&nbsp;
  <a href="FAQ.md"><b>FAQ</b></a> &nbsp;·&nbsp;
  <a href="Import-String.md"><b>Import String</b></a>
</p>

---

## 📖 Overview

High-Low Game is a chat game for Streamer.bot. There is always a number from 1 to 100 waiting, drawn when
Streamer.bot starts. Viewers guess whether the next one will be higher, lower or the same, and the answer names
both numbers. The new number is what the next guess is measured against.

```
!high
→ Hey Nova! Previous: 42, New: 77. Your guess '!high' was correct 🙂 won 1.234 Points. Session: 3 guesses, All-time: 57.
```

## ✨ Highlights

- 🎲 **Nothing to set up before playing.** A number is ready from the first second. `!highlowsetup` is there for
  moderators who want to announce a fresh one.
- 💰 **Low stakes in chat.** A correct `!high` or `!low` pays the win amount and a wrong one costs nothing. `!equal`
  is the risky guess: it pays double, and a miss costs the win amount.
- 💜 **Channel points on Twitch.** Three rewards for high, low and equal. The stake can be the reward's cost, a fixed
  bet, a bet the viewer types (a number, `all`, `half`, `third`, `quarter` or `random`), or free play like the chat.
- ↩️ **Refunds that hold up.** A redemption that does not end in a guess (blocked viewer, cooldown, refused bet,
  error) gets its channel points back, and every played one is marked as fulfilled.
- 🏆 **Scoreboards.** `!hlgsession`, `!hlgalltime` and `!hlgpersonal`, with wins, guesses and win rate.
- 🆓 **Free mode.** A switch in the window or `!SetFreeHighLow` / `!EndFreeHighLow` in chat (moderators): nobody
  wins or loses points, with a message and a custom trigger each.
- 🔔 **Hooks for your own actions.** Custom triggers for every won, lost and settled guess with the guess as
  arguments, for a new number and for Free mode, plus `GetLastGuessResult` for an Execute C# Method.
- ⚙️ **One settings window.** Built on [UIFramework for streamer.bot](https://github.com/aaskjer/UIFramework-Streamer.bot),
  the window the other chat games share: eight pages, light and dark themes, and every chat message with a live
  preview.

---

## Credits

- **Author:** [aaskjer on Twitch](https://twitch.tv/aaskjer) · [aaskjer.github.io](https://aaskjer.github.io/)
- **Built for:** [Streamer.bot](https://streamer.bot) by [nate1280](https://www.patreon.com/c/nate1280/home)
- **Works with:** [Currency Core by StreamUP](https://streamup.tips/product/currency-core)
- **Thanks:** YOU ♡

None of the projects above is affiliated with or endorses High-Low Game.
