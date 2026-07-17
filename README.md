# Maze Generator & A* Pathfinding Solver

A C# Windows Forms desktop application that procedurally generates solvable mazes, solves them with a custom A* search implementation, and lets a user race the algorithm by drawing their own path through the maze with the mouse.

This project was built as the Non-Exam Assessment (NEA) for A-Level Computer Science.

## What it does

The app is a small interactive tool rather than a script, run it and you get a live canvas you can generate, solve, play with, and save:


Generate a maze of any odd size, drawn instantly on screen.
Solve it with AI: a custom A* implementation finds the shortest route from entrance to exit and draws it as a line over the maze.
Solve it yourself: click your way through the maze cell by cell. Invalid moves (walls, non-adjacent cells) are rejected in real time, and backtracking removes your last step.
Compare: once you reach the exit, the app tells you your path length versus the A* path length and by how much you beat or lost to it.
Save and reload any generated maze as a plain text grid.
Browse history: step back and forward through every maze generated in the current session.


## Technical highlights

Maze generation (mazegen3): a randomised recursive-backtracking algorithm. It carves passages two cells at a time through a walled grid, picking a random unvisited neighbour at each step and backtracking when it hits a dead end, which guarantees a maze that is always solvable and has no disconnected areas.

Pathfinding (astarsearch): a from-scratch A* search over the maze. Rather than treating every cell as a search node, the algorithm walks along corridors and only creates a node at junctions or dead ends, which keeps the open/closed lists small even on large mazes. Node priority is driven by a Manhattan-distance heuristic to the exit.

Manual solution validation (createusersolution): every mouse click is checked against the maze's wall data and the player's current position, so the user can only move into an orthogonally adjacent, non-wall cell, and can pop their last move to undo it.

Custom file format: mazes are saved and loaded as a plain grid of digits (wall/path per cell) via StreamReader/StreamWriter, with no external serialisation library.

Rendering: the maze, the user's path, and the AI's path are all drawn by hand with GDI+ (System.Drawing) inside the form's paint event, and the canvas keeps a square aspect ratio and rescales automatically when the window is resized.

## Tech stack


Language: C#
Framework: .NET, Windows Forms
Graphics: GDI+ (System.Drawing), custom rendering, no external UI or graphics libraries
Core data structures: Stack<T>, List<T>, and hand-written Node/Cell/Maze classes


## Skills demonstrated


Implementing a classic search algorithm (A*) from scratch, including a custom heuristic and an optimisation to reduce the search space
Designing a separate, correct maze-generation algorithm and reasoning about why it guarantees solvability
Object-oriented design across multiple cooperating classes (Maze, Node, Cell) with encapsulated state
Event-driven desktop UI programming with Windows Forms
Manual 2D graphics rendering and coordinate/scaling maths
File I/O with a custom save format
Input validation and defensive coding around user interaction
