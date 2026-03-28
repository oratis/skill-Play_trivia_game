# Trivia Game — Claude Code Skill

An interactive trivia quiz skill for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Play solo, challenge the AI, or compete with a friend — all inside your terminal.

## Features

- **10 built-in categories**: Science, History, Geography, Tech, Literature, Sports, Movies, Music, Food, Business (or add your own)
- **3 game modes**:
  - **Solo** — answer questions, get instant feedback and explanations
  - **User vs AI** — compete against Claude (it plays at ~70% accuracy to keep things fun)
  - **User vs User** — two players take turns on the same terminal
- **Flexible game length**: 5 / 10 / 15 / 20 questions per round
- **Automatic record keeping**: every game is saved to `trivia_record.md`
- **Flash card review**: missed questions become flash cards for spaced review
- **Bilingual**: auto-detects Chinese or English based on user input

## Installation

### 1. Copy the skill file

```bash
# Create the skill directory
mkdir -p ~/.claude/skills/trivia-game

# Copy the skill definition
cp SKILL.md ~/.claude/skills/trivia-game/SKILL.md
```

### 2. Register the skill

Add the following to your Claude Code `settings.json` (usually at `~/.claude/settings.json` or project-level `.claude/settings.json`):

```json
{
  "skills": {
    "trivia-game": {
      "path": "~/.claude/skills/trivia-game"
    }
  }
}
```

### 3. Start playing

Open Claude Code and type any of:

```
trivia
quiz
play trivia game
问答游戏
答题
```

## How It Works

### Game Flow

```
Start game
    |
    v
Select categories (multi-select)
    |
    v
Choose question count + game mode
    |
    v
Answer questions (A/B/C/D multiple choice)
    |  - Instant feedback after each question
    |  - Running score display
    v
View results summary
    |
    v
Auto-save to trivia_record.md
    |
    v
(Optional) Review flash cards later
```

### Game Modes

| Mode | Description |
|------|-------------|
| Solo (vs AI judge) | You answer, AI judges and explains. Great for learning. |
| User vs AI | You and AI both answer each question. AI plays at ~70% to stay competitive. |
| User vs User | Two players take turns. Perfect for friendly competitions. |

### Flash Cards

After each game, questions you got **wrong** are automatically saved as flash cards in `trivia_record.md`. You can review them anytime:

```
review flash cards
复习闪卡
```

The review system supports:
- Review all cards across all games
- Filter by category
- Focus on recent mistakes
- Track last-reviewed dates

## File Structure

```
~/.claude/skills/trivia-game/
├── SKILL.md            # Skill definition (the brain)
└── trivia_record.md    # Game history & flash cards (auto-generated)
```

## Record Format

Each game session is recorded with:
- Date, categories, mode, players, final score
- Full question-by-question breakdown table
- Auto-generated flash cards for missed questions

Example entry:

```markdown
## Game #1 — 2026-03-28 14:30

**Categories**: Science, History
**Mode**: Solo
**Players**: User
**Result**: 7/10 (70%)

### Questions & Answers
| # | Category | Difficulty | Question | Correct Answer | P1 Answer | P1 |
|---|----------|------------|----------|----------------|-----------|-----|
| 1 | Science  | Medium     | What is the chemical symbol for gold? | Au | Au | ✓ |
| 2 | History  | Hard       | In what year was the Magna Carta signed? | 1215 | 1066 | ✗ |

### Flash Cards
| Front (Question) | Back (Answer + Explanation) | Category | Last Reviewed |
|---|---|---|---|
| In what year was the Magna Carta signed? | 1215. King John signed it at Runnymede. | History | — |
```

## Customization

### Adding Categories

Edit the category table in `SKILL.md` to add new categories:

```markdown
| gaming | Gaming | 游戏 |
| anime | Anime & Manga | 动漫 |
```

Or simply type a custom category when prompted — the skill accepts free-form input via the "Other" option.

### Changing Difficulty Mix

The default difficulty distribution is:
- 30% Easy
- 50% Medium
- 20% Hard

Adjust in the "Question Generation Rules" section of `SKILL.md`.

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI
- Internet connection (for web-search-powered question generation)

## License

MIT
