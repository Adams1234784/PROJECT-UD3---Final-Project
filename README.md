# Battle Arena - Turn-Based Combat Game

## Project Description

Battle Arena is an interactive turn-based combat game built with JavaFX where players engage in strategic battles against progressively challenging monsters. Players can choose from different combat actions including normal attacks, special attacks, and healing abilities, each with unique strategic implications. The game features a custom exception handling system (`BattleException`) to manage invalid game states and provides real-time visual feedback through health bars and a comprehensive battle log. This project was inspired by classic turn-based RPG games like Final Fantasy and Pokemon, where strategic decision-making and resource management are key to victory. The game demonstrates object-oriented programming principles including inheritance, polymorphism, encapsulation, and exception handling in a fun and engaging way.

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

```
┌─────────────────────────────────────────────────────────────┐
│                        Exception                            │
│                    (Java Standard)                          │
└───────────────────────────┬─────────────────────────────────┘
                            │
                            │ extends
                            │
                ┌───────────▼───────────┐
                │   BattleException     │
                ├───────────────────────┤
                │ + BattleException(    │
                │     String message)   │
                └───────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│                      Character                              │
│                    (Abstract Class)                         │
├─────────────────────────────────────────────────────────────┤
│ # String name                                               │
│ # int health                                                │
│ # int maxHealth                                             │
│ # int attack                                                │
│ # int defense                                               │
├─────────────────────────────────────────────────────────────┤
│ + Character(String, int, int, int)                         │
│ + abstract int attack(Character) throws BattleException    │
│ + int takeDamage(int)                                       │
│ + boolean isDefeated()                                      │
│ + void heal(int)                                            │
│ + String getName()                                          │
│ + int getHealth()                                           │
│ + int getMaxHealth()                                        │
│ + int getAttack()                                           │
│ + int getDefense()                                          │
│ + double getHealthPercentage()                             │
└───────────────┬───────────────────────┬─────────────────────┘
                │                       │
                │ extends               │ extends
                │                       │
    ┌───────────▼──────────┐  ┌────────▼──────────┐
    │       Player         │  │      Monster       │
    ├──────────────────────┤  ├───────────────────┤
    │                      │  │                   │
    ├──────────────────────┤  ├───────────────────┤
    │ + Player(String)     │  │ + Monster(String) │
    │ + Player(String,     │  │ + Monster(String, │
    │   int, int, int)     │  │   int, int, int)  │
    │ + int attack(        │  │ + int attack(     │
    │   Character)         │  │   Character)       │
    │ + int specialAttack( │  │                   │
    │   Character)         │  │                   │
    └──────────────────────┘  └───────────────────┘

┌─────────────────────────────────────────────────────────────┐
│                    BattleSystem                             │
├─────────────────────────────────────────────────────────────┤
│ - Player player                                             │
│ - List<Monster> monsters                                    │
│ - Monster currentMonster                                    │
│ - int currentMonsterIndex                                   │
│ - int round                                                 │
│ - String battleLog                                          │
├─────────────────────────────────────────────────────────────┤
│ + BattleSystem(Player, List<String>)                       │
│ + String playerAttack() throws BattleException             │
│ + String playerSpecialAttack() throws BattleException      │
│ + String monsterAttack() throws BattleException            │
│ + String playerHeal() throws BattleException               │
│ + boolean isBattleOver()                                    │
│ + boolean playerWon()                                       │
│ + Player getPlayer()                                        │
│ + Monster getCurrentMonster()                               │
│ + int getRound()                                            │
│ + String getBattleLog()                                     │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│                  BattleController                           │
│                  (JavaFX Controller)                        │
├─────────────────────────────────────────────────────────────┤
│ - TextField playerNameField                                 │
│ - Button startButton                                        │
│ - Label playerNameLabel                                     │
│ - Label playerHealthLabel                                   │
│ - ProgressBar playerHealthBar                              │
│ - Label monsterNameLabel                                    │
│ - Label monsterHealthLabel                                  │
│ - ProgressBar monsterHealthBar                             │
│ - Button attackButton                                       │
│ - Button specialAttackButton                                │
│ - Button healButton                                         │
│ - TextArea battleLogArea                                    │
│ - Label roundLabel                                          │
│ - Label statusLabel                                         │
│ - VBox gameArea                                             │
│ - VBox startArea                                            │
│ - BattleSystem battleSystem                                 │
│ - boolean gameStarted                                       │
├─────────────────────────────────────────────────────────────┤
│ + initialize()                                              │
│ + onStartButtonClick()                                      │
│ + onAttackButtonClick()                                     │
│ + onSpecialAttackButtonClick()                              │
│ + onHealButtonClick()                                       │
│ - updateDisplay()                                           │
│ - endBattle()                                               │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│                 HelloApplication                            │
│              (JavaFX Application)                           │
├─────────────────────────────────────────────────────────────┤
│ + start(Stage)                                              │
│ + main(String[])                                            │
└─────────────────────────────────────────────────────────────┘
```

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

CS112 Student - UD3 Final Project

