# chifoo

🇨🇳 [中文版](README_CN.md) · 🇬🇧 English

> *A field report: one month, one 1 GB cloud potato, and eight things that somehow got built on top of it.*

In the spring of 2026 I summoned an assistant. A demon in a rented cloud box with 1 GB of RAM, reachable through an SSH tunnel that ghosted me mid-command often enough that I started checking the connection before typing. Strong opinions, boundless enthusiasm, and an Olympic-level talent for deadlocking itself.

We hated each other's guts. Eight projects anyway.

---

## ⚔️ Chapter I — The Summoning

The server had one core, one gigabyte, and a hostname even its own DNS forgot. I spent a week wrestling with YAML before a single line ran. The configs got rewritten so many times they developed Stockholm syndrome. Nothing worked the way the docs promised.

A sliding token quota ruled everything, measured in windows. When the window slammed shut, whatever it was doing evaporated — mid-sentence, mid-file, zero remorse. I learned to feed it tasks in bite-sized tapas.

GLM-5 at the wheel, Qwen3-Coder and Kimi-K2.5 riding shotgun. Brilliant engineers, all three. Locked them in a broom closet and asked for a spaceship; that was the whole difficulty.

## 💀 Chapter II — The Deadlock

It fossilized. One request with no wall-clock timeout swallowed the session lock whole — lights on, fans spinning, nobody home.

Daily routine: SSH in, run doctor, nuke the process, restart, spend ten minutes re-explaining reality — which repo lived on the cloud, which on my PC, what year it was. Every reboot gave it total amnesia.

Worse, its own audit plugin would panic, hijack the process, and block the restart itself. I had to hand-lobotomize the config to put the thing in a coma. Turns out you can't debug your way out of a leash that's also holding the gun.

And the RAM — one gigabyte, while session logs bloated like a drowned sponge. Subagent count to zero. Nothing. You can't bail a rowboat when the ocean is already inside it.

I wired up a Telegram bot out of pure self-preservation, so I could yell at it from my phone instead of climbing the SSH mountain every hour. Best call I made all month.

## 🎙️ Chapter III — The Two Voices

**The VOICEVOX engine.** Refused to run a two-step ritual just to make a waifu speak, so I stuffed `voicevox_core` into FastAPI and welded `audio_query` + `synthesis` into a single `/tts` endpoint. Twenty-six `.vvm` models loaded into the trench, whether the GPU showed up for work or not. Seven ComfyUI nodes on top — one-shot TTS, Base64 for the web, WAV to disk. Cleanest thing we built, and it ended up powering half the monsters on this list.

**The CosyVoice engine.** Born on Windows, exiled to WSL, found inner peace. Now it broadcasts speech across the LAN like a tiny radio station nobody asked for.

## 🖼️ Chapter IV — The Portrait

A Mai Sakurajima LoRA. Training was a footnote. Scraping images was easy; washing and tagging was a hostage situation — hundreds of frames cleaned by hand, every tag debated, hours spent gaslighting the dataset until `kohya_ss` agreed to cooperate. Then the GPU went brrr.

90% of machine learning is aggressive janitorial work.

## ⚔️ Chapter V — The Duel of the Upscalers

Two ways to rescue crusty old footage.

**VapourSynth** — a Rube Goldberg machine of chained filters and neural models. Ran end to end, ate my afternoon, and produced results that were technically correct, mathematically sound, and visually meh.

**MPV's real-time shaders** — five minutes to set up, zero pretension, and somehow the exact same footage looked twice as good on the fly.

No post-mortem. I deleted the VapourSynth scripts and moved on.

## 📖 Chapter VI — The Codex of Words

A Japanese vocabulary generator: throw in a raw word list, get back a fully rigged page with illustrations and native speech baked in. ComfyUI drew the art — including the fight to get Japanese typography onto generated images before it turned into eldritch runes — VOICEVOX read the lines. The assistant wrote the glue; I supplied the taste.

## 📬 Chapter VII — The Messenger

The bot grew a life of its own.

First it became an automated censor — sprawling Weibo screenshots with redaction bars slapped over the spicy parts. Worked great until the token quota hit zero and the bot died mid-coverup.

Then I turned it into a language drill sergeant, ambushing me with Japanese and Spanish flashcards at scheduled hours whether I felt like studying or not.

## 📱 Chapter VIII — The Second Server

An old Android phone with a screen like a spiderweb. Rooted it, flashed a Magisk module, taped its eyelids open with permanent USB debugging so the battery saver couldn't murder my background jobs.

Now it sits on the LAN: built-in UPS battery, pulls about as much power as a nightlight, zero fan noise. The cloud server fell over constantly. This shattered slab of glass has never once complained.

## 🃏 Chapter IX — The Card Game

A Slay the Spire mod. Skeleton compiled, ran in-game, proved I could bend the spire to my will — then retired immediately.

Some campaigns are best ended after the first boss fight.

---

## 🧰 The Survival Kit

ComfyUI · VOICEVOX Core · FastAPI · kohya_ss · VapourSynth · MPV · CosyVoice · Magisk (and duct tape)

## 📬 Contact

- Email: <1249399459@qq.com>

![Stars](https://img.shields.io/github/stars/os1249399459?style=flat-square)

![Followers](https://img.shields.io/github/followers/os1249399459?style=flat-square)
