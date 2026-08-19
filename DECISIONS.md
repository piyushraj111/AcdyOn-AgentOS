# Engineering Decisions — AcdyOn AgentOS

## 1. Why I chose this architecture over the alternatives

When I sat down to plan the project, I originally thought about spinning up a React app with Vite because that is what I usually reach for. But after thinking through what the page actually needs to do, I realized that would be total overkill.

React makes sense when you have shared state, nested routing, or dozens of dynamic components talking to each other. For a single landing page with a few DOM toggles and an interactive canvas, pulling in a build pipeline and 200MB+ of node_modules just adds dead weight. I went with semantic HTML5, Tailwind CSS via CDN, and a modular vanilla JS script. It loads instantly in the browser without any hydration delay, and inspecting or debugging the DOM in DevTools is completely frictionless.

For the background effect, I knew I wanted moving stars to give the page an active runtime feel. My options were to grab an existing library like Particles.js or Three.js, or write something lightweight myself. I skipped the heavy libraries because they often tank frame rates when layered underneath CSS backdrop-filter blurs. Instead, I wrote a ~40-line canvas loop from scratch. It stays locked at 60fps, lets me control particle density directly, and made it easy to swap particle colors between themes without tearing down DOM nodes.

The challenge brief made a clear point about avoiding fake social proof like made-up user numbers or fake review cards. I completely agree with that. Instead of inventing claims, I built an interactive workflow simulator and a throughput calculator with a live volume slider. This lets anyone inspecting the project actually click around, test out inputs, and see how the state machine behaves in real time.

---

## 2. Trade-offs and compromises under time constraints

With a tight deadline, you have to prioritize what matters most to the user experience and leave out the heavy backend setup.

The biggest compromise was the waitlist form. Building an Express backend with PostgreSQL, auth tokens, and queue management just to collect waitlist emails would have eaten up too much time. I ended up routing the form through FormSubmit using an asynchronous fetch call. It sends submissions straight to my inbox and swaps in a clean UI confirmation state without refreshing the page. If I had another week, I would write a proper serverless Edge API with rate-limiting and a real database table.

Another minor edge case is canvas resizing. If you manually drag and stretch the browser window width on desktop, the canvas clears and re-renders stars at fresh random coordinates rather than smoothly interpolating existing ones. It looks completely fine on standard fixed screens, but it is something I noticed while resizing windows during testing.

---

## 3. Where I used AI and what I had to fix myself

I used AI tools as a sounding board for initial layout ideas and for drafting repetitive utility classes. However, getting the page to feel polished and accessible took a lot of manual debugging.

AI helped me get started with Tailwind utility combinations, baseline color tokens, and the initial boilerplate for the canvas requestAnimationFrame loop. It also suggested the starting math formulas for the latency-to-savings curve on the slider.

The real engineering work came down to fixing what broke:

First, the starter canvas code only drew white stars. That looked great in dark mode, but the second I clicked the theme toggle, the stars completely vanished against the light slate background. I had to rewrite the draw loop to inspect the document element's active theme class and dynamically paint dark charcoal and indigo particles whenever light mode was active.

Second, the navbar initially had zero visual separation. It looked completely flat and blended straight into the moving starfield behind it. I rebuilt it with a backdrop-blur-2xl glass layer, an illuminated border, and high-contrast pill navigation containers so it stays distinct while scrolling.

Third, the mobile layout broke badly around 390px. The 4-column metric grid and 3-step pipeline were squishing together into narrow columns and causing horizontal scroll. I restructured the layout breakpoints so all multi-column sections collapse into single-column vertical cards on mobile viewports.

Finally, I did an accessibility pass across the DOM. The initial draft had generic clickable div elements, so I replaced them with proper button and anchor tags, ensured clear focus-visible outline rings for keyboard users, and verified contrast ratios across both color themes.
