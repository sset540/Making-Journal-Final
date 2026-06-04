## Week 10

Week ten was the second formal critique session of the project phase, structured around progress report presentations, a gallery walk across Padlet boards, and an action plan. With two weeks remaining before the showcase, the session had a different quality to Week 08's critique — the feedback was more focused on resolution and completion than on open-ended redirection, and the action plan that came out of it needed to be specific enough to drive the final sprint of development.

### Progress Reports

Groups of five or six formed at the start of class with Chair, Technical Commenter, and Conceptual Commenter roles assigned and rotated after each presenter. I presented the five-slide progress report prepared during Week 09 independent study, which covered the current state of the p5.js sketch, the revised project statement, the key decisions made since Week 08, visual references for the nebula aesthetic, and three feedback questions: whether the three-second transition duration was right or should be tempo-driven, whether the monospace typeface in the data portrait reinforced or undermined the immersive quality, and whether the fallback ambient state communicated clearly enough that the piece was waiting for input.

The feedback posted to my Padlet card across the four columns was detailed and consistent. The Technical Commenter raised a practical concern about browser compatibility — specifically whether the Spotify OAuth PKCE flow would behave consistently across different browsers in a showcase context where the hardware and browser version would be fixed but unknown in advance. They recommended testing on Chrome and Firefox ahead of Week 12 and building a clear error state for cases where authentication fails. They also noted that the canvas resize behaviour needed attention: if the sketch was displayed at a resolution different from the one it was developed on, the nebula and star field proportions might break.

The Conceptual Commenter engaged directly with the typeface question and came down clearly in favour of keeping the monospace: their reading was that the instrument-panel quality of the data portrait was precisely what distinguished it from decorative data art, and that switching to a proportional typeface would soften the critical edge. On the transition timing question, they suggested that tempo-driven duration was conceptually strong but risked being imperceptible in practice — a viewer watching the dissolve would not know whether it was fast or slow because of the tempo unless the tempo was also made visible somehow. Their suggestion was to keep the duration fixed but use the tempo value to vary the easing curve of the transition instead, so fast-tempo tracks dissolve with a sharper onset and slow-tempo tracks ease in more gradually. This felt immediately right as a solution — it preserves the critical legibility of the data mapping without introducing a variable the viewer cannot read.

The Chair noted that the fallback state was the right call for a showcase context but that the current prompt text — inviting the viewer to search for a track — was too small to read from a standing distance. They recommended increasing the type size and moving the prompt to a more central position on the canvas so it functions as an invitation rather than a footnote.

### Gallery Walk

After the progress report session I visited the other groups' Padlet boards via the main class board and browsed the Technical and Conceptual feedback cards. The most common technical concern across projects was display and scale — how work developed on a laptop screen translates to a larger monitor or projector in the showcase space. Several projects were also navigating questions about interaction in a public context: how much instruction a viewer needs, and what happens when the piece is left unattended between interactions. These are directly relevant to my own project and reinforced the fallback state as a necessary component rather than an optional refinement.

On the conceptual side, the gallery walk highlighted how much the quality of the project statement shapes the way feedback is given. Projects with a clearly articulated provocation received more specific and useful conceptual feedback than those where the critical framing was still implicit. The statement revision I had done in Week 09 appeared to be paying off — the Conceptual Commenter's response to my project was grounded in the algorithmic opacity framing rather than treating the piece as a general music visualiser.

I added comments to two other projects' cards — one offering a suggestion about how a static data layer could be used to anchor an otherwise kinetic composition, and one upvoting feedback about the importance of testing interaction timing with people unfamiliar with the piece.

### Action Plan

The critique session produced three clear action points for the final two weeks of development.

The first priority is canvas scaling and browser compatibility. The sketch needs to be tested at the display resolution that will be used in the showcase and on both Chrome and Firefox. Any proportional issues with the nebula or star field at non-standard canvas sizes need to be resolved before Week 12, and a clear error state needs to be built for cases where the OAuth flow fails or the Spotify API is unreachable.

The second priority is refining the fallback state and the search prompt. The prompt text needs to be larger and repositioned toward the centre of the canvas so it reads clearly from a standing distance. The fallback ambient environment should be visually distinct enough from an active track environment that a viewer understands the piece is in a waiting state rather than displaying a fixed output.

The third priority is implementing the tempo-driven easing curve for the transition, as suggested by the Conceptual Commenter. This is a relatively contained technical change — adjusting the easing function used in the lerp-based transition rather than the duration itself — but it adds a layer of data expressiveness that the current fixed dissolve lacks.

The broader framing I am carrying into the final development sprint is that the piece needs to be robust enough to run without supervision in a public showcase context. Every interaction path — successful search, failed authentication, no active Spotify session — needs to lead somewhere intentional rather than to a broken or empty state.

### Independent Study

#### Project Development

The independent study period was spent working through the three action points from the action plan, with a focus on the technical stability tasks first since they represent the most risk to the Week 12 showcase.

Canvas scaling was addressed by replacing the fixed-dimension canvas with a responsive setup that fills the browser window and redraws proportionally on resize. The nebula generation was refactored to use normalised coordinates — positioning and scale defined as proportions of canvas width and height rather than fixed pixel values — which means the composition holds at any display resolution. Testing at 1920×1080 and 2560×1440 confirmed the approach works without visual degradation.

Browser compatibility testing revealed one issue: the session storage approach used to persist the OAuth access token between page loads behaved differently in Firefox's private mode, where session storage is cleared between navigations. Since the PKCE flow involves a redirect back to the page, this caused the token to be lost mid-authentication on Firefox private. The fix was to use the URL hash parameters returned by the redirect — where Spotify deposits the authorisation code — as the primary source of truth rather than relying on session storage surviving the redirect. This resolved the issue across both browsers.

The fallback state was redesigned so that the search prompt sits centrally on the canvas in larger type, set in the same monospace typeface as the data portrait. The ambient environment behind it uses a slow, cool palette — deep blue-violet with minimal movement — that is visually consistent with a low-valence, low-energy track environment but distinct enough from an active state that the waiting condition reads clearly.

The tempo-driven easing curve was implemented using a cubic easing function whose steepness is mapped from the incoming track's tempo value. High-tempo tracks now dissolve with a sharper initial onset that settles quickly, while low-tempo tracks ease in gradually across the full three seconds. The difference is subtle but perceptible when switching between tracks at opposite ends of the tempo range, and it adds a layer of responsiveness to the transition that the fixed linear dissolve lacked.

With the three action points addressed, the remaining development work for Week 11 is focused on visual quality — refining the star field rendering and finalising the data portrait styling — and preparing the project statement as a formatted PDF for submission alongside the GitHub Pages documentation.
