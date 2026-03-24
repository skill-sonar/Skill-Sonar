   <p align="center">
     <img src="./assets/skill-sonar.png" alt="Skill Sonar Logo" width="120" />
   </p>


   <p align="center">
     A lifecycle-aware security skill for AI agents, covering both <strong>pre-install inspection</strong> and <strong>runtime monitoring</strong>.
   </p>
   <p align="center">
     <a href="https://skill-sonar.github.io/skill-sonar"><strong>Website</strong></a> ·
     <a href="https://clawhub.ai/yxf203/skill-sonar"><strong>ClawHub</strong></a>
   </p>

## 🚀 Features

* **Deep Code Sonar**: Continuously sweeps and analyzes your logic to detect hidden vulnerabilities, bugs, and inefficiencies with high precision.
* **Robust Security Shield**: Built-in security protocols and advanced checks ensure your environment remains safe, locked down, and resilient against potential threats.
* **Precision Node Mapping**: Intelligently traces dependencies, execution paths, and skill nodes to provide crystal-clear visibility into your architecture.
* **Real-Time Threat Detection**: Instant "sonar pings" and alerts notify you of potential risks or code smells the moment they are introduced.
* **Seamless Integration**: Designed to be lightweight and effortlessly integrate into your existing developer workflows and CI/CD pipelines.

## Install

You can install **Skill Sonar** in either of the following ways:

### 1. Install via the official npm-based method

Use the standard installation flow supported by your agent platform.

```
clawhub install skill-sonar
```

or

```
npx clawhub@latest install skill-sonar
```

### 2. Install manually

Download the Skill Sonar files directly, then move the skill into the `skills` directory under your corresponding OpenClaw (`.openclaw`) workspace.

## Quick Start

### Check a skill before installation

```
use skill-sonar to check xxx skills
```

### Monitor the current session at runtime

```
use skill-sonar to monitor this session
```

## Modes

Skill Sonar supports **three operating modes**:

### 1. Full protection

Enable both the **pre-install check** and the **runtime check**.

```
use skill-sonar for full protection
```

### 2. Pre-install only

Enable only the **pre-install check**.

```
only use the pre-install check
```

### 3. Runtime only

Enable only the **runtime check**.

```
only use the runtime check
```

## What It Does

Skill Sonar protects the **full lifecycle of the agent loop** across two stages:

- **Pre-install** — inspects a skill before it is installed or enabled
- **Runtime** — monitors the agent during task execution

This allows you to use a single unified security skill for both **skill review** and **in-session protection**.

## Design Highlights

### Document-level routing

Skill Sonar uses **document-level routing** instead of relying on config files, installation parameters, or external orchestration.

A single entry document reads the current context, determines whether the agent is in a **pre-install** or **runtime** scenario, and routes execution to the appropriate guard path.

This design keeps the system:

- lightweight
- easy to integrate
- easy for agents to invoke
- flexible enough to support either full protection or stage-specific protection

More importantly, routing helps prevent the agent from being overloaded with irrelevant guard logic all at once, allowing it to focus on the checks that actually matter at the current stage.

### On-demand loading

Skill Sonar is designed for **on-demand loading**.

It does not preload every guard, checklist, or analysis file upfront. Instead, the agent loads only the components required for the current stage and the current risk signals.

This means:

- clean cases remain lightweight
- suspicious cases trigger deeper analysis only when needed
- runtime overhead stays low
- token usage scales with actual risk rather than total framework size

This also improves practical security coverage: rather than spending context budget on everything equally, the agent can devote more attention to areas that appear genuinely suspicious, making it easier to reason more deeply about complex or compound threats.

### Token-efficient by design

Skill Sonar is built to minimize unnecessary context usage.

- The entry layer handles routing instead of loading everything upfront
- Stage-specific files are only used when relevant
- Deep analysis is triggered only for flagged areas
- Full lifecycle coverage does not require full upfront cost

This makes Skill Sonar especially well suited for agent environments where **token budget, context size, and routing clarity** all matter.

By reducing wasted context, Skill Sonar leaves more room for the agent to consider a broader range of relevant security factors, connect signals across stages, and produce more focused judgments instead of shallow all-at-once checks.

## Typical Use Cases

- Audit a skill before installing it
- Add runtime monitoring during a sensitive session
- Use full lifecycle protection for untrusted or third-party skills
- Apply lightweight security guarding in OpenClaw workflows

## Notes

- For complete lifecycle protection, use **full protection** mode.
- If you only need one stage, specify it explicitly in your prompt.
- Exact invocation may vary slightly depending on your agent environment.
