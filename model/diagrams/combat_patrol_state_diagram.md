```mermaid
---
title: Combat Patrol State Diagram
---

stateDiagram-v2
%% start
1a: declare teams
1b: define primary mission
1c: choose secondary objective
[*] --> 1a
1a --> 1b
1b --> 1c

%% Deployment
2a: roll for choice of first placement
2b: placement
1c --> 2a
2a --> 2b

%% Post Deployment
3a: post placement ability
3b: roll for choice of first turn
2b --> 3a
3a --> 3b

%% Rounds
3b --> round
state round {
    %% Turns
    [*] --> turn : for each player
    turn: Turn
    state turn {
        [*] --> 4a
        4a --> 4b
        4b --> 4c
        4c --> 4b
        4b --> 4d
        4c --> 4d
        4d --> 4e
        4e --> 4f
        4f --> 4g
        4a: command phase
        4b: movement phase
        4c: overwatch (opponent)
        4d: shooting phase
        4e: charge phase
        4f: fight phase
        4g: fight back (opponent)
        4g --> [*]
    }
    turn --> [*]
}

state if_state <<choice>>
round --> if_state : increment round count
if_state --> round : <= 5

%% Endgame
5a: second player scores primary objective
if_state --> 5a : > 5
5a --> [*]
```
