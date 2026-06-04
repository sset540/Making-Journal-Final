## Week 09

Week nine was the second development studio of the project phase, structured around two parallel streams of work: conceptual development through drafting a project statement, and practical development through a making sprint and round robin rapid reactions. The class returned to a making-focused mode after last week's critique, with the project statement draft serving as a conceptual anchor for the hands-on work that followed.

### Project Statement: First Draft

The session opened with a case study engagement using Tega Brain and Sam Lavigne's *Xeno Computer 0.1: Labor*, which the class analysed in pairs using a Miro board. The work draws on labour data to construct a speculative computational system, and the discussion centred on how its statement articulates a provocation about data and power without becoming didactic. The data sources are embedded in the work's logic rather than displayed; the future scenario is implied by the system's design rather than stated outright. What the case study clarified for me is that a strong project statement does not explain the work — it extends it, giving a public audience a way into the critical framing without pre-empting their experience of the piece.

Using the NotebookLM template prompt with my Reflective Proposal, journal entries for Weeks 07 and 08, and data source documentation as sources, I generated a draft project statement and then evaluated it against the slide prompts: what was working, what was missing or underdeveloped, and what felt overly generalised. The draft captured the core concept — that the piece renders Spotify's algorithmic interpretation of mood as an inhabitable world — but leaned too heavily on describing the visual properties without sufficiently foregrounding the critical framing. The data portrait and the question of algorithmic opacity were underdeveloped in that first pass.

After revising the draft, the one-sentence directional commitment I wrote was: this project makes a machine's reading of emotional content into something a viewer can inhabit and question.

### Peer Share

I shared the revised draft and evaluation notes with a partner for the peer share exchange. Their feedback on what was clear and compelling identified the critical anchor — the idea that the space environment is Spotify's interpretation rather than a neutral portrait — as the strongest part of the statement. What they flagged as needing further development was the description of the interaction: the search mechanic and the dissolve transition between track environments were not yet present in the statement, and their absence made the piece sound more passive than it actually is. They also noted that the statement did not yet acknowledge the opacity of Spotify's valence scores as a deliberate provocation rather than a limitation.

Both observations were accurate and directed the revisions I carried forward into the making sprint.

### Making Sprint

Before the sprint I took ten minutes to plan, drawing on the draft statement and the peer feedback. The project most needed two things at this point: a refined nebula rendering that holds up at showcase display scale, and a tighter integration between the data portrait and the main canvas so the two visual registers feel compositionally unified rather than appended. I set those as the specific goals for the thirty-five minute sprint.

For the nebula, I replaced the single-layer noise call with three layered `noise()` passes at different scales and opacities, which produces a more complex atmospheric form with visible depth variation. The colour of each layer is tinted separately — the outermost layer takes the valence-driven hue directly, the inner layers shift slightly toward the complementary hue — so the nebula has internal variation rather than being a flat tinted wash. Testing at a larger canvas size confirmed the approach holds up at scale without becoming noisy or muddy.

For the data portrait integration, I repositioned the circular readout from the top-right corner to the bottom-left and adjusted its size so it sits proportionally within the canvas at the intended display dimensions. The arc strokes were thinned and the opacity reduced so the readout reads as a subtle informational layer rather than a competing graphic element. The track name and artist text below the arcs was restyled in a monospace typeface to emphasise its data-display character. The overall effect is closer to instrument panel than annotation — it reads as part of the piece rather than an explanation of it.

### Round Robin Rapid Reactions

For the round robin I presented my draft project statement and the current state of the p5.js sketch across two rounds, first as a presenter and then as a visitor. The reactions I noted during the presenting round were consistent across visitors. Several people immediately understood the critical angle without needing it explained — the phrase "Spotify's interpretation" in the statement landed as a provocation rather than a description. One visitor asked whether the piece would be running live during the showcase or displaying a recording, which confirmed that the live search interaction needs to be technically stable enough to run in public without a fallback. Another noted that the dissolve transition between track environments was one of the most compelling moments in the piece and suggested making it slightly slower to give viewers time to register that a change is happening.

During the visitor round I circulated across five other projects and used the visitor prompts to structure my responses. The most consistent observation I offered was about the relationship between statement and artefact: projects where the statement articulated a specific provocation — rather than a general theme — tended to have a clearer sense of what the visualisation needed to do. This reinforced my own commitment to keeping the algorithmic opacity framing central rather than letting it become a footnote.

The reactions and questions from this session fed directly into the independent study priorities for the week.

### Independent Study

#### Project Development

The independent study period was focused on two priorities that emerged from the making sprint and the round robin: technical stability for the live showcase context, and further revision of the project statement.

On the technical side, I rebuilt the OAuth authentication flow using the PKCE method to eliminate the hardcoded access token I had been using during development. The piece now handles the full authorisation cycle in the browser, redirecting to the Spotify login page and returning with a valid token that is stored in session storage for the duration of the session. I also built the fallback state that the Technical Commenter from Week 08 had suggested — when no track is detected or the Spotify session is inactive, the canvas displays a slow, cool, ambient environment with minimal movement, accompanied by a prompt in the data portrait area inviting the viewer to search for a track. This makes the piece self-contained in a showcase context where the presenter may not have Spotify actively playing.

The search interaction was also stabilised. The dropdown that appears when typing a query now dismisses cleanly when a track is selected, and the transition delay — currently two seconds — was extended to three seconds based on the round robin feedback that the dissolve needed more time to register. Timing this against several different track pairs confirmed that three seconds feels intentional rather than slow.

The project statement was revised in response to the peer share and round robin feedback to bring the search interaction into the description and to sharpen the framing of Spotify's valence scores as an active provocation rather than a technical constraint. The final committed direction from this week is to build toward a piece that holds both registers simultaneously: immersive enough to be felt, legible enough to be questioned.

#### Progress Report

The progress report for Week 10 covers: the current state of the p5.js sketch with screenshots of two contrasting track environments and the data portrait integration; the revised project statement; the key technical and conceptual decisions made since Week 08 — the nebula layering, the data portrait repositioning, and the extended transition timing; a set of visual references for the refined nebula aesthetic; and three feedback questions for the group. The questions are: whether three seconds is the right transition duration or whether it should be variable and tied to the tempo of the incoming track; whether the monospace typeface in the data portrait reinforces or undermines the immersive quality of the space environment; and whether the fallback ambient state communicates clearly enough that the piece is waiting for input rather than simply broken.
