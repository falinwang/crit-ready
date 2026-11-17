# Chapter 3: Design the Meeting

## Core Idea
Meetings are the primary interface where design decisions are approved or rejected. By treating the meeting itself as a design problem—optimizing for memory, reducing cognitive load, and removing distractions—you can free stakeholders to focus purely on the primary task of supporting your work.

## Frameworks Introduced
- **Setting the Context**: A structured opening sequence for every design meeting to orient stakeholders and prevent derailed conversations.
  - When to use: At the very beginning of any formal or informal design review.
  - How: 
    1. State the agreed-upon project goal.
    2. Summarize the last meeting's decisions.
    3. Show a timeline of where you are in the design process.
    4. Specify the exact type of feedback you need (and what you don't need).
    5. State the goal again to anchor the discussion.

## Key Concepts
- **Cognitive Load (in meetings)**: The limited mental capacity stakeholders bring to a meeting. Unnecessary clutter in mockups or disorganized agendas exhaust this capacity, making agreement harder.
- **Placeholder Distractions**: Elements in early designs (e.g., stock images, lorem ipsum copy, misaligned grids) that stakeholders fixate on, distracting them from the actual layout or flow being reviewed.
- **Design Advocates**: Allies (developers, other designers, friendly executives) who are pre-briefed to support your designs during the meeting, creating a sense of consensus.
- **Primacy and Recency**: The psychological principle that people remember the first and last things they hear in a meeting, while the middle gets lost.

## Mental Models
- **Anticipating Reactions**: The formula for predicting stakeholder feedback: Personality + Role/Values + Past Observed Reactions = Predictable Behavior.
- **The Element of Surprise**: Using unexpected elements (a joke, a strange image, a unique meeting format) to jolt stakeholders' attention and ensure they remember key decisions.

## Anti-patterns
- **Using Unrelated Placeholder Content**: Why it fails: Non-designers often cannot look past "wrong" data or images. They will spend the entire meeting arguing over an irrelevant stock photo rather than evaluating the user flow.
- **Async Design Discussions via Chat/Email**: Why it fails: Dropping static screenshots in chat lacks context, invites knee-jerk reactions, and strips away the designer's ability to control the narrative. Use screen-recorded video walkthroughs instead.
- **Fearing Alternative Designs**: Why it fails: Hiding alternative solutions out of fear the client will pick the "wrong" one leaves you vulnerable when they inevitably suggest an alternative themselves.

## Worked Example
<!-- Reproduce one concrete example the author works through -->
The author presented wireframes to a stakeholder who became obsessed with the left-hand navigation panel that the prototyping tool (Axure) automatically generated. The client loved it so much she suggested replacing the app's carefully designed hierarchy with this generic tool panel. Instead of arguing in the meeting, the author simply changed his workflow for the next review, sending direct HTML links that completely bypassed the tool's iframe wrapper. The distraction vanished, and the client never mentioned the left panel again.

## Key Takeaways
1. Name calendar invitations clearly (e.g., "Home Services UX Design") rather than vague titles like "Design Sync," and include a brief agenda in the invite.
2. Break up long presentations with visual transitions (changing slide background colors) to reset stakeholders' attention spans.
3. Bring alternative designs to the meeting as evidence that you explored other options and to control the discussion when stakeholders suggest changes.
4. Pre-wire the room by briefing your "design advocates" before the meeting so they can verbally support you and tip the scales.
5. If a visual distraction (like a bad placeholder icon) derails a meeting once, fix it immediately. Distractions should only happen once.

## Connects To
- **Ch 3**: Connects to the previous chapter's emphasis on empathy, translating that understanding into tangible meeting structures and artifacts.
- **User Experience (UX) Principles**: Takes core UX concepts (reducing friction, cognitive load, user flows) and applies them to the interpersonal space of running a meeting.
