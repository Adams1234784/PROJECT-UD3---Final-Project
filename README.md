# Battle Arena - Turn-Based Combat Game

# Project Description

Battle Arena is an interactive turn‑based combat game built with JavaFX where players face progressively stronger monsters using normal attacks, special attacks, and healing abilities, each with unique strategic implications. Inspired by classic RPGs such as Final Fantasy, Pokemon, and Dragon Quest, the project demonstrates core object‑oriented programming principles including inheritance, polymorphism, encapsulation, and custom exception handling through a BattleException system that manages invalid game states. The game provides real‑time visual feedback with health bars and a comprehensive battle log, while the UML diagram and GUI wireframe illustrate the planning and structure behind the implementation. Some features were streamlined to meet the deadline, focusing on the essential mechanics rather than optional extras, ensuring a playable and functional experience. Users interact through a simple JavaFX interface, choosing actions each turn and watching the results unfold in the log, highlighting how strategic decision‑making and resource management drive gameplay.

## Project Inspiration

This project was inspired by classic turn-based role-playing games (RPGs) such as:
- **Final Fantasy series** - Strategic turn-based combat mechanics
- **Pokemon games** - Progressive difficulty and monster battles
- **Dragon Quest** - Simple yet engaging battle systems

The goal was to create a modern JavaFX implementation that captures the essence of these classic games while demonstrating core OOP concepts learned in CS112.

## Animated Demo

![Battle Arena Gameplay](battle-arena-demo.gif)

*Note: Add your animated GIF/PNG screenshot here using Giphy Capture (Mac) or ScreenToGif (Windows)*

## UML Diagram

The following UML diagram represents the final class structure of the Battle Arena game:
┌───────────────────────────────┐
│          Exception            │
│       (Java Standard)         │
└───────────────┬───────────────┘
                │ extends
┌───────────────▼───────────────┐
│       BattleException          │
│ + BattleException(String msg)  │
└───────────────────────────────┘

┌───────────────────────────────┐
│          Character             │
│      (Abstract Class)          │
├───────────────────────────────┤
│ - name : String                │
│ - health : int                 │
│ - maxHealth : int              │
│ - attack : int                 │
│ - defense : int                │
├───────────────────────────────┤
│ + Character(...)               │
│ + attack(Character) : int      │
│ + takeDamage(int) : int        │
│ + heal(int) : void             │
│ + isDefeated() : boolean       │
│ + getHealthPercentage() : double│
└───────────────┬───────────────┘
                │
   ┌────────────▼─────────────┐       ┌────────────▼─────────────┐
   │          Player           │       │         Monster          │
   ├───────────────────────────┤       ├──────────────────────────┤
   │ + specialAttack(Character)│       │ + attack(Character)      │
   │ + useHeal()               │       │ + Monster(...)           │
   └───────────────────────────┘       └──────────────────────────┘

┌───────────────────────────────┐
│        BattleSystem            │
├───────────────────────────────┤
│ - player : Player              │
│ - monsters : List<Monster>     │
│ - currentMonster : Monster     │
│ - round : int                  │
│ - battleLog : StringBuilder    │
├───────────────────────────────┤
│ + playerAttack() : String      │
│ + playerSpecialAttack() : String│
│ + playerHeal() : String        │
│ + monsterTurn() : String       │
│ + isBattleOver() : boolean     │
│ + playerWon() : boolean        │
│ + getBattleLog() : String      │
└───────────────────────────────┘

┌───────────────────────────────┐
│     BattleController (JavaFX)  │
├───────────────────────────────┤
│ - UI controls (labels, bars,  │
│   buttons, text area)          │
│ - battleSystem : BattleSystem  │
├───────────────────────────────┤
│ + initialize()                 │
│ + onStart()                    │
│ + onAttack()                   │
│ + onSpecial()                  │
│ + onHeal()                     │
│ - updateUI()                   │
│ - endBattle()                  │
└───────────────────────────────┘

### OOP Concepts Implemented

1. **Inheritance**: `Player` and `Monster` extend the abstract `Character` class
2. **Polymorphism**: The `attack()` method is overridden in both `Player` and `Monster` classes
3. **Encapsulation**: All class fields are properly encapsulated with private/protected access modifiers
4. **Abstraction**: `Character` is an abstract class that defines the structure for all characters
5. **Exception Handling**: Custom `BattleException` class extends `Exception` for game-specific error handling
6. **Composition**: `BattleSystem` contains `Player` and `List<Monster>` objects

### Concepts Not Used

- **Interfaces**: While interfaces could have been used, abstract classes were chosen for this implementation to provide both method signatures and shared implementation
- **Generics**: The project uses standard collections without custom generic types, though `List<Monster>` does utilize Java's built-in generics

## GUI Wireframe Diagram

The following wireframe represents the final GUI layout of the Battle Arena game:

### Start Screen
```
┌─────────────────────────────────────────────────────────────┐
│                    ⚔️ BATTLE ARENA ⚔️                       │
│                                                             │
│              Welcome to Battle Arena!                       │
│        Enter your name to begin your adventure!            │
│                                                             │
│                    Player Name: [___________]               │
│                                                             │
│                      [ Start Battle ]                       │
│                                                             │
│                    Game Instructions:                       │
│              • Attack: Deal normal damage                   │
│              • Special Attack: Deal increased damage        │
│              • Heal: Restore 30 HP                          │
│              • Defeat all monsters to win!                  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Battle Screen
```
┌─────────────────────────────────────────────────────────────┐
│                    ⚔️ BATTLE ARENA ⚔️                       │
│              Battle in Progress                             │
│                        Round: 1                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  Player Name                                        │   │
│  │  100 / 100 HP                                       │   │
│  │  [████████████████████████████████] 100%           │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│                        ⚔️ VS ⚔️                            │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │  Goblin                                              │   │
│  │  80 / 80 HP                                          │   │
│  │  [████████████████████████████████] 100%            │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│        [ ⚔️ Attack ]  [ 🔥 Special ]  [ 💚 Heal ]         │
│                                                             │
│  Battle Log:                                                │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ === BATTLE BEGINS ===                               │   │
│  │ Round 1: Goblin appears!                            │   │
│  │ Choose your action!                                 │   │
│  │                                                     │   │
│  │ Player attacks Goblin for 28 damage!               │   │
│  │ Goblin attacks Player for 22 damage!               │   │
│  │                                                     │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Victory/Defeat Screen
```
┌─────────────────────────────────────────────────────────────┐
│                    ⚔️ BATTLE ARENA ⚔️                       │
│                    VICTORY! / DEFEAT!                       │
│                        Round: 4                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  [Player and Monster stats displayed]                       │
│                                                             │
│        [ ⚔️ Attack ]  [ 🔥 Special ]  [ 💚 Heal ]         │
│              (All buttons disabled)                         │
│                                                             │
│  Battle Log:                                                │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ ...                                                  │   │
│  │                                                     │   │
│  │ === VICTORY! ===                                    │   │
│  │ You have defeated all monsters!                    │   │
│  │                                                     │   │
│  │ Click 'Start New Battle' to play again.            │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## How to Run

1. Ensure you have Java 23 and Maven installed
2. Navigate to the project directory
3. Run the application using:
   ```bash
   mvn clean javafx:run
   ```
   Or use the Maven wrapper:
   ```bash
   ./mvnw clean javafx:run
   ```

## Project Structure

```
ud3-Adams1234784-main/
├── pom.xml                          # Maven configuration
├── README.md                        # This file
├── src/
│   └── main/
│       ├── java/
│       │   ├── module-info.java     # Java module configuration
│       │   └── cs112/
│       │       └── ud3/
│       │           ├── HelloApplication.java    # Main application
│       │           ├── BattleController.java    # GUI controller
│       │           ├── BattleSystem.java         # Game logic
│       │           ├── Character.java            # Abstract base class
│       │           ├── Player.java               # Player character
│       │           ├── Monster.java              # Monster enemy
│       │           └── BattleException.java      # Custom exception
│       └── resources/
│           └── cs112/
│               └── ud3/
│                   └── battle-view.fxml          # GUI layout
```

## Features

- **Turn-based Combat**: Strategic battle system with player and monster turns
- **Multiple Actions**: Attack, Special Attack, and Heal options
- **Progressive Difficulty**: Monsters become stronger as you progress
- **Visual Feedback**: Health bars and real-time battle log
- **Exception Handling**: Custom exceptions for invalid game states
- **Modern GUI**: Clean JavaFX interface with intuitive controls

## Technologies Used

- **Java 23**: Core programming language
- **JavaFX 22**: GUI framework
- **Maven**: Build and dependency management
- **FXML**: Declarative UI layout

## Author

CS112 Adam Szloboda - UD3 Final Project

