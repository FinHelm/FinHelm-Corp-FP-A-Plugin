---
description: Score a forecast's reliability against its own history
---

Run the forecast-reliability skill.

Determine the entity and the lines under review from the conversation. If they are not specified, ask which lines matter most before proceeding.

Check data adequacy first and report it before any score. If there is less than two full budget cycles of usable forecast-versus-actual history, stop and say so rather than producing a score from insufficient history.

Call the computation tool for all figures. Report the band alongside the composite, state that lower is better, and lead with the dimension driving the reading.

$ARGUMENTS
