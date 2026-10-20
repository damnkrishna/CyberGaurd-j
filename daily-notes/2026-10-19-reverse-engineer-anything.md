# REA: Reverse Engineer Anything

> **Note:** REA stands for **Reverse Engineer Anything** (not "Research Engineer Anything").
> Repo: `github.com/morluto/rea` · Site: `rea.tools` · npm package: `rea-agents` · License: MIT

---

## Table of Contents

1. [My Raw Thoughts](#1-my-raw-thoughts)
2. [What REA Actually Does](#2-what-rea-actually-does)
3. [The Five Stages](#3-the-five-stages)
4. [Is It Only for Rich People?](#4-is-it-only-for-rich-people)
5. [Legal and Safety](#5-legal-and-safety)
6. [My Setup (Antigravity + Gemini Pro)](#6-my-setup-antigravity--gemini-pro)
7. [Starter Project Ideas](#7-starter-project-ideas)
8. [Prompts to Use](#8-prompts-to-use)
9. [Tips](#9-tips)
10. [Extra](#10-extra)

---

## 1. My Raw Thoughts

*(Kept exactly as written, unedited.)*

> well there has been recently a new repo that is havily being used and publically being in scope for some time now  
> it is crazy how much they have gained recognition and it has actually opened another pandora box which is fucking crazy  
> This can literally reverse engineer anything from scratch to anything like for real it can see

> what do u know about this rea reverse engineer anything repo that is being soo much used in publicly lately  
> and what is that it actually do  
> and i also have another question cause like to use this repo practically we need to integrate it with some ai  
> but good ai like claude requires premium to do such big things  
> but what about people who uses ai for free or doesnt have money to buy premium subscription ai like claude max or gemini pro  
> or gpt latest that are compatible
>
> so this new technique is i think usable by people who are already rich and also deep into tech  
> cause i have listened in some video about the power this rea holds  
> having the power to understand the whole company like a device  
> and use the specific feature u like from some tool u can learn how it do it by this tool and enroll that feature in our own software  
> and build anything  
> and as it rn lack ai rules and regulation which will be build  very  soon  
> than we wont be able to do it  
> so till now i want to know what it can do  
> and what can it do

---

## 2. What REA Actually Does

REA is an open-source (MIT) **CLI and MCP server** that lets AI coding agents investigate how software works. It went viral in 2026 and has hundreds of thousands of GitHub stars.

REA is **not** a new decompiler. It is closer to a toolkit that connects existing decompilers and analysis tools to an AI agent. It does this through **MCP (Model Context Protocol)**, the protocol AI agents use to call external tools. It also gives the agent a five-stage process for studying a feature and rebuilding it, so the agent does not poke around randomly and guess.

### What it can do

- Analyze native apps, Electron/JavaScript apps, .NET assemblies, Android APKs and live browser behavior.
- Return pseudocode, assembly, modules, call chains and relationships between files, along with the evidence for its conclusions.
- Run analysis locally. It does not upload the app to a hosted analysis service.

### What it cannot do

- It does **not** recover the original source code.
- It cannot hand you a company's real codebase. "Understand the whole company like a device" is **hype**.
- It helps an AI *understand how a program works*. That is not the same as owning the program's code.

---

## 3. The Five Stages

| # | Stage | What happens |
|---|-------|--------------|
| 1 | **Pick a feature** | Isolate one piece of functionality instead of pointing the agent at a whole app. One example was Loom's movable camera bubble. Narrow targets work much better than "clone this app." |
| 2 | **Route by build** | The agent first works out what the app is built with, because the tech stack decides which inspection tools make sense. |
| 3 | **Summary first** | Raw analysis can be huge (one demo mentioned over a gigabyte for Loom). REA condenses it into a short summary of what works, how it works, and what is unclear. The summary is saved locally. This matters for free-tier users because it stops the model from re-reading everything each time, which saves tokens. |
| 4 | **Seen / Inferred / Unknown** | Every finding is tagged as directly observed, strongly suggested but unconfirmed, or undetermined. This stops the AI from presenting guesses as facts. |
| 5 | **Rebuild and test** | The agent writes the feature in your own codebase and tests that it behaves like the original, rather than shipping a first draft. |

In the public examples, the rebuilt apps looked visually different from the originals. The goal is to extract *how a mechanic works* and reimplement it, not to copy the UI or code.

---

## 4. Is It Only for Rich People?

**No.**

- REA itself is free. The AI model on top of it is the only possible cost.
- Free tiers and open-source models can handle small, narrow tasks. Big, complex targets work better with stronger models, and free tiers have usage caps.
- Technical judgment matters more than money, because you need to check whether the AI's output is correct.
- The method is not tied to one paid model. Other capable coding agents can follow the same process.

---

## 5. Legal and Safety

*(I am not a lawyer. Check the rules in your own country.)*

### Usually fine
- Learning how techniques work.
- Studying your own software or open-source software.
- Security research on things you are allowed to test.
- Rebuilding common interactions from observed behavior.

### Risky or excluded
- Copying code, assets, images or text from the target.
- Bypassing licenses, DRM, authentication or paywalls.
- Cloning a paid product to compete with it.
- Breaking a service's terms of service (often forbidden even where the law allows reverse engineering).
- The project's own disclaimer excludes DRM bypass, license checks, anti-cheat, game cheats, copying proprietary software and reselling AI access.

### Fake versions exist
A fake trojan copy of REA has been circulating. Only download from:

- `github.com/morluto/rea`
- `rea.tools`
- the `rea-agents` npm package

---

## 6. My Setup (Antigravity + Gemini Pro)

1. Install **Node.js** (the README badge mentions Node 24).
2. Run:
   ```bash
   npx rea-agents setup
   ```
3. Choose your agent, review the proposed changes, approve them, then **restart the agent**. Setup backs up your existing config first.
4. If Antigravity is not in the list, add REA manually through Antigravity's **MCP Servers** menu.
5. Check that everything works:
   ```bash
   npx -y rea-agents doctor
   ```

**Platform notes**

- The README says REA is most useful for **native app investigation on macOS**.
- Hopper (the disassembler it uses for native analysis) needs its own license.
- JavaScript/Electron, .NET, Android APK and browser targets may not need Hopper, but this is **not confirmed**.
- Sources disagree on how automatic Antigravity setup is. One lists Antigravity as supported, while the official README says setup auto-configures only Claude Desktop and Cursor. So expect that manual registration may be needed.

---

## 7. Starter Project Ideas

1. **Trial on an open-source app (best first try).** Let REA analyze one feature, then compare its claims with the real source code. This shows how accurate it is, with no legal worries.
2. **Local screen recorder with a floating camera bubble.** Build it from observed behavior only, for personal use, with no copied code or assets.
3. **Study one website interaction** (for example, how a kanban board drags cards) and rebuild it in your own app. Check the site's terms first.
4. **Understand your own old project** when you have lost the source or documentation.

---

## 8. Prompts to Use

### Prompt A: Verify the setup

```text
Check that the REA MCP server is registered and working. List the REA tools
you can see. Don't analyze anything yet. If REA isn't available, tell me
exactly what's missing instead of guessing or using other tools.
```

### Prompt B: Main project prompt

Fill in the brackets before using it.

```text
Use the REA MCP tools to study ONE feature of an app, then rebuild that
feature independently in a new project.

Target app: [name / path / URL, something I'm allowed to analyze]
Feature: [one narrow feature, e.g. "drag-to-reorder cards on the board"]
My new project: [e.g. a small web app in plain HTML/JS, or React]

Follow these stages in order and stop after stage 3 for my approval:

1. Pick the feature: restate the exact feature and its boundaries.
2. Route by build: identify what the target is built with and say which
   REA tools you'll use and why.
3. Summary first: don't dump raw output. Write a short summary file
   (analysis/summary.md) covering what works, how it works, and what is
   unclear. Keep raw output in separate files and open them only when needed.
4. Label every finding as SEEN (directly observed, with evidence),
   INFERRED (strongly suggested, not confirmed) or UNKNOWN. Never present
   an inference as fact.
5. Rebuild and test: after I approve, build the feature in my project from
   the behavior you documented. Write tests, run them, and fix failures
   before telling me it's done.

Rules:
- Don't copy source code, assets, images or text from the target. Study
  behavior and reimplement it in your own way.
- Don't bypass licenses, DRM, authentication or paywalls.
- Work on this one feature only. Don't try to clone the whole app.
- If something is UNKNOWN, ask me or propose an experiment instead of guessing.
```

### Prompt C: After you approve the summary

```text
The summary looks good. Build the feature now in [project folder]. Start
with the smallest working version, add tests that compare behavior against
the SEEN findings, then handle the INFERRED items one by one and tell me
which ones your tests confirmed or contradicted.
```

---

## 9. Tips

- Keep tasks small so you stay within Gemini's limits.
- Put your rules (no copying, label findings) in Antigravity's **workspace rules** so you do not have to repeat them.
- Do the open-source trial first to learn how far to trust REA.

---

## 10. Extra

Some additional thoughts and reminders.

**On the "window of opportunity" worry**
The idea that this will be impossible once AI rules arrive is not quite right. Studying how software works is already legal in many places, and copying proprietary code or breaking licenses is already restricted today. New regulation is more likely to clarify the line than to erase the whole field. So the useful habit is to build things you are clearly allowed to build.

**On trusting the hype**
- Star counts and viral videos tell you about popularity, not accuracy.
- Different articles describe REA slightly differently (a method for agents versus a toolkit that links decompilers). Both views are probably true.
- Some of the articles are from companies that sell related products, so keep that in mind.
- Test the claims yourself on a small target before believing the big promises.

**Habits worth copying from REA even outside this tool**
- Work on one narrow thing at a time.
- Make the AI separate what it *saw* from what it *assumed*.
- Save summaries to files so you can start a fresh chat without losing progress.
- Always test the result before calling it done.

**Suggested learning path**
1. Install and run `doctor`.
2. Run the open-source trial on one small feature.
3. Compare REA's claims with the real source.
4. Build a small personal project (for example, the camera-bubble recorder).
5. Write down what worked and what failed.

**Open questions to check later**
- Does REA work smoothly with Antigravity on your operating system?
- Which target types need Hopper (and its license), and which do not?
- How well does Gemini Pro handle the five-stage workflow on larger targets?

**Keep updated**
This field changes fast. Check the official repo and `rea.tools` for current instructions before you run anything.
