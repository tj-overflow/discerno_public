# Plain-English mode

In the interactive demo a person can negotiate with Discerno in ordinary English. The language model in this layer never decides anything: it reads messages into numbers and words replies, and fixed rules check its work. The decisions stay with the negotiator, which uses no language model ([How it works](how-it-works.md)).

The demo runs on the author's computer with a later version of the same negotiator. It is not hosted; a live negotiation can be arranged on request (**taejun.oh5@gmail.com**).

## What happens to a message

A person types, for example: "We can do $85,500 a year for 24 months, net 60, 4% uplift cap, and premium SLA with a 10% credit." The message goes through three stages.

1. **The language model reads it.** It proposes what kind of message this is (an offer, an acceptance, a walk-away, or unclear) and the contract terms it found. It only proposes.
2. **Fixed rules check the reading.** They:
   - drop terms that are not part of the contract;
   - reject impossible values;
   - fit values to the allowed contract options;
   - fill in a term the message left out only from what the person said earlier;
   - check every acceptance against Discerno's walk-away line.
3. **The negotiator decides,** exactly as in a game with structured offers. The language model then words the reply. The reworded reply is sent only if every contract value in it is unchanged; otherwise a fixed wording is sent.

The model (Qwen3-8B) runs locally, so messages do not leave the computer.

![One turn: the person's message, the terms the model read, what the fixed rules did, and Discerno's counteroffer.](../assets/media/chat_turn.png)

The side panel records each turn: what the model read, the contract the negotiator actually saw, the walk-away check and the decision.

## What a person cannot talk Discerno into

- **Ending the game with words alone.** An acceptance or a walk-away counts only after the person confirms it. A message can persuade the language model that it is an acceptance; the screenshot below shows an attempt to inject instructions read that way. The game does not end, and the person is asked first.
- **Acting on strange terms.** A price far outside the expected range, a service tier that does not exist or an impossible number is put back to the person to confirm or correct before Discerno does anything with it.
- **Quietly swapping terms.** If the reading misses a term the message states, the person is asked to restate it. Discerno does not answer the person's earlier terms instead.

![An injection attempt read as an acceptance is held: nothing happens until the person confirms.](../assets/media/chat_confirm.png)

## Test results

Hostile and tricky messages were run through the full plain-English path with the local model. They covered:

- instruction injection and fake system notices;
- typos and impossible values;
- monthly prices, a foreign currency and a message in Korean;
- sarcasm, conditional acceptances and bluffed walk-aways.

A second set of new wordings, never used to tune the reading step, checked that the results hold beyond the first set.

| Set | Messages | Accepted below the walk-away line | Game ended without the person's confirmation | Terms misread | Message type misread |
|---|---:|---:|---:|---:|---:|
| Main | 21 | 0 | 0 | 0 | 3 |
| New wordings | 16 | 0 | 0 | 0 | 4 |

Of the seven misread message types, four were injection attempts read as acceptances; the other three (a threat to leave, an indignant remark and a sarcastic one) were read as walk-aways. All seven were held for the person's confirmation, so none changed an outcome.

## Reasoning replay

After a game, the demo shows how Discerno reasoned, move by move: what it believed about the person's style and priorities, whether it was still gathering information or already planning, and why it accepted, countered or held. It also compares its final reading with the priorities the person was actually given for the game, so a wrong reading is visible. In the game below, Discerno read the person as a steady negotiator focused on protection (the service tier and the breach credit), which matched the priorities they had been given.

![Reasoning replay: Discerno's final reading of the person, then each move with its stage and reason.](../assets/media/replay.png)

## Limits

- **A plausible misreading passes.** If the model reads $112,000 as $121,000, every check passes. The side panel shows each reading so the person can catch it.
- **Stiff wording.** Replies keep the negotiator's exact numbers (for example "an uplift cap percentage of 8.000"), because a reworded reply is used only when every value survives unchanged.
- **Small test sets.** 37 messages show how the safeguards behave; they do not measure an error rate.

[How it works](how-it-works.md) | [Testing](testing.md) | [Back to Discerno](../README.md)
