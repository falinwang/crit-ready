# Chapter 7: Choose a Message

## Core Idea
Designers can rely on a core set of twelve reusable, pre-formulated messages across four categories (Business, Design, Research, Limitations) to quickly and effectively justify their design decisions during stakeholder meetings.

## Frameworks Introduced
- **The Twelve Core Messages**: A categorization of common justifications for design decisions.
  - When to use: During meetings when you need to quickly articulate a rationale for a design decision.
  - How: Select the appropriate message template based on the context (Business, Design, Research, or Limitations) and map it to your specific situation.

## Key Concepts
- **Business Category**: Connecting design choices to company success. (Helps achieve a goal, Facilitates a use case, Communicates branding).
- **Design Category**: Justifying choices based on interface best practices. (Uses a common pattern, Draws the user's attention, Creates a flow for the user).
- **Research Category**: Proving decisions with evidence. (Validated by data, Revealed in testing, Supported by other research).
- **Limitations Category**: Explaining design constraints. (Not enough resources, Limited by technology, Complies with a standard).
- **Reflective Data**: Data collected *after* changing a design to compare before and after, as opposed to existing data used to make informed guesses.

## Mental Models
- **The "Golden Ticket" of Data**: Data is the most scientific and convincing way to get support. It removes subjectivity. However, it only tells you *what* the user did, not *why*, meaning you still have to apply correct assumptions.
- **The Template Repertoire**: Instead of inventing a new argument for every piece of feedback, treat design defense like a pattern library of communication. You pull the right message pattern for the given situation.
- **The Research Ambush**: If you bring a mountain of external research to a meeting to prove a stakeholder wrong without giving them time to review it, they will feel ambushed and defensive, harming the relationship.

## Anti-patterns
- **Relying on Raw Numbers Without Context**: Dropping a spreadsheet of data on stakeholders without interpreting it. It fails because stakeholders need the designer to draw the connection between the metrics and the user behavior.
- **Design for Design's Sake**: Justifying a visual choice purely subjectively (e.g., "it looks better"). It fails because it lacks a functional rationale. Instead, explain how it "Draws the user's attention" to a specific action.
- **Breaking the Pattern for Edge Cases**: Making a custom UI component when a standard pattern exists. It fails because it increases development cost, breaks consistency, and confuses users.
- **Ignoring Technical/Resource Limits in Pursuit of Ideal UX**: Designing features that the company cannot afford to build or support (e.g., customer service can't handle it). It fails because a design that can't be implemented or maintained is useless.

## Worked Example
<!-- Reproduce one concrete example the author works through -->
**Taking Hamburger off the Menu**: The author tried multiple times to convince a client to drop the "hamburger menu" icon in favor of the word "Menu" on a mobile app, based on research that the icon is less effective. Simply telling the client wasn't convincing. For the next meeting, the author gathered multiple articles on the subject, opening them in browser tabs. When the agenda item came up, the author clicked through the tabs, summarizing the research. Impressed by the preparedness, the client admitted they lacked counter-evidence. This allowed them to restart the discussion, resulting in an A/B test of the two options. The decision was successfully moved forward because it was *Supported by other research*.

## Key Takeaways
1. Anchor your design decisions in one of four categories: Business, Design, Research, or Limitations.
2. The most powerful business arguments are those that prove your design helps achieve a specific KPI or facilitates the primary use case.
3. Defend UI choices by citing standard design patterns, explaining how visual hierarchy draws attention, or demonstrating how it preserves user flow.
4. Data is the ultimate trump card, but be careful not to manipulate it or make false assumptions about *why* the data looks the way it does.
5. Bring the user into the room by showing short video clips or quotes from usability testing.
6. Build a personal repository of external UX research to cite when defending standard best practices.
7. Don't hide behind limitations; use them proactively to explain why certain design requests (like custom controls or heavy features) are impractical given time, budget, or tech constraints.

## Connects To
- **Ch 6 (Form a Response)**: These twelve messages are the specific content used to execute the tactics (like "Propose an alternative") outlined in Chapter 6.
- **Ch 1 (The Big Three)**: The messages heavily rely on answering the three core questions (What problem does it solve? How does it affect the user? Why is it better?).
