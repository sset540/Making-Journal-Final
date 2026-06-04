## Week 08

Week eight was the first formal critique session of the project phase, structured around progress report presentations and critical design propositions. The emphasis shifted from individual making to peer exchange — using the work developed over Weeks 06 and 07 as a basis for structured feedback and critical reading of each other's projects. This was the first CRIT week in the schedule, sitting between two development studios and intended to redirect making based on what the work reveals when shared with an audience.

### Progress Reports

The class began with fifteen minutes of preparation time to review the progress report slideshow and set up a way to record incoming feedback. I organised my five slides into a clear sequence: the project concept and Spotify API as data source, the audio feature-to-visual-property mappings, a screenshot of the current prototype showing two contrasting track environments, the search interaction sketch, and the three feedback questions.

Groups of five or six formed, with roles of Chair, Technical Commenter, and Conceptual Commenter assigned and rotated after each presenter. When presenting I walked the group through the project in five minutes before opening to discussion. The three questions I posed were: whether the search interaction or a passive currently-playing display would be more engaging for a public audience; whether the colour mapping between valence and emotional temperature felt accurate or needed adjustment; and whether the space environment was visually distinct enough from generic screensaver aesthetics to feel like a deliberate design work.

The feedback across all three roles was specific and useful. The Technical Commenter noted that the API polling approach I was using — fetching audio features once per track change — was correct for this use case but asked whether I had considered how the piece would behave if the Spotify session was paused or if no track was playing. They suggested building a fallback state — a default ambient environment that appears when no data is available. The Conceptual Commenter engaged most directly with the screensaver question, suggesting that what distinguishes the piece from a generic space visualisation is the legibility of the data mapping — if a viewer can sense that the environment is genuinely responding to something specific about the music rather than just being generatively pretty, the work has critical weight. They suggested adding a minimal data overlay showing the current track's valence and energy values as a way of making the algorithm visible. The Chair noted that the search interaction was the most compelling aspect of the presentation because it gave the viewer agency, and encouraged me to prioritise it over the passive display mode.

The feedback from watching other presentations was also informative. Seeing how different data sources and visual approaches communicated to the same group highlighted how important the moment of first contact is — the viewer needs to understand almost immediately what they are looking at and why it is changing.

### Critical Design Propositions

After the break, the class paired with a partner from a different group for the Critical Design Propositions activity. Following a five-minute briefing where I described my project and the feedback just received, my partner spent time in critical reading before developing a design proposition in response.

The proposition my partner developed addressed the screensaver problem directly. Their reading was that the space environment, while visually strong, risked feeling decorative unless the data source was made more present in the experience. The proposition they sketched was to add a second visual register alongside the space scene — a minimal circular data portrait in one corner of the canvas showing the current track's key audio features as abstract marks or segments. This would function like a compass: grounding the viewer in the data logic while the space environment provided the immersive experience. The two layers together would make both the emotional world and the data behind it simultaneously visible.

I spent twenty-five minutes developing a proposition in response to my partner's project, which was working with a different dataset and visual language but facing a similar question about how to communicate data logic without breaking visual immersion. The proposition I produced suggested using typographic scale rather than graphical elements to make data visible — a single large number that changes with the data, legible from a distance, which grounds the viewer without interrupting the aesthetic.

The data portrait idea from my partner's proposition for my own project was one I had not considered before but which felt immediately right. Making the algorithm visible while keeping the space environment intact resolves the tension between critical transparency and immersive experience.

### Independent Study

#### Reflective Summary

The most significant feedback from Week 08 was the Conceptual Commenter's point about legibility: the space environment needs to communicate that it is genuinely data-driven, not just generatively atmospheric. Without that legibility, the critical framing — that the viewer is experiencing Spotify's algorithmic interpretation of a song's emotional content as a world — does not land.

The data portrait idea from the critical design proposition gives me a way to address this. A small, elegant circular readout in the corner of the canvas showing the current valence and energy values would make the data layer present without dominating the visual experience. The viewer can choose to look at the data or let the space environment speak for itself.

The other decision I am making in response to this week is to prioritise the search interaction over the passive display mode. The Chair's feedback was clear: giving the viewer agency over which track they explore is more compelling for a public showcase context than a passive display that depends on the presenter having Spotify open. The search input should be minimal and integrated into the canvas rather than sitting outside it.

These two decisions — the data portrait and the search-first interaction — are the main directions I am taking into Week 09.

#### Project Development

The independent study period was spent implementing the data portrait and refining the search interaction. For the data portrait, I drew a small circle in the top-right corner of the canvas containing two arcs: one mapping valence as a proportion of the full circle, and one mapping energy. The arcs are drawn in the same colour palette as the current space environment so they feel integrated rather than appended. The current track name and artist appear in small text below the arcs. Testing this with several different tracks confirmed that the readout changes in a way that is immediately readable — you can see that a sad, quiet song has short arcs and a bright, energetic song fills them nearly completely.

For the search interaction, I added a text input at the bottom of the canvas using p5.js DOM elements and wired it to the Spotify Search API. Typing a track name returns up to five results displayed as a minimal dropdown list. Selecting a result fetches the audio features and triggers the transition to the new space environment. The transition between environments now uses a cross-fade via canvas opacity rather than lerping individual values, which produces a smoother and more cinematic shift between two space scenes.

The next priority is refining the visual quality of the nebula and testing the full piece at the display scale that will be used in the Week 12 showcase.
