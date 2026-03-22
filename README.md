# Unity Custom Board Game & Engine Framework

A 3D chess-like board game built in Unity, featuring a custom, object-oriented engine framework. This project not only implements the core logic for a turn-based board game (complete with piece validation, timers, and move history) but also abstracts Unity's base components into a streamlined, easy-to-use custom engine API.

##  Project Overview

The repository is divided into two main components:
1.  **The Game:** A fully functional 3D board game that implements chess piece movement logic, turn-based switching, a dynamic camera that rotates based on the active player, and match timers.
2.  **The Engine:** A custom wrapper built on top of Unity's `GameObject`, `Transform`, and `Renderer` systems. It includes abstractions for 3D primitives, a custom UI system (Text, Buttons, Textures), and automated input/collision detectors.

##  Features

* **Custom Object Wrappers:** `DvBaseObject` and `UI_Object` classes that simplify instantiation, positioning, rotation, and scaling of 3D and 2D elements without needing to constantly interact with Unity's verbose component system.
* **Chess-Like Game Logic:** * Includes movement validation for Pawns, Rooks, Knights, Bishops, Queens, and Kings.
    * Turn alignment system (White vs. Black) with an integrated match timer.
    * Move history tracking allowing players to undo moves.
* **Dynamic Camera Controller:** The camera automatically smoothly transitions to face the board from the perspective of the current player's turn.
* **Custom Event System:** A lightweight `MouseDetector` and `CollisionDetector` system that utilizes delegates to handle events like `MOUSE_CLICK`, `MOUSE_OVER`, and `MOUSE_DOWN`.
* **From-Scratch UI:** A custom UI rendering system operating on a separate camera layer, featuring interactive buttons with normal/over/down states and text fields.

##  Architecture

* **Engine/**
    * `CameraController.cs`: Manages 3D camera positioning, following targets, and rotating around the board.
    * `Detectors/`: Contains scripts attached to GameObjects to broadcast collision and mouse events.
    * `DvObjects/`: The core wrapper classes (`BaseObject`, `DvBaseObject`, `Dv3dObject`, `DvPrimitiveObject`) that manage mesh rendering, physics, and basic transformations.
    * `UI/`: Custom user interface framework containing `UI_Camera`, `UI_Button`, `UI_TextField`, and `UI_Texture`.
* **Game/**
    * `Game.cs`: The master controller for the game loop, handling turns, timers, input capture, and the undo system.
    * `Board.cs`: Manages the 8x8 grid matrix, tile generation, and the tile selector logic.
    * `Piece.cs`: Inherits from `Entity` to represent game pieces, storing their alignment and specific type.
    * `Entity.cs`: The base class for all game-specific objects on the board.
* **Screens/**
    * `MainMenu.cs` & `Credits.cs`: Simple UI scene controllers to transition into the main gameplay loop.

##  Controls

The game is played entirely via the keyboard once in the main scene:

    Arrow Keys  : Move the tile selector across the 8x8 board.
    Spacebar    : Select a piece / Confirm movement to the highlighted tile.
    Z           : Undo the last move (reverts to the previous board state).
    Escape      : Quit the current match and return to the Main Menu.

##  Getting Started

1. Clone the repository to your local machine.
2. Open the project using Unity (ensure you have the appropriate `Standard` and `Unlit` shaders available as referenced in `ShaderPath.cs`).
3. The project requires specific folders in your `Resources` directory to load assets dynamically:
    * `Resources/UI/Textures/` (For button and HUD textures)
    * `Resources/UI/Fonts/` (For UI text fonts, e.g., Arial)
    * `Resources/Prefabs/` (For custom 3D models if not using primitives)
4. Open the `MainMenu` scene and press **Play** in the Unity Editor.

## 📝 Notes

This project was built to demonstrate how Unity's component-based architecture can be wrapped into a more traditional Object-Oriented Programming (OOP) hierarchy, hiding the boilerplate code involved with component fetching and physical constraints. Note that the codebase contains several internal comments and variable names in Spanish, but the API and architecture follow standard English naming conventions.
