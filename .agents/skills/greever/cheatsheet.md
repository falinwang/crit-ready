# Cheatsheet

## Decision Rules

- **Rule of Three Validation**: If you cannot clearly answer (1) What problem does it solve?, (2) How does it affect the user?, and (3) Why is it better than the alternative?, the design is not ready to present.
- **Communication Primacy Rule**: Communicating about the design is more important than creating the design itself. A brilliant design without stakeholder support will never ship.
- **Goal Anchoring Rule**: If the business has not provided metrics or KPIs, define them yourself before presenting; never defend a design in an unanchored subjective vacuum.
- **Communication-First Inquiry**: Before discussing layouts, assets, or colors, always ask: *"What are we trying to communicate?"*
- **Momentum over Consensus**: Aim for organizational support to proceed, not unanimous personal preference.
- **Rule of Nobler Motives**: When feedback diverges into personal opinions or tangential features, pull the conversation back to the agreed project phase goal/KPI; move non-essential items to the future backlog.
- **Rule of Direct Comparison**: If a stakeholder insists their design idea is better, never present their idea in isolation. Always display both options side-by-side on one canvas with a dividing line.
- **Rule of Trade-Offs (Rubik's Cube)**: Never say a flat "No" to a feature request. Instead, specify the sacrifice: name the exact feature, screen real estate, or deadline that must be dropped to accommodate it.
- **Rule of Named Inquiries**: When seeking group support, never ask *"Does everyone agree?"* or *"What does the group think?"* Ask a specific ally by name: *"[Name], what is your perspective on this?"*
- **Rule of Tactical Pausing**: If a meeting enters design-by-committee or people start dictating pixel tweaks on your screen, stop the discussion immediately and postpone the decision by hours or days to iterate privately.
- **Rule of Concrete Data Backing**: Whenever citing analytics, always have the source report, chart, or table ready to show or send immediately.
- **Rule of Use-Case Primacy**: Optimize screens strictly for the primary use case. Subordinate edge cases and secondary tasks into dropdowns, progressive disclosure, or secondary menus.
- **The IDEAL Rule**: Never present a solution without first anchoring the problem and following with user empathy, business metrics, and an explicit ask for agreement.
- **The 60-Minute Follow-Up Rule**: Always send the written follow-up within 1 hour while decisions are fresh and before stakeholders reconsider or forget.
- **The 4-Filter Test for Feedback Omission**: Leave a comment/idea off the follow-up notes ONLY IF: The speaker was casually riffing, the room was indifferent, the speaker is not a critical decision-maker, and the speaker is unlikely to raise it again unprompted.
- **The Ambiguity Default Rule**: If stakeholders refuse to decide due to politeness or apathy, make the decision yourself, document it, give a deadline, and proceed if no one objects.
- **The Consequence Choice Rule**: When resisting bad stakeholder requests, always frame the choice against business KPIs or launch dates rather than personal taste.
- **If an executive seems disoriented or detached**: Immediately pause, state the business goal, show the process timeline, and link the screen to their high-level vision.
- **If feedback attacks your personality or role**: Stop and apply attribution theory—assume an unstated situational pressure, not malice or design incompetence.
- **If a stakeholder obsesses over a placeholder or minor detail**: Never debate it twice; clean it up immediately after the meeting. Distractions must only happen once.
- **If communicating design updates asynchronously**: Never paste raw images into Slack/Teams/tickets; record a 2.5–5 minute screen + face video walkthrough.
- **If walking into a high-stakes executive review**: Never present solo; align key swing votes in 1-on-1s beforehand and hold a 5-minute pregame huddle.
- **If a stakeholder presents an explicit solution ("Move this button")** $\rightarrow$ Do not debate the placement; ask: *"What problem are you trying to solve by suggesting this?"*
- **If feedback uses preference language ("I don't like this")** $\rightarrow$ Reframe to effectiveness: *"Why doesn't it work to have it here?"*
- **If you are about to respond to any critique or suggestion** $\rightarrow$ Force the first word to be *"Yes"* (agreeing on the problem, value, or goal), and never follow it with *"but"* or *"however"*.
- **The Core Task Test**: If a proposed change does not disrupt the user's primary journey or violate accessibility/usability standards, concede the point to make a deposit in the Bank of Trust.
- **The 10/90 Recovery Rule**: When a design blunders, spend 10% of your time acknowledging the failure ("I was wrong") and 90% presenting the concrete remediation plan and timeline. Never volunteer defensive justifications.
- **The Three Red Flags of Being Wrong**: Concede that your design is wrong when: The problem still exists, users don't get it, or you lack internal support.
- **The Preference Ban**: Eliminate "like" and "dislike" from design critiques. Frame every critique in terms of "works" or "does not work" relative to documented user goals.
- **The Committee Ban**: Every project must identify exactly one final decision-maker per core discipline (Business, Product, Design, Engineering, Content). Never let design decisions be made by committee vote.

---

## Tells & Smells

- **Smell: The "CEO Button"** — An executive drops in with an out-of-the-blue feature request. *(Tell: Executive lacks visibility into how current designs address their high-level business goals).*
- **Smell: Home Page Syndrome** — Stakeholders fight for landing page real estate for every feature. *(Tell: Project lacks clear metric prioritization and hierarchy).*
- **Smell: Design-by-Committee** — Meetings turn into feature-swapping and endless micro-tweaks. *(Tell: Designer is presenting solutions without articulating the underlying problem and alternatives).*
- **Smell: The "Why did we do this?" Loop** — Stakeholders re-open settled design decisions in later meetings. *(Tell: Prior rationale was neither memorable, compelling, nor documented).*
- **Smell: Aesthetic Jargon Trap** — Defending work with phrases like "it's clean" or "good use of whitespace". *(Tell: The designer is leaning on subjective aesthetics rather than problem-solving logic).*
- **The "Big Button" Tell**: When a stakeholder says *"Just add a big button here,"* they lack design vocabulary. Do not add the button; uncover the underlying visibility or priority concern and offer a refined UI control.
- **The Frankenstein Solution Smell**: When five people in a room start combining multiple competing ideas into one hybrid UI, design-by-committee is happening. Adjourn the meeting and reclaim control of the canvas.
- **The Triviality Spiral Tell**: When an entire meeting gets bogged down in minor stylistic debates (icons, spinners, subtle colors) while core conversion flows remain unresolved, the meeting has lost its nobler motive.
- **Passive Non-Agreement Smell**: Stakeholders nod silently and start chatting about another topic. *(False consensus. They will reopen the debate next week).*
- **Post-Meeting Politics Tell**: An executive stays quiet, but middle managers linger in the hall after the meeting. *(The real decisions happen outside the formal room).*
- **Brainstorming Riff Smell**: Stakeholder suggests an extravagant, out-of-scope technology. *(The speaker likes hearing themselves talk; no commitment behind it).*
- **Analysis Paralysis Smell**: Team spends 20 minutes debating without reaching a conclusion. *(Politeness or lack of conviction is freezing the project).*
- **Follow-Up Failure Smell**: Feedback arrives weeks later claiming "we never agreed to this." *(Missing paper trail allowed retroactive revisionism).*
- **Attribution Fallacy Smell**: Thinking "They just don't get UX" or "They're just difficult" when a stakeholder pushes back.
- **The Disoriented Opening Smell**: Stakeholder enters the meeting and immediately asks "What are we looking at here?" or begins critiquing button colors on a low-fi conceptual wireframe.
- **The Lonely Defender Smell**: The designer sits alone trying to defend every pixel while the entire room offers critique.
- **"Oh, that's interesting. Why did you do that?" Tell**: Polite disagreement. They think an alternate approach is better but avoid direct confrontation.
- **Lukewarm praise ("Wow, nice, but you really shouldn't be spending time on this.") Tell**: Hidden organizational agenda, impending shutdown/pivot, or misaligned strategic priorities.
- **"Yes, but..." or "Yes, however..." Tell**: You just told the stakeholder "No" while pretending to agree, triggering defensiveness.
- **Bike-Shedding Smell**: Stakeholders spend 40 minutes debating a button label or icon color while skimming past core navigation architecture.
- **The "Jim" Syndrome Smell**: A designer responds to stakeholder pushback with defensiveness, complains that stakeholders "just don't get modern design," and retreats into isolation churning out more wireframes.
- **User Blame Smell**: A designer asserts: *"The interface is obvious; our users just aren't tech-savvy enough to understand modern mobile patterns"*.
- **Unprepared Critique Smell**: A stakeholder opens a review with: *"I didn't have time to look at what you sent, but looking at it right now..."*

---

## Trade-offs Summary & Matrix

- **Prep Time vs. Execution Time**: Allocating substantial hours to presentation rehearsals, written rationale, and alternative wireframes reduces raw design output, but saves exponentially more time in prevented rework and approvals.
- **Intuitive Flow vs. Conscious Rationalization**: Breaking flow states to document micro-decisions feels slow and tedious, but is essential for defending decisions to nondesigners.
- **Consensus vs. Velocity**: Seeking "support" allows fast iteration but requires relational capital, whereas seeking "unanimous consensus" guarantees slow progress and diluted solutions.
- **Side-by-Side Comparison vs. Time**: Creating mockups of bad stakeholder suggestions takes time, but saves hours of circular verbal debate.
- **Hard Data vs. Usability Stories**: Analytics provide quantitative proof that convinces executives quickly, but lacks the emotional empathy and contextual "why" found in qualitative usability clips.
- **Immediate Agreement vs. Postponement**: Forcing a consensus in the room risks agreeing to a botched compromise; postponing preserves UX quality at the expense of temporary meeting friction.
- **Standard Controls vs. Custom Flair**: Standard HTML/system controls look less "unique" but ensure accessibility, fast load times, lower dev costs, and familiar mental models.
- **Citing Research vs. Stakeholder Ambush**: Citing external research provides authority, but overloading unprepared stakeholders can make them defensive; share research ahead of time.
- **High-Fidelity Prep vs. Agile Speed**: Spending time polishing wireframe grids, researching realistic copy, and replacing placeholders violates ultra-lean rapid prototyping, but avoids hours of derailed conversations and false rework.
- **Showing Alternatives vs. Decision Paralysis**: Preparing multiple design options controls the comparison and demonstrates thoroughness, but risks stakeholders choosing a suboptimal variant if comparative articulation fails.
- **Vision Presentation vs. Immediate Scope Creep**: Showing a visionary future excites leadership and wins MVP buy-in, but risks stakeholders demanding visionary features in v1.
- **Data-Heavy Defense vs. Stakeholder Engagement**: Having research/metrics ready provides rock-solid defense against skepticism, but leading with data too aggressively can intimidate stakeholders, stifle discussion, or trigger debates over sample size and methodology.
- **Async Video vs. Live Dialogue**: Video captures body language and respects calendar autonomy, but lacks real-time collaborative pivoting and immediate resolution.
- **Conceding on Secondary Issues vs. Defending Every Detail**: Conceding protects the trust account and preserves stakeholder goodwill at the expense of minor design imperfections; stubbornly defending every detail preserves visual purity at the cost of being labeled difficult, arrogant, and untrustworthy.
- **Daily 30-Minute Check-ins vs. Weekly Design Reviews**: Daily check-ins require recurring calendar discipline and frequent stakeholder context switches, but prevent days of misdirected design work; weekly reviews free up calendar blocks, but double project duration due to compounded misalignments.
- **Action-Oriented Admission vs. Historical Justification**: Ripping off the bandage and admitting fault without excuses bruises personal ego and accepts short-term blame, but instantly earns credibility and re-establishes leadership; offering detailed historical defenses temporarily protects pride, but sounds like weak excuse-making.
- **Decisive Iteration vs. Prolonged Consensus Seeking**: Empowering designers to make imperfect calls and iterate live in production risks minor initial missteps, but maintains rapid momentum; waiting for cross-functional consensus eliminates individual risk, but causes projects to stagnate in bureaucratic paralysis.
- **Executive Suite Proximity vs. Studio Silo Isolation**: Placing design leadership near executives exposes designers to spontaneous executive interruptions and political turbulence, but guarantees a direct voice in high-level strategic alignment and prevents disconnected top-down mandates.
