# CLAUDE CODE PROMPT: Build "The PM Pivot"

## Project Overview
Build a single-file HTML game called "The PM Pivot" - a satirical PM survival game in the style of Oregon Trail (1990). The player is a Product Manager trying to ship an onboarding experience during an AI pivot, balancing traditional coding vs AI tools while avoiding two fail states: becoming redundant (too much AI) or becoming a dinosaur (too little AI).

## Game Files Provided
I have the following pixel art images already created (in /images folder):
- `pm-sprint1.png` - Optimistic PM (Sprint 1)
- `pm-sprint2.png` - Focused PM (Sprint 2)
- `pm-sprint3.png` - Stressed PM (Sprint 3)
- `pm-sprint4.png` - Panicking PM (Sprint 4)
- `pm-sprint5.png` - Broken PM (Sprint 5)
- `pm-sprint6.png` - Zombie PM (Sprint 6)
- `penguin-alive.png` - Living penguin sprite
- `penguin-dead.png` - Dead penguin tombstone

## What You Need to Create
Generate the remaining graphics as pixel art using HTML Canvas or inline SVG in Oregon Trail 1990 style:

### ENDING SCREENS (Generate 6 screens as canvas/SVG):
1. **Automated Out** - Empty office desk with robot/AI sitting in chair
2. **Dinosaur** - Sad office worker as literal dinosaur wearing tie
3. **Bankrupt** - Empty office with "FOR LEASE" sign, dark screens
4. **Team Collapse** - Office worker alone at desk with tumbleweeds
5. **Survivor** - Office worker at desk giving thumbs up but exhausted
6. **Penguin Guardian** - Office worker surrounded by happy penguins wearing crown

### EVENT ILLUSTRATIONS (Generate ~8-10 as canvas/SVG):
7. **Archery Accident** - Office worker with arrow in shoulder
8. **AI Facial Recognition Fail** - Person confused at camera scanner
9. **Empty Desks** - Three empty office chairs with OUT signs
10. **AI Hallucination** - Computer screen showing glitchy errors
11. **Phishing Training** - Person sleeping at computer during training
12. **Resignation Email** - Email on screen, shocked face
13. **LinkedIn Crafting** - Person typing intensely with sparkles
14. **Budget Crisis** - Dollar signs with red X marks

Use a 16-color EGA-style palette, dithering, simple shapes, and retro pixelated look.

---

## CORE GAME MECHANICS

### The Stats (Track 6 values):
1. **📦 Onboarding Progress**: 0-100% (goal: reach 100%)
2. **🤖 AI Score**: 0-10 (hit 10 = LOSE "Automated Out")
3. **🦕 Dinosaur Score**: 0-10 (hit 10 = LOSE "Dinosaur")
4. **💰 Budget**: Start $200k (hit $0 = LOSE "Bankrupt")
5. **😰 Team Morale**: 0-10 (hit 0 = LOSE "Team Collapse")
6. **🐧 Penguins**: Start 5 (secret ending if all 5 survive)

### Game Structure: 6 Sprints
Each sprint has 3 phases:

#### PHASE 1: Story Point Allocation
Player allocates 20 story points across 4 categories using sliders:

```javascript
allocation = {
  aiTools: 0-20,      // Fast progress, +AI score, penguin risk
  traditional: 0-20,  // Slower progress, +Dino score
  techDebt: 0-20,     // Prevents disasters, minimal progress
  debugAI: 0-20       // Fixes AI bugs, no score changes
};

// Progress calculation:
progressGain = (aiTools * 2.5) + (traditional * 1.5) + (techDebt * 0.5);
aiScore += Math.floor(aiTools / 4);
dinoScore += Math.floor(traditional / 4);

// Penguin death check:
if (aiTools > 0 && Math.random() < 0.1) {
  penguins--; // 10% chance per sprint if using AI
}
```

#### PHASE 2: Sprint Decision Events (2 per sprint)
Each sprint has 2 binary decisions. Reference the full sprint details from the game design doc.

**Sprint 1: "The Kickoff"**
- Decision 1: Hire designer ($30k, +Dino) vs Use AI ($0, +AI, 20% unusable)
- Decision 2: Use React (+Dino, slower) vs Use VaporJS AI framework (+AI, 30% break)

**Sprint 2: "First Demo"**
- Decision 1: Manual polish (+Dino, -5 points) vs AI placeholder (+AI, 25% offensive)
- Decision 2: Promise AI feature (+AI, morale -2) vs Say not feasible (honest)

**Sprint 3: "The Crisis Sprint"**
- Decision 1: Hire contractors ($50k) vs Use Copilot (+AI, 40% broken)
- Decision 2: Accept scope creep (+AI, morale -1) vs Push back (boss annoyed)
- GUARANTEED EVENT: Security badge AI facial recognition fails (lose 3 points)

**Sprint 4: "The Pivot"**
- Decision 1: Rebuild AI-first (+AI, lose 20% progress) vs Add AI badges (+AI)
- Decision 2: Panic mode (+AI, morale -2) vs Stay the course
- RANDOM EVENT (50%): New AI tool (adopt = +AI, 30% data leak OR ignore = +Dino)

**Sprint 5: "The Breakdown"**
- Decision 1: LinkedIn post (waste 6 points, +AI) vs Focus on work
- Decision 2: Archery injury, send home (morale +1, -4 points) vs "walk it off" (morale -3)
- GUARANTEED EVENT: Dev's AI agent quits for them (lose 1 dev, -8 points next sprint)

**Sprint 6: "The Final Push"**
- Decision 1: AI auto-complete (+AI, 50% bugs, instant 100%) vs Manual grind (+Dino, reliable)
- Decision 2: Phishing training (lose 5 points) vs Skip (25% credential loss)

#### PHASE 3: Random Events (10% chance each sprint)
Pool of 8 random events:
1. AI Hallucination (emoji passwords, lose 1 sprint debugging)
2. Penguin Guilt Email (cosmetic, penguin -1, emotional damage)
3. Zoom Fatigue (6hr meetings, -4 points, morale -1)
4. Prompt Engineer Hire (morale -2, +AI, you feel obsolete)
5. Regulation (lose 10 points OR pay $40k)
6. AI Writes Standup (says you did nothing, morale -1)
7. Server Outage (-5 points)
8. Viral Tweet (+5 points, morale +1)

---

## WIN/LOSE CONDITIONS

Check after each sprint:

### LOSE CONDITIONS (Game Over):
1. **AI Score >= 10**: "Automated Out" ending
2. **Dino Score >= 10**: "Dinosaur" ending
3. **Money <= 0**: "Bankrupt" ending
4. **Morale <= 0**: "Team Collapse" ending

### WIN CONDITION:
- **Onboarding >= 100% AND survived**: "The Survivor" ending

### SECRET ENDING:
- **Win + All 5 Penguins Alive**: "Penguin Guardian" ending

---

## VISUAL STYLE REQUIREMENTS

### Oregon Trail 1990 Aesthetic:
- CRT green text on black background (#00FF00 on #000000)
- VT323 or similar monospace pixel font
- Scanline effect overlay
- 16-color EGA palette for generated graphics
- Dithering for gradients
- Simple pixel art shapes

### Layout:
```
┌─────────────────────────────────────────────┐
│  Title: THE PM PIVOT                        │
│  [PM Character Sprite - changes per sprint] │
├─────────────────────────────────────────────┤
│  Stats Bar:                                 │
│  Sprint X/6 | Progress XX% | Budget $XXXk  │
│  AI: X/10 | Dino: X/10 | Morale: X/10      │
│  Penguins: 🐧🐧🐧💀💀                         │
├─────────────────────────────────────────────┤
│  [Current Situation Text]                   │
│                                             │
│  Allocate 20 Story Points:                  │
│  🤖 AI Tools     [========] XX              │
│  👨‍💻 Traditional [====    ] XX              │
│  🔧 Tech Debt   [==      ] XX              │
│  🐛 Debug AI    [        ] XX              │
│                                             │
│  Remaining: XX points                       │
│  [SUBMIT SPRINT BUTTON]                     │
├─────────────────────────────────────────────┤
│  Event Log (scrollable):                    │
│  > Sprint 3: You allocated 8/8/4/0          │
│  > AI Score +2 (now 6/10) ⚠️                │
│  > 🐧 PENGUIN DIED                          │
│  > ...                                      │
└─────────────────────────────────────────────┘
```

### Modal for Decisions:
```
┌─────────────────────────────────────────────┐
│  [Event Illustration if available]          │
│                                             │
│  DECISION: The Designer                     │
│                                             │
│  You need mockups. What do you do?          │
│                                             │
│  ┌──────────────┐  ┌──────────────┐        │
│  │ OPTION A     │  │ OPTION B     │        │
│  │              │  │              │        │
│  │ Hire Real    │  │ Use AI       │        │
│  │ Designer     │  │ (Midjourney) │        │
│  │              │  │              │        │
│  │ -$30k        │  │ $0           │        │
│  │ +Dino        │  │ +AI, risky   │        │
│  │              │  │              │        │
│  │ [SELECT A]   │  │ [SELECT B]   │        │
│  └──────────────┘  └──────────────┘        │
└─────────────────────────────────────────────┘
```

---

## TECHNICAL REQUIREMENTS

### File Structure:
- Single HTML file (`index.html`)
- Embedded CSS (CRT green terminal theme)
- Vanilla JavaScript (no frameworks)
- Canvas or inline SVG for generated graphics
- Reference external images from `/images/` folder

### State Management:
```javascript
const gameState = {
  sprint: 1,
  onboardingProgress: 0,
  aiScore: 0,
  dinoScore: 0,
  budget: 200000,
  morale: 7,
  penguins: 5,
  techDebt: 0,
  developerCount: 5,
  eventLog: [],
  sprintAllocation: { aiTools: 0, traditional: 0, techDebt: 0, debugAI: 0 },
  choicesMade: []
};
```

### Key Functions Needed:
1. `allocatePoints(category, amount)` - Handle slider changes
2. `submitSprint()` - Process allocation, show decisions
3. `makeDecision(optionA/B)` - Handle binary choices
4. `rollRandomEvent()` - 10% chance trigger
5. `checkWinLose()` - Evaluate end conditions
6. `updateDisplay()` - Refresh all UI
7. `generateEndingScreen(type)` - Canvas/SVG ending graphics
8. `generateEventIllustration(type)` - Canvas/SVG event graphics
9. `showPenguinDeath()` - Animation when penguin dies

### Penguin Display:
Show 5 penguin slots at top right:
- Alive: Show `penguin-alive.png`
- Dead: Show `penguin-dead.png`
- Animate death: Brief shake/fade when dying

---

## GAME FLOW PSEUDOCODE

```javascript
function startGame() {
  showTitleScreen();
  // "THE PM PIVOT - Press START"
}

function startSprint(n) {
  updatePMSprite(n); // Load pm-sprint{n}.png
  displaySprintSituation(n);
  showStoryPointSliders();
  resetAllocation();
}

function submitSprint() {
  calculateProgress();
  updateScores();
  checkPenguinDeath();
  applyAutomaticDecay(); // budget -$60k, morale -1
  logResults();
  showDecisionEvent1();
}

function showDecisionEvent(eventData) {
  displayModal(eventData);
  // Show 2 options with effects
  waitForUserChoice();
}

function processDecision(choice) {
  applyEffects(choice.effects);
  logDecision(choice);
  rollRandomEvent(); // 10% chance
  checkWinLose();
  if (!gameOver) nextPhase();
}

function checkWinLose() {
  if (aiScore >= 10) endGame("automated");
  if (dinoScore >= 10) endGame("dinosaur");
  if (money <= 0) endGame("bankrupt");
  if (morale <= 0) endGame("teamCollapse");
  if (onboardingProgress >= 100) {
    if (penguins === 5) endGame("penguinGuardian");
    else endGame("survivor");
  }
}

function endGame(type) {
  showEndingScreen(type); // Generate canvas/SVG art
  displayFinalStats();
  showRestartButton();
}
```

---

## SPRINT DATA STRUCTURE

```javascript
const sprints = [
  {
    id: 1,
    title: "The Kickoff",
    situation: "You just raised $500k. The board wants an AI product in 3 months. Your team is ready. What's the strategy?",
    pmSprite: "pm-sprint1.png",
    decisions: [
      {
        title: "The Designer",
        prompt: "You need a designer for the onboarding flow mockups.",
        optionA: {
          text: "Hire Real Designer",
          effects: { budget: -30000, dinoScore: +1 },
          description: "Quality designs, traditional approach"
        },
        optionB: {
          text: "Use Midjourney + Figma AI",
          effects: { aiScore: +2 },
          risk: { chance: 0.2, effect: "Designs are unusable, lose 5 points" },
          description: "Free but risky"
        }
      },
      {
        title: "The Tech Stack",
        prompt: "What framework should we use?",
        optionA: {
          text: "React (tried and true)",
          effects: { dinoScore: +1, progressMultiplier: 0.9 },
          description: "Slower but reliable"
        },
        optionB: {
          text: "VaporJS (AI-powered framework)",
          effects: { aiScore: +1 },
          risk: { chance: 0.3, effect: "Framework breaks, lose 1 sprint" },
          description: "Cutting edge, risky"
        }
      }
    ]
  },
  // ... sprints 2-6 following same structure
];
```

---

## ADDITIONAL NOTES

### Humor & Tone:
- Keep event log messages sarcastic and dry
- Use realistic startup jargon ironically
- Make the impossible choices feel authentic
- The penguin deaths should be both funny and guilt-inducing

### Balance:
- Winning should require 40-60% AI usage (not 0%, not 100%)
- Should be possible to win multiple ways
- Randomness should add spice but not determine outcome
- Tech debt should matter (accumulate if ignored → disasters)

### Polish:
- Smooth transitions between sprints
- Sound effects optional but nice (8-bit beeps)
- Penguin death should have brief animation
- Event log should auto-scroll to newest
- Warning indicators when scores approach danger (8+)

---

## DELIVERABLE

Create a single `index.html` file that:
1. Uses the provided images from `/images/` folder
2. Generates remaining graphics via Canvas/SVG in Oregon Trail style
3. Implements all 6 sprints with decisions as specified
4. Tracks all 6 stats with proper win/lose logic
5. Includes all random events with correct probabilities
6. Has CRT green terminal aesthetic
7. Works as a complete playable game in ~10 minutes
8. Is fully self-contained (can be opened directly in browser)

Build this game following the complete design doc I provided earlier. Make it satirical, engaging, and true to the Oregon Trail 1990 aesthetic.
