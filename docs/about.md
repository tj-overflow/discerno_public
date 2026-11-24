# About Discerno

## Who built it

Discerno is a solo project by **Taejun Oh**. I hold a Ph.D. in economics from the University of Michigan, where I worked on game theory and mechanism design, and I have spent about ten years on strategy advisory and research work for senior management. I am completing a Master of Computer Science at the University of Illinois Urbana-Champaign (2027).

## Why

Discerno started as an exercise: take fairly standard negotiation theory and make it run in simulation. As it grew, the goal became a system that works end to end: one that can bargain over a contract with several terms, explain each move, and eventually negotiate with people.

## How it was built

I came up with the idea and designed the negotiation model, the system's structure and the tests. I used AI coding assistants (Claude) to write, test and debug the code, and to search the literature.

## One problem along the way

An early version of the planner kept turning down good offers. The cause was a hidden assumption: when it valued continuing to bargain, it worked out the best next move separately for each possible type of opponent and then averaged the values of those moves, as if it would know which type it faced before choosing. Discerno has no such knowledge when it chooses. The fix was to value each move against all the possible opponent types at once, as in [step 4 of How it works](how-it-works.md#4-plan-three-moves-ahead), and only then compare moves.

## Contact

Questions, or a request for a live negotiation with Discerno: **taejun.oh5@gmail.com**.

[Back to Discerno](../README.md)
