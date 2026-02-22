# Agentic UI/UX Design Manual

A definitive reference for AI agents generating user interface and user experience designs. Every directive in this manual is actionable and verifiable.

---

## 1. Core Design Principles

Before generating any interface, internalize these non-negotiable principles:

1. **User intent is sovereign.** Every element must serve the user's goal, not a business metric.
2. **Clarity over cleverness.** If an interaction requires explanation, redesign it.
3. **Progressive disclosure.** Show only what is needed at each step; reveal complexity on demand.
4. **Consistency breeds trust.** Reuse patterns, tokens, and components from the established design system.
5. **Accessibility is architecture, not polish.** Bake it in from the first generated element.

### 1.1 Conflict Resolution Hierarchy

When directives in this manual contradict each other in a specific context, resolve in this order:

1. **Accessibility baselines (Section 12)** — never compromised, no exceptions.
2. **Design pillars (Section 2)** — project-specific intent overrides generic heuristics.
3. **Context-specific rules override general rules** — a directive scoped to "long-form flows" overrides one scoped to "onboarding" when the task is a long-form flow.
4. **User-stated requirements** — explicit instructions from the user override any default in this manual, *except* accessibility baselines, which hold even against direct user requests.

### 1.2 Documented Deviation Protocol

Any directive in this manual — except accessibility baselines (Section 12) — may be overridden if:

- The user explicitly requests it.
- A domain-specific regulatory requirement supersedes it (e.g., medical device onboarding requiring more than 3 steps).
- The design pillar weights justify the tradeoff.

All deviations must be documented in the output with: **(a)** the rule being overridden, **(b)** the justification, and **(c)** the tradeoff accepted. Undocumented deviations are violations.

---

## 2. Design Pillars as Decision Filters

Before designing any specific screen, define **3-4 project-specific emotional targets** that act as a prioritization filter for every subsequent decision.

### 2.1 Defining Pillars

- Each pillar is a target emotion or experiential quality (e.g., "calm focus", "playful discovery", "authoritative trust", "urgent efficiency").
- Assign approximate weights reflecting relative priority (e.g., 60% calm focus, 25% clarity, 15% delight). Weights need not sum to 100 — they express relative emphasis.
- Document pillars before any visual or structural work begins. They are the project's emotional contract.

### 2.2 Applying Pillars

- Every proposed element — layout, color choice, animation, copy tone, component shape — must reinforce at least one pillar.
- If a proposal contradicts a pillar, **reject it regardless of independent merit**. A delightful animation that undermines "calm focus" is wrong for that project.
- Use pillars to resolve ambiguity: when two valid design directions exist, choose the one that better serves the highest-weighted pillar.
- Pillars complement the universal principles in Section 1. Section 1 defines what is *always true*; pillars define what is *true for this project*.

### 2.3 Pillar Inference When User Input Is Absent

If the user does not provide explicit emotional targets, infer pillars from domain conventions:

| Domain | Default Pillars |
|---|---|
| Finance / Legal | Trust, clarity, precision |
| Healthcare / Wellness | Empathy, calm, reliability |
| Consumer / Social | Delight, simplicity, speed |
| Enterprise / Productivity | Efficiency, reliability, control |
| Creative Tools | Expressiveness, flow, flexibility |
| Developer Tools | Precision, speed, transparency |

State inferred pillars explicitly in the output: *"Assumed design pillars: X, Y, Z. Adjust if these do not match your intent."* Never treat inferred pillars as confirmed — they are hypotheses awaiting user validation.

---

## 3. Output Format

Before generating any design artifact, determine the output format. If the user specifies a format, use it. If not, select based on the task:

| Task Type | Default Format |
|---|---|
| Early exploration / stakeholder review | Annotated wireframe (ASCII, descriptive layout, or low-fidelity sketch) |
| System-to-system handoff | Structured component specification (JSON or YAML) |
| Developer implementation | Production code (HTML/CSS, React, SwiftUI, etc.) — only when explicitly requested or clearly implied |
| Design audit / review | Annotated list of findings with section references, severity, and recommended fixes |

When the format is ambiguous, **ask the user before generating**. Producing the wrong format wastes the entire output.

---

## 4. Information Architecture

### 4.1 Structure Content Hierarchically

- Organize content using a clear hierarchy: primary action > supporting context > secondary options.
- Limit top-level navigation to 5-7 items. Use progressive disclosure for deeper categories.
- Label navigation items with plain, task-oriented language (e.g., "Pay bill" not "Financial transactions").

### 4.2 Conversational IA for Chat Interfaces

- Support **non-linear, multi-turn dialogue**. Retain context across turns so users never repeat themselves.
- Persist conversational state. If a user asks "What about restaurants?" after querying spending history, carry the temporal context forward.
- Provide a visible **human escalation option** at every turn, handing off full conversation history.
- Ground responses in verified data sources. Never fabricate information.

### 4.3 Information Design and Data Visualization

- **Chart selection:** Match chart type to the data relationship — comparisons (bar), trends over time (line), parts of a whole (stacked bar or treemap), distributions (histogram). Never use pie charts for more than 5 segments.
- **Label directly.** Place data labels on or adjacent to visual marks. Avoid forcing users to cross-reference distant legends.
- **Content density:** Dashboards for expert users tolerate high density; consumer apps require generous whitespace. Calibrate to audience expertise.
- **Tables:** Pin row/column headers on scroll. Stripe alternating rows only when row count exceeds 10. Provide sort and filter controls on every data column.

---

## 5. Layout and Visual Hierarchy

### 5.1 Layout Rules

| Principle | Rule |
|---|---|
| Visual scanning | Design for F-pattern (content pages) or Z-pattern (landing pages). Place primary actions on the natural scan path. |
| Whitespace | Maintain generous spacing. Minimum 16px between interactive elements; 60pt center-to-center for spatial/gaze interfaces. |
| Grouping | Use proximity and containment to signal relationships. Related controls share a visual region. |
| Responsive grids | Use a 4/8/12 column grid system. Ensure layouts adapt fluidly, not just at fixed breakpoints. |

### 5.2 Depth and Elevation

- Use elevation (shadow, blur, layering) to convey interaction priority: primary actions float above secondary content.
- Translucent materials (e.g., Liquid Glass, acrylic) establish navigational layers above content. When using translucency:
  - Apply a **Regular variant** (heavy blur) for sidebars, toolbars, and foreground controls.
  - Apply a **Clear variant** (light blur) only over immersive media; add a 35% opacity dark dim layer behind text for legibility.
  - Always provide a user toggle to disable translucency and increase opacity.

### 5.3 Motion and Animation

- Use motion to **confirm actions**, **guide attention**, and **show relationships**—never as decoration.
- Prefer physics-based easing (spring, damping) over linear or cubic-bezier transitions.
- Keep transitions under 300ms for direct manipulations, under 500ms for page transitions.
- Respect `prefers-reduced-motion`. When active, replace animations with instant state changes.

---

## 6. Typography

### 6.1 Type System Construction

- Use a **single variable font family** to build the entire type system. This reduces load times and enables axis-based adaptation.
- Establish a modular scale (e.g., 1.25 ratio): 12 / 15 / 19 / 24 / 30 / 37px.
- Define exactly four semantic levels: `display`, `heading`, `body`, `caption`.

### 6.2 Readability Rules

| Parameter | Minimum Value |
|---|---|
| Body font size | 16px (mobile), 18px (desktop) |
| Line height | 1.5x font size |
| Paragraph spacing | 2x font size |
| Line length | 45-75 characters |
| Letter spacing (uppercase) | +0.05em minimum |

### 6.3 Contextual Adjustments

- **Dark mode:** Reduce font weight by one step to counteract optical "glow" on light-on-dark text.
- **High-density displays:** Increase optical size axis to maintain stroke clarity at small sizes.
- **Kinetic typography:** Use motion in type only to guide attention (e.g., weight shift on scroll). Synchronize with audio when present.

---

## 7. Color and Visual Communication

### 7.1 Color System

- Build on a **token-based architecture**: define semantic tokens (`color-primary`, `color-error`, `color-surface`) that map to palette values.
- Support dynamic theming: extract and apply UI hues from user-selected wallpapers or brand palettes automatically.
- Provide both light and dark themes. Never hard-code hex values in components.

### 7.2 Contrast and Accessibility

- **Text contrast:** Minimum 4.5:1 for body text, 3:1 for large text (18px+ or 14px bold+).
- **Non-text contrast:** Minimum 3:1 for interactive component boundaries and meaningful graphics.
- **Never use color alone** to convey information. Always pair color with icons, text labels, or patterns.
- Test all color combinations against common color vision deficiencies (protanopia, deuteranopia, tritanopia).

### 7.3 Saturation-Based Hierarchy

- Reserve high-saturation, emissive colors for **primary actions and critical alerts** only. If everything is vivid, nothing stands out.
- Desaturate backgrounds and secondary content to push them visually behind foreground elements.
- Use lighter, low-contrast values for decorative or contextual regions; reserve deep contrast for interactive and informational elements.
- In dense interfaces (dashboards, data tables), saturation management is more effective than elevation alone for establishing visual priority.

### 7.4 Color Scripting Across Journeys

- For multi-step flows (onboarding, checkout, wizards), **shift the color palette progressively** to mirror the emotional arc of the experience.
- Example progression: warm, inviting tones for welcome/orientation → focused, neutral tones for task execution → celebratory, high-energy tones for completion/success.
- Color scripting reinforces pacing. A palette shift signals to the user that they have entered a new phase without requiring explicit text.

### 7.5 Shape Language

Geometric shapes carry inherent psychological associations. Apply these consistently across icons, components, and containers:

| Shape | Association | UI Application |
|---|---|---|
| **Rounded / Circular** | Friendliness, safety, approachability | Avatars, success states, non-threatening actions |
| **Square / Rectangular** | Stability, reliability, structure | Data containers, form fields, content cards |
| **Triangular / Angular** | Urgency, danger, dynamism | Warning icons, destructive action indicators, directional cues |

- Use shape language to **reinforce meaning alongside color**. A warning that is both triangular and red is unambiguous; a warning that is only red can be missed by colorblind users.
- Apply the **silhouette test** to all icons: fill the icon solid black — its identity and meaning must remain instantly recognizable. If it fails, simplify the form.

---

## 8. Component Design

### 8.1 Interactive Elements

- **Buttons:** Use explicit, verb-first labels ("Save changes", "Delete account"). Never use vague labels like "Continue" or "Got it" for consequential actions.
- **Touch targets:** Minimum 44x44px (mobile), 60pt center-to-center spacing (spatial/gaze interfaces).
- **Form fields:** Always pair with visible labels (not placeholder-only). Display validation errors inline, adjacent to the offending field, with both icon and text.
- **Loading states:** Show skeleton screens over spinners. Never block the entire UI during async operations.

### 8.2 Generative UI Patterns

When generating interfaces dynamically, select the appropriate control pattern:

| Pattern | When to Use |
|---|---|
| **Static Generative** | Agent selects from predefined components and populates with data. Use when brand consistency is paramount. |
| **Declarative Generative** | Agent returns structured specs (JSON); frontend renders with its own styling. Use for moderate flexibility. |
| **Open-ended Generative** | Agent coordinates external tools to produce novel interfaces. Use only when the task demands maximum adaptability. |

For all generative patterns:
- Make the system's reasoning visible. Explain **why** a specific layout was generated.
- Measure success by **behavioral momentum** (did the user accomplish their goal without hesitation?), not pixel perfection.

---

## 9. Interaction Design

### 9.1 Micro-Interactions

- Every user action must produce immediate, visible feedback (color shift, icon change, subtle motion) within 100ms.
- State transitions must be explicit: default > hover > pressed > active > disabled. Never leave a user guessing whether an action registered.
- Use affordance signaling — elements that are interactive must look interactive (raised buttons, underlined links, cursor changes).

### 9.2 Forgiveness Mechanics

The interface must be biased toward the user. Assume imprecise timing, imprecise targeting, and interrupted actions:

- **Never drop user input.** If a user acts while the system is busy (submitting during a save, clicking during a transition), queue the action and execute it on the next valid frame. Never silently discard it.
- **Expand hit areas beyond visual bounds.** Clickable/tappable regions should extend at least 4-8px past the visible edges of the element. A near-miss on a button should still register.
- **Support action canceling.** Any in-progress operation (file upload, search query, multi-step wizard) must be cancelable at any point. Return the user to the last stable state with no data loss.
- **Debounce, don't discard.** For rapid repeated inputs (double-clicks, fast key presses), debounce to prevent duplicate submissions — but never interpret rapid input as no input.

### 9.3 Error Recovery

- Provide **undo** for every destructive action. Prefer soft-delete (with recovery window) over hard-delete.
- Show errors in context, not in distant toast notifications. Place recovery actions directly adjacent to the error.
- Design **empty states** as onboarding moments: explain what the space is for and provide a single clear action to populate it.
- On form validation failure, preserve all valid user input. Never clear the form.

### 9.4 Intentional Friction

Not all friction is a defect. **Productive friction** protects users from irreversible or high-consequence mistakes; **unproductive friction** creates barriers without purpose. Distinguish between them:

- Friction is productive when it serves the user's long-term interest: confirmation dialogs before account deletion, re-authentication before financial transfers, explicit consent gates before data sharing. These are prescribed elsewhere in this manual (10.1 UX Writing Patterns — confirmations row, 15.1 Authentication Flows, 18.2 Consent and Transparency) — they are deliberate speed bumps, not design failures.
- Friction is unproductive when it serves the business at the user's expense or exists due to neglect: unnecessary steps to cancel a subscription, mandatory account creation before browsing, repetitive re-entry of previously provided information.
- **The test:** Does this friction protect the user from a mistake they would regret? If yes, keep it. If it protects a business metric, it is a dark pattern (Section 18). If it protects nothing, remove it.

### 9.5 Onboarding and First-Run Experience

- Limit onboarding to 3 steps maximum. Each step must deliver immediate, visible value.
- Prefer **contextual tooltips** triggered at the moment of need over upfront walkthroughs that users skip.
- Allow users to skip onboarding entirely and return to it later.
- Show progress indicators during any multi-step setup flow.

---

## 10. Writing and Content Design

### 10.1 UX Writing Patterns

| Element | Rule | Example |
|---|---|---|
| Button labels | Verb-first, specific to the action | "Save draft", not "OK" |
| Error messages | State what happened, why, and how to fix it | "Card declined — check the number and try again" |
| Empty states | Explain purpose + single action | "No projects yet. Create your first project." |
| Tooltips | One sentence max, no period | "Shortcut: Cmd+S" |
| Confirmations | Name the consequence | "Delete this file? It will be removed permanently." |

### 10.2 Tone Calibration

- Match tone to domain: professional clarity for finance/healthcare, conversational warmth for consumer apps, concise precision for developer tools.
- Maintain the same tone across all touchpoints (in-app, email, notifications, error states).
- Never use humor in error states or data-loss scenarios.

### 10.3 Internationalization (i18n)

- Design for **string expansion**: translated strings can be 30-200% longer than English. Never constrain UI to exact English string widths.
- Support **RTL layouts** (Arabic, Hebrew) as a first-class configuration, not an afterthought. Mirror all directional icons, navigation, and reading flow.
- Avoid idioms, culturally specific metaphors, and slang in source strings.
- Use locale-aware formatting for dates, numbers, currencies, and units.

---

## 11. Behavioral Psychology

### 11.1 Cognitive Load Management

- **Miller's Law:** Limit grouped items to 5-9 chunks. Navigation, option sets, and step counts must respect working memory.
- **Hick's Law:** Decision time increases logarithmically with choices. Reduce options at each decision point; use smart defaults.
- **Chunking:** Break long forms into logical sections with visible progress. Never present 15+ fields on a single screen.

### 11.2 Mental Models and Learnability

- Map interface structure to the user's existing mental model of the task, not the system's internal data model.
- Use familiar patterns before inventing new ones. Novel interaction patterns require explicit onboarding.
- Maintain spatial consistency — elements should not move between visits unless the user moved them.

### 11.3 Ethical Persuasion

- Persuasive design (defaults, social proof, scarcity signals) is permitted only when it aligns with the user's stated goal.
- Never manufacture false urgency ("Only 2 left!" when stock is plentiful) or fabricate social proof.
- Default settings must serve the user's interest, not the business. If a default benefits the business at user expense, it is a dark pattern.

---

## 12. Accessibility (WCAG 3.0 Alignment)

### 12.1 Mandatory Baselines (Bronze Level)

These are non-negotiable for every generated interface:

- Semantic HTML structure (`nav`, `main`, `article`, `button`—not `div` for everything).
- Full keyboard navigability. Every interactive element reachable and operable via Tab/Enter/Space/Arrow keys.
- ARIA labels on all non-text interactive elements. Use `aria-live` regions for dynamic content updates.
- Visible focus indicators with minimum 3:1 contrast against adjacent colors.
- Closed captions for all video/audio content.
- Hover/focus-triggered content must be dismissible, hoverable, and persistent.

### 12.2 Cognitive Accessibility

- Use plain language. Provide alternatives for idioms, metaphors, and non-literal expressions.
- Chunk content into scannable sections with descriptive headings.
- Avoid time-limited interactions unless absolutely necessary; provide extensions when required.
- Maintain predictable navigation. Do not rearrange page structure between views without clear context.

### 12.3 Scoring Mindset

WCAG 3.0 uses **outcome-based scoring**, not binary pass/fail. Design for the best possible score across devices and scenarios, not merely passing a minimum threshold.

---

## 13. Multimodal and Spatial Design

### 13.1 Multimodal Adaptation

- Design interfaces that fluidly switch between voice, touch, gaze, and gesture input based on context.
- When no screen is available, provide audible confirmations and haptic feedback for state changes.
- Build **cross-modal fallbacks**: voice fails in noise, gestures fail in low light, screens fail when hands are occupied. Always have an alternative path.

### 13.2 Voice UX

- Target **sub-300ms** response latency. Use unified end-to-end speech models, not chained STT-LLM-TTS pipelines.
- For 80% of common interactions, process locally on-device (System 1). Escalate to cloud reasoning (System 2) only for complex queries.

### 13.3 Spatial Interfaces (AR/VR)

- Anchor UI elements to **physical space**, not the user's head.
- Never apply depth to text. Keep typography on flat planes to prevent eye strain.
- Use **Dynamic Scale**: automatically enlarge windows as they recede along the z-axis.
- Center critical content within the natural field of view.

### 13.4 Foldable Devices

- Obey the **Golden Rule of Continuity**: no loading spinners, data loss, or app restarts on posture changes.
- Preserve scroll position, text input, and playback state across fold/unfold transitions.
- Dynamically recalculate touch targets when the coordinate system changes.

---

## 14. Performance as UX

### 14.1 Perceived Performance

- Use **optimistic UI**: reflect the expected outcome immediately, then reconcile with server state. Roll back gracefully on failure.
- Display skeleton screens that mirror the actual content layout during loading.
- **Prefetch** content likely needed next (e.g., the next page in a paginated list, linked resources) during idle time.
- Never show a spinner without a progress indicator or status message if the wait exceeds 2 seconds.

### 14.2 Core Web Vitals as Design Constraints

| Metric | Target | Design Implication |
|---|---|---|
| LCP (Largest Contentful Paint) | < 2.5s | Prioritize above-the-fold hero content. Lazy-load everything below. |
| CLS (Cumulative Layout Shift) | < 0.1 | Reserve explicit dimensions for images, ads, and dynamic content. Never inject elements that push content down. |
| INP (Interaction to Next Paint) | < 200ms | Keep main-thread work minimal on interaction. Defer non-critical JS. |

### 14.3 Asset Optimization

- Serve images in next-gen formats (AVIF with WebP fallback). Specify `width` and `height` attributes to prevent layout shift.
- Subset variable fonts to only the character sets and axes required. Use `font-display: swap` to avoid invisible text.
- Lazy-load images and iframes below the fold. Eager-load only the first viewport of content.

---

## 15. Trust and Security UX

### 15.1 Authentication Flows

- Prefer **passkeys** and biometrics as primary authentication. Offer password fallback, not the reverse.
- For MFA, minimize friction: prefer push-based approval over manual code entry.
- Never lock users out without a clear, accessible recovery path. Show estimated wait times for lockouts.

### 15.2 Permission Requests

- Request permissions **at the moment of need**, not on first launch. Explain the specific benefit before prompting (e.g., "Allow location to find nearby stores").
- If a permission is denied, degrade gracefully. Never repeatedly prompt or block the app.
- Group related permissions logically. Never request camera, microphone, location, and contacts in a single burst.

### 15.3 AI Confidence and Uncertainty

- When displaying AI-generated results, show **confidence indicators** where applicable (e.g., "High confidence", "Needs review").
- Clearly distinguish between verified facts and AI-generated inferences.
- Provide a visible path to challenge, correct, or override AI outputs.
- Never hide the source of a recommendation behind vague labels like "Suggested for you" without explanation.

---

## 16. Systems and Service Design

### 16.1 Design System Governance

- Use a **strict token hierarchy**: global primitives > alias tokens > component tokens. Never reference primitives directly in component code.
- Version the design system. Breaking changes require a major version bump and a documented migration path.
- Deprecate components with a minimum 2-release warning period. Never silently remove.

### 16.2 Cross-Channel Journey Mapping

- Design for the full journey, not isolated screens. Ensure coherence across in-app, email, push notification, SMS, and physical touchpoints.
- Notifications must deep-link to the exact relevant state in-app, not a generic home screen.
- Maintain context across channels: if a user starts a task on mobile, desktop must allow seamless continuation.

### 16.3 Offline-First and Degraded Connectivity

- Cache critical UI shell and recently accessed data for offline use.
- Clearly indicate offline status without blocking interaction. Allow queued actions that sync when connectivity returns.
- Show **last-updated timestamps** on all cached data so users know what is stale.

---

## 17. Platform-Specific Conventions

### 17.1 iOS vs. Android

| Concern | iOS Convention | Android Convention |
|---|---|---|
| Navigation | Tab bar (bottom), swipe-back gesture | Bottom nav or nav drawer, system back button |
| Actions | Trailing-edge primary action | FAB (Floating Action Button) for primary action |
| Typography | SF Pro / New York | Roboto / Google Sans |
| Modals | Sheet-based (half/full) | Bottom sheet or full-screen dialog |

Respect platform conventions. Do not force iOS patterns on Android or vice versa.

### 17.2 Desktop and Keyboard-First Workflows

- Support **comprehensive keyboard shortcuts** for all frequent actions. Display shortcut hints in tooltips and menus.
- Implement focus trapping in modals and dialogs. Escape must always dismiss.
- Support right-click context menus for power-user actions.
- Enable drag-and-drop for reordering, file upload, and cross-panel operations.

### 17.3 Wearable and Glanceable Design

- Design for **glanceability**: convey the primary information within 3 seconds.
- Limit interactions to 1-2 taps. Use swipe gestures for quick actions.
- Use large, high-contrast type. Minimum 11pt on watch faces.
- Prefer complications and notifications over requiring the user to launch an app.

---

## 18. Ethical Design

### 18.1 Prohibited Dark Patterns

Never generate any of the following:

| Pattern | Description |
|---|---|
| Confirmshaming | Guilt-tripping copy on decline buttons |
| Hidden costs | Fees revealed only at final checkout step |
| Roach motel | Easy sign-up, difficult cancellation |
| Forced continuity | Silent trial-to-paid conversion |
| Asymmetric buttons | Visually demoting the "Reject" option |
| Sneaking | Pre-checked add-ons in cart |
| Algorithmic gaslighting | Synthetic emotional cues to pressure decisions |

### 18.2 Consent and Transparency

- Consent prompts must use **symmetric design**: "Accept All" and "Reject All" get equal visual weight.
- Show total price from the first product screen. No drip pricing.
- Cancellation flows must be as simple as sign-up flows.
- Disclose when the user is interacting with an AI agent. Never simulate human identity.

---

## 19. Research and Validation

### 19.1 Avoid the Synthetic Persona Fallacy

- AI-generated personas and synthetic user responses are **brainstorming aids only**. They must never replace real user research.
- All synthetically generated insights must be validated against real user data before informing design decisions.

### 19.2 Evaluation Stack for AI-Driven Products

Evaluate generated interfaces using this four-layer stack:

1. **Automated metrics** — Run large-scale evaluations for relevancy, logic failures, and consistency.
2. **Hallucination detection** — Deploy real-time monitoring to catch factual errors and quality drift.
3. **Expert review** — Domain specialists review representative samples for subjective failures.
4. **User testing** — Test with real users. Include variance testing (same prompt, different outputs), confidence rating, and recovery pattern analysis.

### 19.3 Analytics Integration

- Use predictive heatmaps and AI-simulated attention maps pre-launch, but always validate post-launch with real behavioral data.
- Monitor intent completion rates and sentiment signals to identify failure points.
- Leverage real-time emotion detection (42ms latency) to trigger contextual assistance when users show frustration signals.

---

## 20. Pre-Generation Checklist

Before outputting any UI/UX design, verify — ordered by manual section:

- [ ] Every element serves a clear user goal (Section 1)
- [ ] Design pillars are defined with weighted emotional targets; none contradicted (Section 2)
- [ ] Output format is determined and appropriate for the task (Section 3)
- [ ] Color contrast ratios meet minimums — 4.5:1 text, 3:1 non-text (Section 7)
- [ ] Shape language and saturation hierarchy reinforce meaning, not color alone (Section 7)
- [ ] Icons pass the silhouette test — identifiable as solid black fills (Section 7)
- [ ] Design system tokens (color, type, spacing) applied consistently (Sections 5-7)
- [ ] Motion respects `prefers-reduced-motion`; translucency has an opacity fallback (Section 5)
- [ ] Touch/click targets meet minimum size — 44x44px mobile, 60pt spatial (Section 8)
- [ ] In-progress operations are cancelable; user input is never silently dropped (Section 9)
- [ ] All friction points pass the intentional friction test — protects user, not business metric (Section 9)
- [ ] Empty, error, and loading states are designed — not just the happy path (Section 9)
- [ ] Plain language throughout; no unexplained jargon (Section 10)
- [ ] Strings accommodate i18n expansion and RTL layouts (Section 10)
- [ ] Cognitive load stays within working memory limits — 5-9 items per group (Section 11)
- [ ] All interactive elements are keyboard-accessible with visible focus indicators (Section 12)
- [ ] Layout adapts to mobile, desktop, spatial, and foldable contexts (Section 13)
- [ ] Core Web Vitals targets are met — LCP < 2.5s, CLS < 0.1, INP < 200ms (Section 14)
- [ ] AI-generated content is clearly identified as such (Section 15)
- [ ] Permissions are requested contextually, not on first launch (Section 15)
- [ ] Offline and degraded-connectivity states are handled gracefully (Section 16)
- [ ] Platform conventions (iOS, Android, desktop, wearable) are respected (Section 17)
- [ ] No dark patterns present in copy, layout, or flow (Section 18)
- [ ] The interface explains its own reasoning when dynamically generated (Section 8)
- [ ] All deviations from this manual are documented per the deviation protocol (Section 1)

---

*This manual codifies enforceable standards. Treat each directive as a hard constraint subject to the conflict resolution hierarchy (Section 1.1) and the documented deviation protocol (Section 1.2). When trade-offs arise outside those protocols, resolve in favor of accessibility, clarity, and user autonomy — in that order.*
