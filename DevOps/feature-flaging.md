# Feature Flagging

Feature flagging is a software technique used to manage features in robust, large-scale software systems.

The idea is to control the availability of certain features, allowing the system to decide — based on predefined rules or configurations — whether to enable or disable a particular feature for specific users or user groups. This enables teams to test new features safely, roll out experiments, or provide early access to select users (such as beta testers, specific roles, or randomly chosen users).

Feature state and rules are typically stored in a configuration system or database, describing which features are enabled, for whom, and under what conditions. This store acts as the decision point for feature access across the application.

---

## The Four Types of Feature Flags

The four canonical types come from Pete Hodgson's article on Martin Fowler's site. Each type differs across two key dimensions: **how long it lives** and **how dynamic its routing needs to be**.

### 1. Release Flags

**Lifespan:** Short-lived · **Dynamism:** Static

Deploy code before it's ready to be seen. Release flags let incomplete features ship to production as dark, inactive code, then get switched on when the team is confident — or rolled back instantly if something breaks. No redeployment needed.

Common uses:

- Trunk-based development without long-lived feature branches
- Dark launches — merge weeks before launch day
- Emergency kill switch after a bad release

> Remove these as soon as the feature is fully rolled out. They have the shortest intended life of all four types.

---

### 2. Ops Flags (Operational Flags)

**Lifespan:** Long-lived · **Dynamism:** Highly dynamic

Give operations teams a runtime lever. When a system is under stress, an ops flag lets an SRE disable an expensive feature, switch to a fallback service, or throttle traffic — without touching code or triggering a deploy.

Common uses:

- Circuit breakers during high-load incidents
- Switching between a primary and fallback service implementation
- Graceful degradation under system pressure

> Unlike release flags, ops flags are often kept permanently as standing kill switches.

---

### 3. Permission Flags

**Lifespan:** Long-lived · **Dynamism:** Static to dynamic

Control access based on who the user is — their role, plan tier, geographic region, or an explicit allowlist. The flag's configuration is relatively stable; what changes is the user's context at request time.

Common uses:

- Gating premium features behind a paid plan (free vs. pro)
- Internal or staff-only tools
- Closed betas with a named allowlist of users or emails

> Permission flags often live for the entire product lifetime — a pro-plan gate isn't temporary.

---

### 4. Experiment Flags

**Lifespan:** Short-lived · **Dynamism:** Dynamic routing

Split users into cohorts and send each down a different code path. The assignment is deterministic (hashed on user ID), so a user always sees the same variant across sessions. Once a winning variant is confirmed, the flag is retired and that path becomes the default.

Common uses:

- A/B and multivariate testing in production
- Measuring conversion, retention, or engagement across variants
- Validating a product hypothesis before full rollout

> Treat experiment flags as temporary experiments — once the data is in, clean them up.

---

## How the Four Types Relate

|             | Short-lived | Long-lived |
| ----------- | ----------- | ---------- |
| **Static**  | Release     | Permission |
| **Dynamic** | Experiment  | Ops        |

Each type has different infrastructure needs. Release flags can live in a config file. Ops flags need a live admin interface for incident response. Experiment flags need cohort-bucketing logic. Permission flags need access to user attributes at runtime. Lumping them all together leads to confusion — treat each category differently from the start.

---

## Why Feature Flags Matter

Feature flags are essential in continuous delivery, experimentation, and progressive releases. They decouple **deployment** from **release** — code ships to production, and the decision of when (and for whom) to reveal it is a separate, configuration-level concern.

Key benefits:

- **Safer deployments** — ship unfinished code without exposing it to users
- **Instant rollbacks** — flip a flag instead of reverting a deployment
- **Progressive delivery** — expand a rollout gradually as confidence builds
- **Experimentation** — measure real user behavior before committing to a design
- **Operational control** — disable costly features under load without an incident response

---

## A Note on Flag Debt

Feature flags accumulate fast. Old flags that were never cleaned up become _flag debt_ — they clutter the codebase, make logic harder to follow, and can interact with each other in unexpected ways.

A healthy rule of thumb: **schedule a flag's removal the day you create it.** Release and experiment flags should have an expiry date. Ops and permission flags should be reviewed periodically and removed if the capability they guard is no longer needed.
