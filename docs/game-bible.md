# Reorg - Game Bible

> Source of truth. If code and this doc disagree, fix one of them in the same PR.
> Numbers marked **(t)** are tunable balance guesses. Market context: [market-research.md](market-research.md).

## 1. Pitch

**Reorg** is an online office-politics strategy game for 3-6 players.
**Ship the quarter together. Survive the review alone.**

Browser first, plays live (25 min) or async (one move a day). Sharp satire, plain 2D.

## 2. Pillars

| Pillar | Means |
|---|---|
| Team vs greed | If the company fails, everyone loses. But only one person wins. |
| Satire lives in the rules | Credit theft, meetings, burnout are mechanics, not just jokes. Mock the system, never the player. |
| Plays where offices live | Browser link, no install, async turns between real work. |
| Short, readable turns | One screen, one decision set, under 90 seconds. |
| Nobody sits out | Getting cut changes your role, never ends your game. |

## 3. Roles

| Role | Who | Goal |
|---|---|---|
| **Employee** | Every player at start | Highest Career Score while the company survives |
| **Manager** | Optional human (needs 4+ players) or AI | Hit targets, avoid Legal Strikes, own secret goal |
| **Consultant** | Any cut player | Keep scoring from outside: fees, leaks, revenge |

**AI Manager personalities** (shown at match start):

| Personality | Patrols | Cuts |
|---|---|---|
| Numbers | Desks | Lowest Performance this quarter |
| Optics | Meeting Room | Lowest Visibility |
| Favorites | Kitchen, own office | Lowest Trust with Manager |
| Chaos | Random | Weighted random (low Visibility = more likely) |

MVP ships Numbers + Optics.

## 4. Meters

| Meter | Range | Start | Meaning |
|---|---|---|---|
| Performance (P) | 0+ | 0 | Real output. Also feeds the team target. |
| Visibility (V) | 0-10 | 3 | What leadership *thinks* you do. |
| Wellbeing (W) | 0-10 | 7 | Work-life balance. **0 = Burnout**: next week all blocks forced Home, no output. |
| Trust | -3..+3 per pair | 0 | Relationships. Drives deals, betrayal cost, cut fallout. |
| **Company Health** | 0-10 (shared) | 5 | Team gate. **0 = company folds, everyone loses.** |

True P and W are hidden from others. V is public. Trust you see only for your own pairs.

## 5. Match structure

1 match = 1 fiscal year = **4 quarters x 3 weeks = 12 turns**, plus a Performance Review after each quarter.

| Mode | Turn timer | Length |
|---|---|---|
| Live | 90 s (t) | ~25-30 min |
| Async | Host sets 4h / 12h / 24h, weekends paused, resolves early when all submit | ~2.5 work weeks at 1 turn/day |

Missed turn = **Autopilot** (repeat last week's plan, no card).

## 6. A turn (one work week)

1. **Monday memo**: an Event card is revealed (rules twist for this week).
2. **Plan**: on the map, place your **40 hours as 8 blocks of 5h** into rooms. Up to **2 overtime blocks** (count as Desk, cost 2 W each) (t).
3. **Politics**: play 0 or 1 card from your hand.
4. **Talk**: #general, DMs, give or call in Favors. All promises are non-binding.
5. **Reveal**: everything resolves at once. A plain-language log tells the story ("Priya took credit for Sam's deck.").

Baseline: everyone loses **2 W per week** (the week happened) (t).

## 7. The map

Static, plain top-down office. Click a room to go there and add blocks. No real-time movement.

| Room | Per block (t) | Notes |
|---|---|---|
| Desk | +1 P, +1 team output | The honest choice |
| Meeting Room | +1 V | Meetings eat work. Alone it is "just a calendar block": 0 V |
| Manager's Office | +2 V, max 2 blocks count | 2+ visitors same week: everyone there -1 Trust with each other (brown-nosing pileup) |
| Kitchen | +1 Trust with each other player there | 2+ present: **Gossip**, each sees one hidden stat of someone present |
| Coworker's Desk (Help X) | X gets +1 P and team output, you +1 Trust with X | You get no P |
| Gym | +1 W | Safe slacking |
| Home | +2 W | Risky if pinged |

**Manager patrol** (the "avoid the boss" mind game): each week the Manager visits **2 rooms** (AI: per personality; human: chosen). Anyone in a patrolled room:
- Desk / Meeting / Helping: **seen working, +1 V**
- Kitchen / Gym: **seen slacking, -1 V**
- Home: **"you there?" ping unanswered, -2 V**

## 8. Politics cards

Hand of 3, draw 1 per week. 12 at launch (t):

| Card | Effect |
|---|---|
| Take Credit | Target shares a room with you: move 2 of their P to you. They lose 2 Trust with you. |
| Cc the Boss | You +2 V, target -1 V, target -1 Trust with you |
| Call a Meeting | Move 2 of target's blocks to Meeting Room |
| Reply All | Everyone -1 W, you +1 V |
| Sick Day | 2 of your blocks become Home, no patrol risk |
| Coffee Run | Everyone in Kitchen with you: +1 Trust, +1 W |
| Document It | Blocks Take Credit / Cc the Boss against you and reflects it back |
| Out of Office | Immune to patrol this week |
| Skip-Level | You +3 V, -2 Trust with Manager |
| Postmortem | If team output is behind pace, target -2 V |
| Volunteer for the Offsite | +1 Trust with everyone, -1 W |
| Focus Block | 1 Desk block counts double, cannot be pulled into meetings |

## 9. Event cards (Monday memo)

~20 at launch (t). Examples: **RTO Mandate** (Home ping penalty doubled), **AI Pilot** (Desk output +50%, Manager cuts 2 at next review if allowed), **Hiring Freeze** (no rehires), **Offsite** (Kitchen effects doubled), **Server Outage** (target +4), **Wellness Week** (Gym +2 W), **Reorg Rumor** (everyone reveals their secret goal's category), **Pizza Friday** (+1 W all), **Quarter-end Crunch** (overtime costs 1 W).

## 10. Talking and dealing

| Tool | Use |
|---|---|
| #general | Public channel, visible to all incl. Manager |
| DMs | Private backroom deals |
| Favor tokens | Give one as a promise. Holder can call it in once: you must Help them 1 block next week or lose 2 Trust with everyone. |

Text only. Groups bring their own voice (Discord/Teams).

## 11. Performance Review and The Cut

After every quarter:

1. **Team target**: required team output = **15 x employees** per quarter (t). Hit: Health +1. Miss: Health -2. Miss by 30%+: Health -3.
2. **Bonus**: top P this quarter +3 Career.
3. **Promotion** (after Q2 and Q4): highest V (tie: P) +5 Career.
4. **The Cut** (after Q1, Q2, Q3 only): 1 employee is cut. **Never below 2 employees.**

**Human Manager cuts freely, but pays:**

| If the cut person... | Consequence |
|---|---|
| Had the top P | Health -2 |
| Had average Trust +2 or more | Every employee -2 W (morale) |
| Has fewer than 2 Documentation marks | **Legal Strike**. 2 strikes: HR cuts the Manager, AI Manager takes over. |

**AI Manager** cuts by personality rule (section 3).

**Rehire**: at a review the Manager may rehire 1 Consultant: Health -1, they return with V 2.

## 12. Human Manager turn

Manager gets 8 blocks too:

| Action | Effect |
|---|---|
| Walk the floor | Patrol 1 room (max 2) |
| 1:1 with X | See X's true P and W, +1 Trust both ways |
| Document X | +1 Documentation mark on X (needed for a clean cut) |
| Report Up | Smooths a miss: next missed target costs 1 less Health |
| Recharge | +1 Manager W |

Manager score: Health x3 + targets hit x3 + avg employee W + secret goal - Legal Strikes x5 (t).

## 13. Consultants (cut players)

No hours. 1 action per week:

| Action | Effect |
|---|---|
| Invoice | +2 Career (fees) |
| Leak | Publicly reveal one employee's true P, W or secret goal category |
| Poach | Offer an employee a job. If they accept at the next review they leave voluntarily: +8 Career, become Consultant (does not count as a Cut) |
| Advise | Target +1 or -1 V (the Manager listens to consultants) |

Consultants keep their score and **can still win**.

## 14. Secret goals

Each player is dealt 1 secret goal, worth **+10 Career** (t). 20 at launch, 10 in MVP:

Job Hunter (get Poached), Climber (2 promotions), Ally (named player never cut), Rival (named player cut before you), Quiet Quitter (fewest Desk blocks, never cut), Office Parent (most Help given), Work-Life Hero (W 7+ at every review), Teacher's Pet (Trust +3 with Manager), Gossip (10+ Kitchen blocks), Overachiever (top P in 2 quarters), Ghost (never caught by patrol), Networker (Trust +2 with 3 players), Union Rep (all employees end with W 5+), Hero (team hits all 4 targets), Credit Thief (3 successful Take Credits), Meeting Person (12+ Meeting blocks), Exit Strategy (V 8+ at Q3 then leave), Lifer (survive all reviews with V 5+), Firefighter (Help during 3 missed-pace weeks), Spotlight (V 10 once).

Manager goals: Clean Hands (no Legal Strikes, 3 cuts), Numbers Guy (all 4 targets), People First (avg W 6+ at end).

## 15. Winning

1. If Health hits 0 at any point: **company folds, everyone loses** (Manager too).
2. Else highest **Career Score** wins:

| Source | Points (t) |
|---|---|
| Performance | 1 per P |
| Visibility (end) | 2 per V |
| Wellbeing (end) | 2 per W |
| Promotion | +5 each |
| Quarter bonus | +3 each |
| Secret goal | +10 |
| Consultant fees, poach bonus | as earned |

## 16. Modes

| Mode | Players | Bots | Price |
|---|---|---|---|
| Multiplayer Live | 3-6 humans | None | Host needs license |
| Multiplayer Async | 3-6 humans | None | Host needs license |
| Solo Practice | 1 + AI coworkers + AI Manager | Yes | Free |
| **Daily Workday** | 1 vs AI, same seed for everyone | Yes | Free |

**Daily Workday**: one quarter (3 weeks + mini review) in 3-5 minutes. Same seed worldwide each day. Did you survive, and with what score? Wordle-style share card:
`Reorg Daily #142 | P 9 | V +3 | W 6 | Survived`
Leaderboards: friends, league, global.

## 17. Groups and competition

**Private Leagues** (host creates, invite link):
- Season = N matches (default 6) (t).
- Placement points: 1st 10, 2nd 6, 3rd 4, 4th 3, 5th 2, 6th 1. Company folds: 0 for all.
- Joke awards: Employee of the Season, Golden Parachute (most consultant fees), Teflon (never cut), Burnout Award (lowest avg W).
- League Daily leaderboard.

**Parked** (not in scope until demand proves it): ranked ladder, public lobbies, company leaderboards, tournaments.

**Matchmaking**: invite-only (link or code). Guests can join with a display name; accounts needed for leagues and purchases.

## 18. Monetization: host pays (Jackbox model)

| Free | Host License (one-time, ~$9.99 (t)) |
|---|---|
| Join any match | Host live and async matches |
| Daily Workday | Create leagues |
| Solo Practice | Custom settings (length, timers, Manager on/off) |

- Only one person per group pays, so invites have no friction. Every guest is a future host.
- **Steam** version is paid and includes the Host License. Same account, cross-play with web.
- Web payments via a merchant of record (Paddle or Lemon Squeezy) so global VAT is handled for us.
- Later: map packs (Startup, Bank, Remote-only), cosmetics. Never pay-to-win.

## 19. Setting, art, audio

- First map: **mid-size tech company**. Standups, tickets, AI pilots, RTO memos.
- Flat 2D, SVG rooms, simple avatars, one accent color per player. Readable over pretty.
- Minimal SFX (Slack-like pings, keyboard clacks). No music in MVP.
- Tone: sharp, funny, punches up at the system.

## 20. Tech

**.NET 10 / C#, Blazor everywhere.**

| Folder | Project | What |
|---|---|---|
| `src/core` | Reorg.Core | Rules engine: immutable state, `Resolve(state, orders, seed)`, seeded RNG, AI coworkers and Managers. No platform or network code. |
| `src/ui` | Reorg.Ui | Razor class library: map, panels, chat. Shared by web and app. |
| `src/web` | Reorg.Web | Blazor Web App. **Browser first.** |
| `src/app` | Reorg.App | MAUI Blazor Hybrid shell: Windows (Steam), Android later. |
| `src/server` | Reorg.Server | ASP.NET Core + SignalR, authoritative. Matches, async turn scheduler, auth, EF Core + PostgreSQL. |
| `src/sim` | Reorg.Sim | Console: runs thousands of bot matches for balance. |
| `test/core-tests/...` | | Mirrors source tree (repo conventions). |

- Server is the only judge of rules. Clients send orders, never results.
- Async notifications: email + optional Discord/Slack webhook per match or league.
- Hosting: one container + managed PostgreSQL. Add a SignalR backplane only when running more than one instance.

**Steam path**: Steam Direct fee $100 per app -> unpackaged Windows build of Reorg.App -> Steamworks.NET (login, achievements, friend invites) -> upload with SteamPipe -> store page early for wishlists -> Next Fest demo -> launch.

| Known risk | Plan |
|---|---|
| Steam overlay does not render over WebView2 | Not needed: invites via Steam friends list / rich presence |
| MAUI has no Linux (Steam Deck) | Test Windows build under Proton early. Fallback: Photino.Blazor |

## 21. MVP (part-time, ~3 months)

**In:** Reorg.Core + tests, 1 map, Live multiplayer 3-6, AI Manager (Numbers, Optics), Consultants, 12 cards, 10 events, 10 secret goals, chat + DMs + Favors, invite links, guest join.

**Out:** async, human Manager, Daily, Solo Practice, leagues, payments, Steam, mobile.

**MVP is done when** 3 friend groups finish a full match and at least 2 ask to play again.

## 22. Roadmap

| Milestone | Scope |
|---|---|
| M1 | MVP + friends playtests, balance with Reorg.Sim |
| M2 | Async mode, human Manager, Solo Practice, Daily Workday |
| M3 | Accounts, Private Leagues, Host License, public web launch |
| M4 | Steam page, Next Fest demo, Steam launch |
| Later | Android/iOS, map packs, public lobbies, Discord Activity, B2B team plan |

**Split suggestion**: one owns Core + Sim + bots, the other owns Server + UI. Both own this doc.

## 23. Success metrics

| Metric | Target (t) |
|---|---|
| Live match completion | 85%+ |
| Async match completion | 60%+ |
| Groups that start a 2nd match within 7 days | 50%+ |
| Daily D7 return | 30%+ |
| Guest to host conversion | 10%+ |

## 24. Risks

| Risk | Mitigation |
|---|---|
| Needs 3 humans online | Async mode, Daily and Practice keep solo players around |
| Balance (dominant strategy, e.g. always Kitchen) | Reorg.Sim bot matches before every playtest |
| Chat abuse | Invite-only, mute, host kick |
| Sensitive topic (layoffs) | Mock the system, never real people or companies |
| Name clash ("Reorg" = former Octus brand) | Trademark check before store page |
| Scope creep | This doc. New feature = update the doc first. |

## 25. Open questions (parked)

- Final price and regional pricing.
- Scoring weights (decide from Sim + playtests).
- Daily anti-cheat (server-validated replays?).
- Minimum players for a human Manager (4 or 5?).
- Steam Deck: Proton good enough, or Photino?

## 26. Glossary

| Term | Meaning |
|---|---|
| Block | 5 hours placed in one room |
| Cut | Being laid off at a Review. You become a Consultant. |
| Consultant | Cut player who keeps playing from outside |
| Health | Shared company meter. 0 = everyone loses. |
| Review | End-of-quarter scoring, promotion, Cut |
| Patrol | Manager visiting rooms; catches slackers |
| Favor | Promise token, can be called in once |
| Daily Workday | Free daily solo puzzle, same seed for everyone |
