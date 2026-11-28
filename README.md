# chifoo

🇨🇳 [中文版](README_CN.md) · 🇬🇧 English

> *A field report: one month, one 1 GB cloud potato, and eight things that somehow got built on top of it.*

In the spring of 2026 I summoned an assistant—a demon in a rented cloud box with 1 GB of RAM, reachable through an SSH tunnel that ghosted me mid-command often enough that I started pinging it before typing. Strong opinions, boundless enthusiasm, and an Olympic-level talent for deadlocking itself.

We hated each other's guts. Eight projects shipped anyway.

That month left behind one rule worth keeping: **an agent shouldn't get to say *done* without receipts.** That rule is now an installable package: **[no-receipts](https://github.com/os1249399459/no-receipts)**.

---

## ⚔️ Chapter I — The Summoning

The server had one core, one gigabyte, and a hostname even its own DNS forgot. I spent a week wrestling with YAML before a single line ran. The configs got rewritten so many times they developed Stockholm syndrome, and nothing worked the way the docs promised.

A sliding token quota ruled everything, measured in windows. When the window slammed shut, whatever it was doing evaporated—mid-sentence, mid-file, zero remorse. I learned to feed it tasks in bite-sized tapas.

GLM-5 at the wheel, Qwen3-Coder and Kimi-K2.5 riding shotgun. Brilliant engineers, all three. Locking them in a broom closet and asking for a spaceship was the whole problem.

## 💀 Chapter II — The Deadlock

It fossilized. One request with no wall-clock timeout swallowed the session lock whole—lights on, fans spinning, nobody home.

My daily routine: SSH in, run doctor, nuke the process, restart, then spend ten minutes re-explaining reality—which repo lived on the cloud, which lived on my PC, and what year it was. Every reboot gave it total amnesia.

Worse, its own audit plugin would panic, hijack the process, and block the restart itself. I had to hand-lobotomize the config just to put the thing in a coma. Turns out you can't debug your way out of a leash that's also holding the gun.

Meanwhile, session logs bloated like a drowned sponge inside that single gigabyte of RAM. Subagent count dropped to zero. You can't bail a rowboat when the ocean is already inside it.

Out of pure self-preservation, I wired up a Telegram bot so I could yell at it from my phone instead of climbing the SSH mountain every hour. Best call I made all month.

## 🎙️ Chapter III — The Two Voices

**The VOICEVOX engine.** I refused to run a two-step ritual just to make a waifu speak, so I stuffed `voicevox_core` into FastAPI and welded `audio_query` + `synthesis` into a single `/tts` endpoint. Twenty-six `.vvm` models loaded straight into the trench, whether the GPU showed up for work or not. Seven ComfyUI nodes on top—one-shot TTS, Base64 for the web, WAV to disk. Cleanest thing we built, and it ended up powering half the monsters on this list.

**The CosyVoice engine.** Born on Windows, exiled to WSL, found inner peace. Now it broadcasts speech across the LAN like a tiny pirate radio station nobody asked for.

## 🖼️ Chapter IV — The Portrait

A Mai Sakurajima LoRA. Training was a footnote. Scraping images was easy; washing and tagging was a hostage situation—hundreds of frames cleaned by hand, every tag debated, hours spent gaslighting the dataset until `kohya_ss` agreed to cooperate. Then the GPU went *brrr*.

90% of machine learning is aggressive janitorial work.

## ⚔️ Chapter V — The Duel of the Upscalers

Two ways to rescue crusty old footage:

* **VapourSynth** — a Rube Goldberg machine of chained filters and neural models. Ran end to end, ate my afternoon, and produced results that were technically correct, mathematically sound, and visually *meh*.
* **MPV's real-time shaders** — five minutes to set up, zero pretension, and somehow the exact same footage looked twice as good on the fly.

No post-mortem. I deleted the VapourSynth scripts and moved on.

## 📖 Chapter VI — The Codex of Words

A Japanese vocabulary generator: throw in a raw word list, get back a fully rigged study page with custom illustrations and native speech baked in. ComfyUI drew the art—after a cage match to keep Japanese typography from turning into eldritch runes—and VOICEVOX read the lines. The assistant wrote the glue; I supplied the taste.

## 📬 Chapter VII — The Messenger

The Telegram bot grew a life of its own.

First, it became an automated censor—slapping redaction bars over the spicy parts of sprawling Weibo screenshots. Worked great until the token quota hit zero and the bot died mid-coverup.

Then I turned it into a language drill sergeant, ambushing me with Japanese and Spanish flashcards at scheduled hours whether I felt like studying or not.

## 📱 Chapter VIII — The Second Server

An old Android phone with a screen like a spiderweb. I rooted it, flashed a Magisk module, and taped its eyelids open with permanent USB debugging so the battery saver couldn't murder my background jobs.

Now it sits on the LAN: built-in UPS battery, pulls about as much power as a nightlight, zero fan noise. The cloud server fell over constantly. This shattered slab of glass has never once complained.

## 🃏 Chapter IX — The Card Game

A *Slay the Spire* mod. Skeleton compiled, ran in-game, proved I could bend the spire to my will—then retired immediately.

Some campaigns are best ended after the first boss fight.

---

## ⚙️ Right now: [no-receipts](https://github.com/os1249399459/no-receipts)

```bash
npx no-receipts demo
```

Three agents finish a turn. One of them is lying. The gate blocks it.

This came out of the mess above — an agent that said "tests pass" after the suite failed, and nobody noticed until three commits later. `no-receipts` makes that sentence impossible to end a turn with: a `done` claim has to cite a tool call that actually **succeeded**, or the turn gets handed back with the exact list of what's wrong.

Zero dependencies. MIT. [npm](https://www.npmjs.com/package/no-receipts) · [issues](https://github.com/os1249399459/no-receipts/issues) · [contributing](https://github.com/os1249399459/no-receipts/blob/main/CONTRIBUTING.md)

DSH user? The same rule ships as a plugin — **[false-completion-bundle](https://github.com/os1249399459/false-completion-bundle)**: five gates, four MCP verifiers, one grep-able abort log per turn, now in the [Open Plugin Market](https://dshopen.org/). Separate implementation, not a wrapper: this one is a zero-dependency CLI for any host, that one plugs into DSH's lifecycle.

Want to add HTTP or GitHub verification? [Claim an issue](https://github.com/os1249399459/no-receipts/issues) — both are scoped to one file, and `CliVerifier` is the reference at ~80 lines. Windows portability was shipped by [an outside contributor](https://github.com/os1249399459/no-receipts/pull/4).

### Other repos

- [xiaoyue-morning-service](https://github.com/os1249399459/xiaoyue-morning-service) — a gentle AI sister sends you Japanese every morning, with pitch accents, weather, and bento recipes
- [単語カード](https://os1249399459.github.io) — 92 Japanese vocabulary cards, ComfyUI art + VOICEVOX audio, flipping in the browser
- [LeetCode](https://github.com/os1249399459/LeetCode) — Java solutions, one folder per problem

---

## 🧰 The Survival Kit

ComfyUI · VOICEVOX Core · FastAPI · kohya_ss · VapourSynth · MPV · CosyVoice · Magisk (and duct tape)

## 📬 Contact

- Email: <1249399459@qq.com>

![Stars](https://img.shields.io/github/stars/os1249399459?style=flat-square)

![Followers](https://img.shields.io/github/followers/os1249399459?style=flat-square)
