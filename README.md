# Visual Studio C++ Debugging Lab: Elemental Combat

## 🎮 Scenario: The Broken Game
Welcome to the Elemental Combat Debugging Lab! In this practical example, we explore a simple C++ game similar to "Rock, Paper, Scissors" (using Fire, Grass, and Water). 

The game is currently riddled with errors. Your goal is to move from a non-compiling state to a fully functional game using Visual Studio's debugging tools.

## 🎯 Learning Objectives
By completing this lab, you will practice:
* Handling build errors and using code isolation strategies.
* Identifying runtime crashes caused by uninitialized pointers.
* Fixing insidious logic errors like assignment mistakes and magic numbers.
* Mastering advanced debugging tools in Visual Studio.

---

## 🚀 Phase 1: Handling Build Errors

When code fails to compile, your first step is to consult the **Error List**.

* **Identify the Line:** The console will attempt to identify the specific line causing the issue (e.g., line 56).
* **Isolation Strategy:** If the error is unclear, a useful technique is to **Block Comment** large sections of code. By commenting out complex logic and leaving only the basic structure, you can determine if the core program compiles. If it does, you can slowly uncomment sections to pinpoint the exact location of the failure.

---

## 🛠️ Phase 2: The Debugging Challenges

Once the game compiles, you will encounter several runtime and logic errors. Use this checklist to track them down and fix them.

### Challenge 1: The Null Pointer Crash (Runtime Error)
A common runtime error in C++ is the **Null Reference Exception**. This occurs when the code tries to access an object that hasn't been created or assigned memory yet.
* **The Symptom:** The code compiles but crashes immediately upon running.
* **The Task:** In `main()`, the `player` and `enemy` pointers are declared but never assigned to a `new Actor(30)`. Fix the allocation so the game can actually start.

### Challenge 2: The Missing Headers (Build Error)
* **The Symptom:** The compiler may complain that it doesn't recognize `srand`, `rand`, or `time`.
* **The Task:** Ensure you have included `<cstdlib>` and `<ctime>` at the top of your file. Relying on `<iostream>` to provide these is "brittle" code and will fail on many compilers.

### Challenge 3: The "Always Enemy" Glitch (Logic Error)
* **The Symptom:** During testing, you might notice the enemy wins every single round, even if you chose the winning element.
* **The Task:** Look closely at the `DidPlayerWin` function and the attack logic. Check for the **Assignment vs. Comparison** mistake. Ensure you are using `==` to check for equality, rather than `=` which accidentally overwrites your variables.

### Challenge 4: The Zero-Index Logic (Logic Error)
* **The Symptom:** The enemy occasionally chooses "0", which isn't a valid move (Fire=1, Grass=2, Water=3).
* **The Task:** Inspect the `enemyChoice` calculation. `rand() % 3` produces 0, 1, or 2. Use the debugger to watch this value and fix the math so the enemy only picks between 1 and 3.

### Challenge 5: Magic Numbers & Damage Balancing
* **The Symptom:** The player deals 10 damage manually, but the enemy uses an `Attack()` method. This is hard to balance and prone to typos.
* **The Task:** Replace the "Magic Numbers" (the raw 10s in the code) with a constant or a member variable like `attackPower`. This ensures both actors play by the same rules.

### Challenge 6: The Infinite Loop (Input Validation)
* **The Symptom:** If a user types a letter instead of a number, the game enters an infinite loop of text.
* **The Task:** Implement a check for `std::cin.fail()`. If the input is invalid, clear the error and ignore the bad input so the user can try again.

---

## 🔬 Phase 3: Advanced Debugging Tools

To find these logic errors, we utilize specific features within the Visual Studio IDE:

* **Breakpoints:** By clicking in the left margin, you can force the game to pause execution at a specific line. This allows you to inspect the state of the game at that exact moment.
* **Watch Window:** Instead of hovering over variables with your mouse, you can right-click a variable and select **Add to Watch**. This creates a dedicated window that tracks the value of that variable in real time as you step through the code.
* **Conditional Breakpoints:** Sometimes you only want to pause the game in a specific scenario. You can convert a standard breakpoint into a conditional one by adding a logic check (e.g., only break if `enemyChoice == 1`).
* **Call Stack:** This window shows the history of function calls that led to the current pause point. It is essential for tracing back how the program arrived at a specific state or error.