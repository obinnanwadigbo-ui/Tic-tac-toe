# Contributing to Tic Tac Toe AI

Thank you for your interest in contributing! 🎉

We welcome all types of contributions:
- 🐛 Bug reports
- ✨ Feature suggestions
- 📚 Documentation improvements
- 🔧 Code enhancements
- 🎨 Design improvements

---

## 📋 Code of Conduct

Be respectful and constructive in all interactions. We're here to learn and grow together!

---

## 🚀 How to Contribute

### 1. Fork the Repository
```bash
# Click "Fork" on the GitHub page
```

### 2. Clone Your Fork
```bash
git clone https://github.com/YOUR-USERNAME/Tic-tac-toe.git
cd Tic-tac-toe
```

### 3. Create a Feature Branch
```bash
git checkout -b feature/your-feature-name
# or for bug fixes:
git checkout -b fix/your-bug-fix
```

### 4. Make Your Changes
- Write clean, readable code
- Add comments for complex logic
- Update documentation if needed
- Test thoroughly in your browser

### 5. Commit Your Changes
Use clear, descriptive commit messages:
```bash
# Features
git commit -m "feat: add player vs player mode"

# Fixes
git commit -m "fix: resolve AI delay issue on mobile"

# Documentation
git commit -m "docs: update README with examples"

# Style
git commit -m "style: improve responsive design for tablets"
```

### 6. Push to Your Fork
```bash
git push origin feature/your-feature-name
```

### 7. Create a Pull Request
- Go to the original repository
- Click "New Pull Request"
- Select your branch
- Add a descriptive title and description
- Submit!

---

## 💡 Feature Ideas

Here are some features we'd love to see:

- [ ] **Player vs Player Mode** - Two players on same device
- [ ] **Larger Board Sizes** - 4x4, 5x5 game variants
- [ ] **Sound Effects** - Audio feedback for moves and wins
- [ ] **Theme Toggle** - Dark/Light mode switcher
- [ ] **Game Replay** - Analyze previous games
- [ ] **Move History** - See all moves in a game
- [ ] **Animations** - Enhanced visual effects
- [ ] **Accessibility** - Keyboard navigation, screen reader support
- [ ] **Leaderboard** - Online statistics tracking
- [ ] **Mobile App** - PWA or native apps

---

## 🐛 Reporting Bugs

When reporting bugs, include:

1. **Description** - Clear explanation of the issue
2. **Steps to Reproduce** - How to trigger the bug
3. **Expected Behavior** - What should happen
4. **Actual Behavior** - What actually happens
5. **Environment** - Browser, OS, device type
6. **Screenshots** - Visual evidence (if applicable)

**Example:**
```
Title: AI moves are delayed on mobile devices

Description:
When playing on mobile, there's a noticeable delay between 
my move and the AI's response, even on hard difficulty.

Steps to Reproduce:
1. Open game on iPhone 12
2. Make a move
3. Wait for AI response

Expected: AI responds within 1 second
Actual: AI takes 3-5 seconds to respond

Environment: iPhone 12, Safari 15
```

---

## 📝 Code Style Guidelines

### JavaScript
```javascript
// Use meaningful variable names
const HUMAN = "X"; // Good
const h = "X"; // Avoid

// Use JSDoc for functions
/**
 * Checks if a player has won
 * @param {Array} boardState - Current board state
 * @param {string} player - Player to check
 * @returns {boolean} - True if player won
 */
function checkWinner(boardState, player) {
  // ...
}

// Use const by default, let if needed, avoid var
const unchanging = "value"; // Good
let changing = "value"; // OK for reassignment
var old = "avoid"; // Avoid

// Use arrow functions for callbacks
array.map(item => item * 2); // Good
array.map(function(item) { return item * 2; }); // Avoid
```

### CSS
```css
/* Use descriptive class names */
.cell-hover /* Good */
.ch /* Avoid */

/* Use semantic HTML-based classes */
.restart-btn /* Better than .btn-blue */
.difficulty-toggle /* Better than .toggle */

/* Group related properties */
.element {
  /* Display & Layout */
  display: flex;
  gap: 10px;

  /* Sizing */
  width: 100%;
  height: 100%;

  /* Styling */
  background: #fff;
  border-radius: 10px;
}
```

### HTML
```html
<!-- Use semantic elements -->
<div class="status" id="status">Your Turn</div>

<!-- Use descriptive IDs and classes -->
<button id="restart-btn" class="btn btn-restart">Restart</button>

<!-- Include comments for complex sections -->
<!-- Game board: 3x3 grid of clickable cells -->
<div class="board" id="board"></div>
```

---

## ✅ Testing Checklist

Before submitting a PR, test:

- [ ] Game works in Chrome
- [ ] Game works in Firefox
- [ ] Game works in Safari
- [ ] Game works on mobile (iOS, Android)
- [ ] Game works on tablet
- [ ] All buttons are clickable
- [ ] Statistics are saved correctly
- [ ] AI makes valid moves
- [ ] Game resets properly
- [ ] Win detection works
- [ ] Draw detection works

---

## 📚 Documentation

When adding features, update:

1. **README.md** - Add to features list or add new section
2. **Code Comments** - Explain complex logic
3. **JSDoc** - Document functions with types

Example:
```javascript
/**
 * Toggles difficulty between Impossible and Hard
 * Updates button text to reflect current mode
 * @returns {void}
 */
function toggleDifficulty() {
  impossibleMode = !impossibleMode;
  // ...
}
```

---

## 🔄 PR Review Process

1. **Automated Checks** - CI/CD tests run automatically
2. **Code Review** - Maintainers review code quality
3. **Feedback** - Suggestions for improvements
4. **Revisions** - Make requested changes
5. **Merge** - PR is merged when approved!

---

## 📞 Questions?

Feel free to:
- Open a discussion on GitHub
- Email: obinna.nwadigbo@gmail.com
- Check existing issues for answers

---

## 🎓 Resources

- [GitHub Flow Guide](https://guides.github.com/introduction/flow/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Semantic Versioning](https://semver.org/)
- [Markdown Guide](https://www.markdownguide.org/)

---

## 🙏 Thank You!

Your contributions make this project better for everyone. We appreciate your time and effort!

**Happy Contributing! 🚀**
