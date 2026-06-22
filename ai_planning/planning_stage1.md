# Planning - Stage 1 - June 2026

This is a planning document for my personal website.

**IMPORTANT**: AI agents CANNOT edit this file.

The website is a Github page, meaning that it is a single html page hosted by Github: https://fertmeneses.github.io

## Constrains

My website must:
- Represent my personal trajectory styles and values.
- Be hosted free of charge.
- Have a relatively simple design, nothing too fancy nor heavy to be displayed (computational resources)
- Be tracked by Google analytics (it is currently being tracked)

## Suggestions for next version V2

Right now, my website has a very simple structure, displaying section after section without a top nor side menues, and without animations.
It is using a very simple style in @_config.yml: remote_theme: pages-themes/slate@v0.2.0.
One aspect that I don't like is that content display is a single narrow column, which leaves a lot of blank spaces for wide screens.

I want suggestions to improve the layout a bit more:
- Add some animations but not many nor too heavy, as I want to page to load fast.
- Improve the layout so it becomes more readable.
- Make the website responsive to different screen sizes.
- Add a floating top menu.
- Add a banner at the bottom that explicitly says that the website is designed by me, assisted by Clauce Code.
- If necessary, you change the configuration of [README.md + _config.yml] to something else, but it must work with Github pages.
- If you add colors bor boxes, decoration, etc., then one of the main colors must be green, similar to #169903ff.

Also, I will modify some of the core features of my website:

- The section Scientific Publications currently shows all my papers as a list with links. I want to convert them in something much more graphical and limited in space, because this section is not very important anymore. Maybe a carrousel, or a tiles gallery that are expanded on hover/touch. 

- The section Research AI-Projects and Coding Challenges should be merged into a single section "AI-Projects and Challenges", keep the order of the subsections and the content.

- In the "Core competencies" section, let's change ⚙️ Machine Learning & AI: Deep learning | Computer vision | Time series forecasting | NLP | Classical ML (scikit-learn) to the following: 🤖 Machine Learning & Agentic AI: Deep learning | Claude Code | Spec-driven development | Computer vision | Time series forecasting.
Change [☁️ Cloud & Big Data: Google Cloud Platform (GCP) | BigQuery | Dataproc | SQL] to:
[☁️ Cloud & Big Data: AWS | GCP | SQL]
Change [🤝 Soft Skills: Clear communication of technical results | Problem-solving | Cross-functional collaboration | Project leadership | Project management | International teamworking] to:
🤝 Soft Skills: Communication | Problem-solving | Project leadership | Project management | Teamworking

## Comments after AI implementation - Version 1

After commit 8969cfa84c99ebfcc455e7fce8d6072dc0041eac, I have the following comments:

Things I like:

- Top menu
- Dark/bright themes
- Scientific publications tiles

Things should be improved:

- The header section, with my image and text, has a terrible layout, with a lot of blank space next to my image. You should place the text next to the image. Also, change the left margin of the card, that's too Claude-standard-style, I want to stand out, so make something different.
- Core compentencies should be organized with a more attractive layout, with some animations. The text should always be visible.
- In CV and links, the GitHub icon cannot be seen in the dark mode, because it is black.
- In Career trajectory, the layout is terrible: the images on the left take a lot of space in wide screens.
- In AI-Projects and Challenges, similar comment for layout: images take too much space in some cases, when the text is relatively short. For example, the Crypto project has a too large image. The other projects are ok, so reduce the crypto image size.
In Spaceship Titanic, there is a too large space between the two text paragraphs! Reduce that space.
The Open coding challenge image should be to the left, and also reduce the image a bit. Again, there is a too large space between the two paragraphs.
- In Media releases, same comment for image size: they are too big compared to the text in the cases "Graduates" and "Show us your Science".
- In Image Gallery, fit the images in one row for each subsection
- Remove the "Back to top", it is no necessary now that we have the top menu.
- Change "Designed by Fernando Meneses, assisted by Claude Code." by "Designed by Fernando Meneses, using spec-driven development with AI agents."

Scientific Publication Updates:

- <a class="pub-tile" href="https://arxiv.org/abs/2505.13675" target="_blank" rel="noopener"><span class="pub-venue">arXiv</span><span class="pub-year">2025</span><span class="pub-title">Temperature dependence of coercivity for isolated Ni nanowires unraveled by high-sensitivity micromagnetometry</span><span class="pub-cta">Open →</span></a> should be changed by:
<a class="pub-tile" href="https://journals.aps.org/prb/abstract/10.1103/dcf2-7rsc" target="_blank" rel="noopener"><span class="pub-venue">Physical Review B</span><span class="pub-year">2025</span><span class="pub-title">Temperature dependence of coercivity for isolated Ni nanowires unraveled by high-sensitivity micromagnetometry</span><span class="pub-cta">Open →</span></a>
- New publication: 
<a class="pub-tile" href="https://iopscience.iop.org/article/10.1088/1361-6463/ae410e/meta" target="_blank" rel="noopener"><span class="pub-venue">J. Phys. D: Appl. Phys.</span><span class="pub-year">2026</span><span class="pub-title">Readout optimisation for spin-based quantum sensing using the nitrogen vacancy centre in diamond</span><span class="pub-cta">Open →</span></a>

## Suggestions for next version V3

Comments after version V2:

Things I like:

- The header is great now
- Core competencies is much better
- GitHub icon is great now
- Gallery is great now

Things I don't like:

- In Core compentences, if we could introduce slight animations, like enlargement on tiles when hovering, or some color highlighting, that would be better.
- The section CV and links looks poor compared to the other sections now. Let's implement something different there, such as tiles, but more creative.
- The Career trajectory section now looks much worse! The icons for companies are too small (at least in wide screens), you should enlarge the column on the right, reduce the one on the left and at the same time enlarge the icons. Implement some creative layout as well, and/or animations. You can play with the icons, the date ranges, the titles and the contents of each work-element.
- The crypto image is too small now, enlarge it so it occupies the same space as the text content (two paragraphs).
- In the Quantum Sensing project, include all the text in the right column.
- In the Noise Spectroscopy project, there is too wide space between the title and the first paragraph, and then between the description and the links
- In the Titanic-disaster section, place all text and links on the right column.
- In the Spaceship Titanic section, now the image is extremly small!
- In the Bottle sets section, place all text and links to the right, enlarge the image a bit.
- In Media releases, let's alternate images in left-right columns, starting on the left. For Graduates, enlarge the image 50% more.
- Top menu: when you click a section, the screen goes to that section but the title is placed too low, it should place it on top.