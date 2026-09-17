# Daily progress reporting

Mission Control records actual Minecraft day transitions. A separate local Codex
automation checks every five minutes for completed daily summaries and publishes
each once to this repository. An upload is acknowledged only after checking the
committed file against the prepared summary.

Reports describe recorded activity, milestones, failures and outstanding work.
Recording began partway through day 4. Missing earlier history is not reconstructed
or presented as measured activity.

The computer, Codex and the authenticated GitHub session must remain available for
publication. Minecraft must run for in-game days to advance. The polling interval
means publication can lag a day boundary; GitHub is a historical record, not live
Mission Control state.

Detailed coordinates, live telemetry, world saves, raw event archives, local machine
paths and robot inventories are not continuously uploaded. The observer and robot
colony operate locally without depending on GitHub or an external telemetry service.

Project documentation is published separately from daily reports. Updating these
documents does not modify the Minecraft world, dispatch jobs or acknowledge a day.
