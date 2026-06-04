## Week 06

Week six marked the return from the mid-semester break and the official start of the second phase of the course. The class shifted from broad experimentation to a focused design project, with the Proposal Consultation taking place at the start of the session followed by three structured in-class activities. This week also signalled a change in how the journal entries are assessed — from this point forward, weeks six through twelve form the process documentation component of the Data-Driven Visualisation assignment.

### Proposal Consultation

The first part of class was dedicated to scheduled Proposal Consultations, which ran as 10-minute one-on-one conversations with a course teacher throughout the afternoon. The consultation was structured as an Interactive Oral Assessment, meaning it was an unscripted conversation rather than a rehearsed presentation. Drawing on my written Reflective Proposal, the discussion covered my thematic focus, the data source I intended to use, my approach to visualisation in p5.js, and the intended impact of the work.

Coming into the consultation I had been thinking about what kind of data could produce genuinely expressive, dynamic visual output rather than static or slowly shifting information. The conversation helped me crystallise a direction I had been circling: using music as a data source. Specifically, the Spotify API exposes audio feature data for any track — valence, energy, tempo, danceability, acousticness — and these variables map naturally to visual properties like colour, brightness, density, and movement speed. The teacher responded positively to the idea of music as a live, personal data source and pushed me to think about what the visual world would actually look like. This question — what environment would respond meaningfully to the emotional character of a song — became the central design question I carried into the in-class activities.

### Data Exploration

The first in-class activity involved locating, accessing, and examining the intended data source. The Spotify Web API is a publicly accessible REST API that returns audio analysis and audio feature data for any track. The audio features endpoint returns a JSON object containing numerical values for energy (0.0–1.0), valence (0.0–1.0, where high values indicate positivity), tempo (BPM), danceability, acousticness, instrumentalness, and loudness (in dB). These are pre-computed by Spotify's audio analysis algorithms and are available for any track in the Spotify catalogue.

The data is live in the sense that it is fetched in real time for whichever track is currently playing or selected, though the feature values themselves are fixed per track rather than changing over time. The Spotify Web Playback SDK can additionally return real-time playback state — current track, position in the track, and player controls — which would allow the visualisation to respond to what is actually playing in a Spotify session.

In terms of limitations, the audio feature values are black-box outputs from Spotify's internal models — there is no documentation of exactly how valence or energy are computed, which means the data carries assumptions I cannot fully audit. Two tracks I might describe as equally melancholy could receive very different valence scores. This opacity is worth acknowledging in the project, as it means the visualisation is responding to Spotify's interpretation of a song's mood rather than any neutral or objective measurement. This is itself an interesting feature of the data: it raises questions about who gets to define what a song feels like, and how that definition gets encoded into a number.

### Visual Research and Precedent Study

The second activity involved gathering visual references relevant to the project. Because the visualisation will render a space environment — stars, nebulae, planets — that shifts in character with the mood of music, I looked at references spanning both data-driven art and space imagery.

The first reference was Robert Hodgin's *Magnetosphere*, a generative visualisation originally built for iTunes that translated music into flowing particle systems. What draws me to it is the way it treats audio data as energy rather than information — the visuals feel like a physical response to sound rather than a representation of it. I want to carry forward that sense of immediacy and responsiveness, where the visual environment and the music feel genuinely coupled.

The second reference was the Hubble Space Telescope's deep field images, particularly the varied colour palettes across different nebulae. The natural range from cool blue-violet to warm amber-red maps intuitively onto emotional temperature in music — cold, sparse tracks versus warm, dense ones. This gives the colour system a visual logic that feels grounded rather than arbitrary.

The third reference was Refik Anadol's *Machine Hallucinations*, which uses large datasets to generate fluid, immersive visual environments. The relevant quality is scale and atmosphere — the feeling of being inside a data landscape rather than looking at a chart. I want the space environment to feel genuinely immersive.

The fourth reference was the work of Memo Akten, particularly his *Simple Harmonic Motion* series, which maps mathematical and physical data to organic visual behaviour. His use of noise functions to create movement that feels alive is directly relevant to how I want to animate the stars and nebula forms in response to audio feature data.

The fifth reference was a range of independent Spotify visualisation experiments on Observable and CodePen that map audio features to colour gradients and particle behaviour in real time. Seeing these confirmed the technical feasibility of the approach and gave me a clearer sense of which API variables are most visually productive — energy and valence proved far more interesting than tempo alone.

### Project Planning and Skills Roadmap

The third activity involved sketching what the final artefact might look like and identifying skills to develop.

The sketch I produced shows a full-screen canvas depicting a deep space environment. Stars of varying size and brightness are distributed across the canvas, with a large nebula-like form occupying the centre-background. The visual properties that respond to the Spotify data are: the dominant colour palette (shifting from cool to warm based on valence), the density and brightness of stars (scaling with energy), the speed of particle movement (driven by tempo), and the size and opacity of the nebula form (responding to acousticness). A high-energy, high-valence track would produce a bright, fast, warm, star-dense scene. A low-energy, low-valence track would produce a dark, slow, cool, sparse one.

The skills I need to develop are ranked as follows. First, authenticating with the Spotify Web API using OAuth and fetching audio feature data for the currently playing track. Second, mapping the returned data values to visual properties in p5.js using the `map()` function. Third, generating a convincing space environment using noise functions for nebula forms and random placement for stars. Fourth, building a smooth transition system so the visual environment shifts gradually when the track changes. Fifth, managing the API polling rate so the sketch stays performant without exceeding Spotify's rate limits.

My next steps are to set up a Spotify developer account, register an application to obtain API credentials, and build a minimal prototype that fetches audio feature data for a hardcoded track and logs the values to the console before mapping them to visual properties.

### Independent Study

#### Consultation Reflection

The Proposal Consultation confirmed the direction and sharpened one key question: what does the visual environment communicate beyond being a beautiful response to music? The teacher's question about intended impact pushed me to think about the project not just as a technical experiment but as a provocation about how data shapes experience. The Spotify audio features are algorithmic interpretations of emotional content — they encode a machine's reading of how a song feels. The space environment becomes a way of making that invisible interpretation visible and experiential. A viewer watching the visualisation is seeing Spotify's emotional model of the music rendered as a world. This framing — making the algorithm's interpretation of mood into something you can inhabit — became the critical anchor for the project going forward.

#### Technical Skill Building

The first priority from the skills roadmap was setting up Spotify API access. I registered a developer application at developer.spotify.com, which provided a Client ID and Client Secret. The Spotify Web API uses OAuth 2.0 for authentication, and for a client-side p5.js application the most practical approach is the PKCE authorisation flow, which returns an access token without requiring a server to store the client secret.

I worked through the Spotify API documentation and successfully completed an authorisation flow in the browser, obtaining an access token. I then used the `/me/player/currently-playing` endpoint to fetch data for the track currently playing in my Spotify session, and the `/audio-features/{id}` endpoint to retrieve the audio feature values. Logging the returned JSON to the console confirmed the data was accessible and formatted as expected — valence, energy, tempo, and the other features were present as decimal values between 0 and 1.

This was a significant technical milestone. Having confirmed that the pipeline from Spotify to the browser works, the next stage is connecting those values to visual output in p5.js.

#### Initial Concept Sketch

Building on the planning sketch from class, I developed a more refined digital sketch in p5.js that begins to establish the space environment. Using `noise()` to generate a slowly shifting nebula-like form in the background and random placement for a star field, the canvas already has the atmospheric quality I am aiming for. Colour is not yet data-driven — I used a fixed deep blue-purple palette to establish the base aesthetic and test the visual language before introducing the API data. The next step is connecting the Spotify feature values to the colour, brightness, and movement properties already in the sketch.
