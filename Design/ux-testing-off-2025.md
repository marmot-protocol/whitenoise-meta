# UX Testing at Oslo Freedom Forum 2025

## What is this doc?

We're planning to do user testing of the beta of White Noise with activists at HRF's Oslo Freedom Forum in late May 2025. This doc should be used to help us plan everything related to these sessions.

> [!CAUTION]
> This repo is public, please DON'T add any names of activists or other people we'll be working with to this doc. This is only to plan the questions and format of the testing we'd like to do and to add anonymous learnings to the doc once we've finished.

| Task                                                    | What we hope to learn                                                                |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Login with existing Nostr account                       | Can existing nostr users easily log in and use the app                               |
| Create new account                                      | Is it easy for new users to create a new account - do they understand what it means? |
| Onboarding flow - existing Nostr users                  | Can existing nostr users complete the steps needed to start sucure chat groups?      |
| Find contact to create new chat                         | Can new nostr users get set up for chats quickly and easily                          |
| Search for Nostr user (not followed) to create new chat |                                                                                      |
| Create new chat                                         |                                                                                      |
| View chat details and chat specific settings            |                                                                                      |
| Send message in chat                                    |                                                                                      |
| React to message in chat                                |                                                                                      |
| Reply to message in chat                                |                                                                                      |
| Send image in chat                                      |                                                                                      |
| Update your Nostr profile                               |                                                                                      |
| View connected relays                                   |                                                                                      |
| Set up NWC (for advanced Nostr users)                   |                                                                                      |
|                                                         |                                                                                      |
## A little context

Fourteen people gave us their time and honest reactions to help shape Whitenoise. They came from all over: Africa, Latin America, Europe, the Nordics, MENA, North America. Some were Bitcoin developers and educators. Others were human rights advocates, NGO workers, entrepreneurs. A few were deep in the Nostr ecosystem, others had never heard of it.

None of them were Freedom Fellows, and that was intentional. We wanted a real range of people, technical and non-technical, privacy-savvy and not, all of whom have one thing in common: they need tools that actually work when it counts.

All 14 sessions are included in this analysis.

---

## Who we spent time with

- Total participants - 14
We had a genuine mix of developers, advocates, and people with no technical background

---

## The numbers

Each participant was walked through eight core tasks. Here's how it went:

|Task|Completed|Where things got tricky|
|---|---|---|
|Create an account|13 / 14|No signal that a key had been created|
|Connect and start a chat|12 / 14|"No contacts found" was disorienting on first load|
|Send messages|14 / 14|Reaction button glitched; reply took some hunting to find|
|Update profile name|13 / 14|No confirmation after saving; keyboard hard to dismiss|
|Share contact / QR code|14 / 14|Private key sitting a little too close to the QR screen|
|Move to a new phone|10 / 14|Most participants weren't sure what nsec was or where to find it|
|Delete account|11 / 14|Easy to confuse sign out with delete; settings buried it|
|Add a second account|12 / 14|The + button wasn't easy to spot|

Messaging itself: 14 out of 14. Every single person got there. That's a good foundation to build from.

---

## What we heard and saw

Beyond the tasks, there were moments, reactions, and little comments that paint a fuller picture. Here are the themes that kept coming up.

### 1. The first impression is working

People lit up at the welcome screen. The logo landed well. The black and white aesthetic felt clean and intentional. The name Whitenoise resonated. One participant said they loved the icon straight away. Another appreciated the "secure, distributed, uncensored" framing.

The one thing worth looking at: most people couldn't quite tell what the app _does_ just from looking at it. One thought it might be a music app. The vibe is right, the story just needs a little more room to breathe on that welcome screen.

### 2. Account creation is smooth, it just goes quiet at the end

The account creation flow worked well. People clicked through without much friction. What several participants noticed is that once it's done, nothing happens. No confirmation, no little moment of "you're in." A few people asked aloud whether it had actually worked.

It's a small thing but it matters, especially for an app where the thing being created is a cryptographic identity. A simple signal that says "your account is ready" would go a long way.

### 3. The QR flow for connecting is good once you find it

Once people found the plus button and scanned a QR code, things clicked. The flow made sense, felt fast, and participants liked it. Getting there was the tricky part for some. A few headed to their profile first, others looked for a username search. The QR path is the right one, it just needs a bit more visibility when the chat list is empty.

### 4. Messaging feels natural

People sent messages, reacted, replied, and deleted without much trouble. The core experience works and that's worth celebrating. A few things to look at: the long press for reactions wasn't obvious to everyone, the three-dot menu took some finding, and there was a small bug where the reaction button stacked up multiple likes.

One participant said "that's cute" when they discovered reactions. That kind of reaction is exactly what you want.

### 5. Profile saving needs a small signal

Almost everyone who updated their profile name ran into the same moment: they saved, and then silence. Nothing to say it worked. Several people pressed save a second time just to be sure. A couple tried to dismiss the keyboard and found it unresponsive.

The display name vs. name distinction also tripped people up across the board. If the difference between the two isn't immediately obvious, it's worth simplifying or adding a short explanation next to each field.

### 6. QR sharing is great, just keep the private key safe

Finding the QR code was quick and felt intuitive to most participants. The feature itself is well placed. The thing to be thoughtful about is that the nsec (private key) is visible and copyable nearby, and the red warning didn't get read by most people. One participant suggested the copy button itself should be in the red zone, something that makes it _feel_ like the serious thing it is. This is a safety consideration worth prioritising.

### 7. Moving to a new phone revealed a gap worth closing

This task was the most revealing of the whole session. Four participants weren't able to complete it without support. The ones who got there quickly were already familiar with Nostr keys. For everyone else, the concept of an nsec, what it is, why it matters, where to find it, wasn't something the app had ever explained.

One participant said they'd just create a new account on the new phone. Another said they'd copy-paste their key through Signal. A small piece of onboarding, a gentle prompt to back up your key in plain language with a QR option, would make a huge difference for the people who need this app most.

### 8. Deleting an account takes more steps than it should

Three participants couldn't find the delete option without some guidance. The journey often went: try sign out (understandable), head to privacy and security, eventually find it. One participant noted that the collapsing settings sections looked more like an FAQ than navigation. Another signed out thinking that had deleted their account.

This one is worth cleaning up. Not because deleting is a common action, but because when someone needs to wipe their account quickly, they need to be able to do it quickly.

### 9. The wallet was a lovely surprise

Nobody expected a wallet. The reactions were warm. One participant who knew what NWC (Nostr Wallet Connect) is was visibly excited by it. That kind of moment is gold. For participants who weren't already in the Lightning ecosystem, the entry point just needs a bit more context so they know what they're looking at and where it can take them.

### 10. Technical language is a wall for some users

Relays, npub, nsec, NWC, key packages. For participants already in the Nostr world, this is home turf. For everyone else, these terms created confusion or got ignored entirely. One person asked if the relay list was like a phone carrier. Another said "I don't want to see these" and asked if they could be hidden.

The app doesn't need to simplify everything. It just needs a clear division between what someone new needs to see and what a more technical user wants to configure. Default to simple, and make the deeper settings findable for those who want them.

---

## What's already working well

It's worth pausing here because there's genuinely a lot going right.

- No phone number required. This was one of the most appreciated features across the board, especially for participants in sensitive advocacy contexts.
- The visual design: minimal, clean, black and white, got consistent positive feedback.
- QR code sharing: fast, intuitive, people found it satisfying to use.
- Multi-account support: participants who manage multiple identities appreciated this being built in.
- The core messaging experience: sending, reacting, and replying all worked well.
- The wallet integration concept: unexpected and exciting for the right audience.

---

## Recommendations

### Start here

- **Add confirmation feedback** after account creation, profile saves, and any action that changes state. A simple toast notification is enough. People need to know something happened.
- **Support the key backup flow.** Add a prompt during or right after onboarding that explains what the nsec is in plain language, why it matters, and gives people a QR option to transfer it safely to a new device.
- **Keep the private key separate from the QR sharing screen**, or make the warning impossible to miss. Consider a dedicated step before the private key is ever shown, so people have to actively choose to reveal it.
- **Fix the keyboard dismiss issue** on profile editing.

### Worth prioritising next

- When someone lands on an empty chat screen with "no contacts found," guide them. A simple empty state with a clear next step would help a lot.
- The delete account flow should be findable in two taps. Sign out and delete account should never feel like the same thing.
- Clarify display name vs. name. If the distinction matters, explain it. If it doesn't, simplify.
- Add plain-language explainers for Nostr concepts. Relays, keys, NWC: these need one-line descriptions next to them for users who aren't already in the ecosystem. Or give people the option to hide them by default.

### Nice to have down the road

- A welcome screen that tells people what the app actually does. The aesthetic is there, one line of clarity would complete it.
- Auto-save on profile edits, or at least a prompt when navigating away. The save button is being missed.
- Wallpaper or some visual customisation on the chat screen. Multiple participants commented it feels a little blank.
- A deep link or QR that works across apps for easier contact sharing.
- Group chat support: mentioned by several participants as something they'd need.
- A duress PIN feature, requested by one participant working in a high-risk context.
- Dark mode.

---

## Closing thoughts

Whitenoise is building something genuinely needed. The people in these tests, activists, Bitcoin educators, NGO workers, developers, are exactly the audience that needs a tool like this. And many of them liked what they saw.

The things that need attention are real but very fixable. Most of them come down to a few simple things: people need to know their actions worked, the language needs to meet users where they are, and the key backup flow needs to be as supported as the rest of the app. Those are very solvable problems.

The voices of these 14 participants represent a much bigger user base. The work is to make sure those users don't have to think too hard to stay safe. That's the whole point.

Thank you to everyone who showed up and shared their time and honest thoughts. It all feeds into building something better.