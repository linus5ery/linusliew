<template>
  <div class="site">
    <nav class="nav">
      <div class="wrap">
        <a class="brand" href="#top">
          <img src="./assets/logo.png" alt="" />
          Linus Liew
        </a>
        <button class="menu-btn" @click="menuOpen = !menuOpen" :aria-expanded="menuOpen">Menu</button>
        <ul :class="{ open: menuOpen }">
          <li v-for="l in links" :key="l.id">
            <a :href="'#' + l.id" :class="{ active: activeId === l.id }" @click="menuOpen = false">{{ l.label }}</a>
          </li>
        </ul>
      </div>
    </nav>

    <header class="hero" id="top">
      <div class="wrap">
        <div>
          <span class="eyebrow">Freelance developer · Web & Mobile</span>
          <h1>Hi, I'm Linus.<br>I build with <em class="typed">{{ typed }}<span class="caret" aria-hidden="true"></span></em></h1>
          <p class="lead">
            I turn ideas into clean, responsive web apps and mobile apps, and the scripts that keep them running.
            7+ years of experience, now freelancing full time.
          </p>
          <div class="actions">
            <a class="btn btn-primary" href="#contact">Hire me</a>
            <a class="btn btn-ghost" href="#services">See what I do</a>
          </div>
        </div>
        <div class="portrait-stage">
          <img class="portrait" src="./assets/profile_pic.jpg" alt="Linus Liew" />
          <div class="portrait-tag"><strong>Open for projects</strong>Freelancing and working remotely.</div>
        </div>
      </div>
    </header>

    <div class="strip">
      <div class="wrap">
        <div v-for="s in stats" :key="s.label"><b>{{ s.value }}</b><span>{{ s.label }}</span></div>
      </div>
    </div>

    <section class="block" id="services">
      <div class="wrap">
        <div class="head">
          <span class="eyebrow">What I do</span>
          <h2>From first sketch to live product</h2>
          <p>Pick one service or let me handle the whole build. Either way you get clear updates and code you can maintain.</p>
        </div>
        <div class="services">
          <div class="service" v-for="s in services" :key="s.title">
            <svg viewBox="0 0 40 40" aria-hidden="true">
              <polygon :points="s.shape" fill="var(--accent)" />
              <polygon :points="s.shape2" fill="var(--accent-deep)" />
            </svg>
            <h3>{{ s.title }}</h3>
            <p>{{ s.text }}</p>
          </div>
        </div>
      </div>
    </section>

    <section class="block" id="projects" style="padding-top:0">
      <div class="wrap">
        <div class="head">
          <span class="eyebrow">Projects</span>
          <h2>Guess Translate Word</h2>
          <p>An Android word game I built at my company for language learners. You see a word in another language and guess what it means. Try a round right here.</p>
        </div>

        <div class="product">
          <div class="product-intro">
            <img src="./assets/guess-logo.png" alt="Guess Translate Word app icon" />
            <h3>Guess Translate Word</h3>
            <p>Hello, 你好, apa khabar. Learn everyday words across languages one guess at a time.</p>
            <div class="chips">
              <span class="chip" v-for="c in ['English', '中文', 'Bahasa Melayu']" :key="c">{{ c }}</span>
            </div>
            <ul class="feature-list">
              <li>Short rounds that fit a coffee break</li>
              <li>Hints show the language and how to say it</li>
              <li>Track your streak as you learn</li>
            </ul>
            <p class="built-with">Android · Testing on Google Play</p>
          </div>

          <div class="game">
            <div class="game-top">
              <span class="label">Try it · Round {{ round }} of {{ deck.length }}</span>
              <span class="score">Score {{ score }} · Streak {{ streak }}</span>
            </div>
            <template v-if="!finished">
              <div class="card-word">
                <small>{{ current.lang }}</small>
                <div class="word">{{ current.word }}</div>
                <div class="hint">{{ showHint ? 'Say it: ' + current.say : '' }}</div>
              </div>
              <div class="options">
                <button v-for="o in current.options" :key="o" class="opt" :class="optClass(o)" :disabled="picked !== null" @click="pick(o)">{{ o }}</button>
              </div>
              <div class="game-foot">
                <span class="feedback" aria-live="polite">{{ feedback }}</span>
                <button v-if="picked === null" class="btn btn-outline-light" @click="showHint = true">Show hint</button>
                <button v-else class="btn btn-light" @click="next">{{ round < deck.length ? 'Next word' : 'See result' }}</button>
              </div>
            </template>
            <template v-else>
              <div class="card-word">
                <small>Round complete</small>
                <div class="word">{{ score }} / {{ deck.length }}</div>
                <div class="hint">{{ score === deck.length ? 'Perfect score. Bravo!' : 'Nice work. Play again to beat it.' }}</div>
              </div>
              <div class="game-foot"><span></span><button class="btn btn-light" @click="restart">Play again</button></div>
            </template>
          </div>
        </div>
      </div>
    </section>

    <section class="block" id="experience" style="padding-top:0">
      <div class="wrap">
        <div class="head">
          <span class="eyebrow">Work experience</span>
          <h2>Where I've been building</h2>
        </div>
        <ol class="timeline">
          <li class="job" v-for="job in workExperience" :key="job.company + job.period">
            <span class="job-period">{{ job.period }}</span>
            <div>
              <h3>{{ job.role }}</h3>
              <p class="job-company">{{ job.company }}</p>
              <ul>
                <li v-for="point in job.points" :key="point">{{ point }}</li>
              </ul>
            </div>
          </li>
        </ol>
      </div>
    </section>

    <section class="block" id="about" style="padding-top:0">
      <div class="wrap about">
        <div>
          <div class="head" style="margin-bottom:24px">
            <span class="eyebrow">About me</span>
            <h2>A developer who likes the web best</h2>
          </div>
          <p>
            Hey there! I have 7+ years of experience as a developer and I love discovering new technologies,
            especially in software. I switched to freelance and work through Upwork, so feel free to reach out about any exciting project.
          </p>
          <p>
            My main languages are Python, PHP and Vue. I prefer web over native apps because the web offers so many
            possibilities, and responsive design means one product works on every screen.
          </p>
        </div>
        <div class="values">
          <div class="value" v-for="v in values" :key="v.mark">
            <span class="mark">{{ v.mark }}</span>
            <div><h3>{{ v.title }}</h3><p>{{ v.text }}</p></div>
          </div>
        </div>
      </div>
    </section>

    <section class="block contact" id="contact">
      <div class="wrap contact-grid">
        <div class="head">
          <span class="eyebrow">Contact</span>
          <h2>Have a project in mind?</h2>
          <p>Reach out through any of these channels and I'll get back to you as soon as possible.</p>
        </div>
        <!-- TODO: replace with your real contact details -->
        <div class="contact-list">
          <a class="contact-item" v-for="c in contacts" :key="c.label" :href="c.href" target="_blank" rel="noopener">
            <span>
              <small>{{ c.label }}</small>
              {{ c.value }}
            </span>
            <span class="arrow" aria-hidden="true">→</span>
          </a>
        </div>
      </div>
    </section>

    <footer>
      <div class="wrap">
        <span>© {{ year }} Linus Liew. All rights reserved.</span>
        <span>Freelance developer · Python, PHP & Vue</span>
      </div>
    </footer>
  </div>
</template>

<script>
// Word list for the Guess Translate Word demo (same as the AY-Tech site).
const WORDS = [
  { word: '你好', lang: 'Chinese', say: 'nǐ hǎo', answer: 'Hello', pool: ['Goodbye', 'Thank you', 'Friend'] },
  { word: 'Apa khabar', lang: 'Malay', say: 'AH-pah KAH-bar', answer: 'How are you?', pool: ['Where are you?', 'What time is it?', 'Excuse me'] },
  { word: 'Terima kasih', lang: 'Malay', say: 'teh-REE-mah KAH-see', answer: 'Thank you', pool: ['Welcome', 'Hello', 'Yes'] },
  { word: '谢谢', lang: 'Chinese', say: 'xiè xie', answer: 'Thank you', pool: ["You're welcome", 'Good morning', 'Water'] },
  { word: '朋友', lang: 'Chinese', say: 'péng you', answer: 'Friend', pool: ['Family', 'Teacher', 'Book'] },
];
const shuffle = (a) => {
  const b = a.slice();
  for (let i = b.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [b[i], b[j]] = [b[j], b[i]];
  }
  return b;
};
// Picks 5 random words and shuffles each word's answer options.
const buildDeck = () => shuffle(WORDS).slice(0, 5).map((w) => ({ ...w, options: shuffle([w.answer, ...w.pool]) }));

export default {
  name: 'App',
  data() {
    return {
      menuOpen: false,
      activeId: '',
      year: new Date().getFullYear(),
      roles: ['Python', 'PHP', 'Vue'],
      typed: '',
      links: [
        { id: 'services', label: 'Services' },
        { id: 'projects', label: 'Projects' },
        { id: 'experience', label: 'Experience' },
        { id: 'about', label: 'About' },
        { id: 'contact', label: 'Contact' },
      ],
      stats: [
        { value: '7+', label: 'Years of experience' },
        { value: 'Python', label: 'Plus PHP & Vue' },
        { value: 'Platform', label: 'Web and Mobile' },
        { value: 'Remote', label: 'Working worldwide' },
      ],
      services: [
        { title: 'Web development', text: 'Responsive websites and web apps built with Vue, from landing pages to full single-page applications.', shape: '4,8 36,8 36,16 4,16', shape2: '4,22 26,22 26,32 4,32' },
        { title: 'Backend & APIs', text: 'REST APIs and server-side logic in Python and PHP, including database design and third-party integrations.', shape: '4,4 18,4 18,18 4,18', shape2: '22,22 36,22 36,36 22,36' },
        { title: 'Automation & scripting', text: 'Python scripts that automate repetitive tasks, scrape and process data, or glue your tools together.', shape: '4,36 20,4 26,4 12,36', shape2: '20,36 30,14 36,36' },
        { title: 'Maintenance & fixes', text: 'Fixing bugs, improving performance and adding features to your existing Python, PHP or Vue codebase.', shape: '20,4 36,20 20,36 4,20', shape2: '20,12 28,20 20,28 12,20' },
      ],
      workExperience: [
        {
          period: 'Sep 2026 – Present',
          role: 'Founder',
          company: 'Linus Liew',
          points: [
            'Building fluent, complete and lag-free mobile apps and websites.',
            'Using less AI during development and thinking outside the box to build complete systems.',
            'Focused on unique products for Southeast Asia and worldwide markets, connecting users across countries.',
          ],
        },
        {
          period: 'Sep 2023 – Nov 2025',
          role: 'Full Stack Developer',
          company: 'BeED · Full-time · Subang Jaya, Selangor (Hybrid)',
          points: [
            'Built Curriculum Builder, Gradebook, Admin Panel and Nexus with the latest Angular forms and components, including Signals.',
            'Implemented SEO for better searchability and SSR for more secure rendering in Angular.',
            'Restructured Angular classes, HTML, CSS and TypeScript across 100+ code files for a tidier codebase.',
            'Migrated the ASP.NET file storage system from AWS S3 to local storage.',
            'Increased the image upload limit from 1MB to 5MB in Node.js.',
            'Converted most of the native MySQL code into raw queries in Node.js, making it easier to switch database services.',
            'Built 20+ new APIs for the revamped Admin Panel with response times under 300 ms in Node.js.',
            'Updated Node.js packages to be compatible with Docker builds.',
            'Worked with my supervisor and all team leads to meet project goals and timelines.',
            'Technologies: Angular 7 & 13, Node.js 10 & 14, TypeScript, ASP.NET, Redis, RabbitMQ, Docker, MSSQL, MySQL.',
          ],
        },
        {
          period: 'May 2022 – Jun 2023',
          role: 'Frontend Developer',
          company: 'UP DevLabs · Full-time · Bangsar South (On-site)',
          points: [
            'Developed and maintained a high-traffic e-gaming website mixing Vue 2 and Vue 3 components, working on most browsers including Safari.',
            'Applied theme changes to an e-gaming app using mixins, merging at least 5 codebases into 1 in uni-app with cross-platform support for Android, iOS and web.',
            'Worked with QA engineers and the QA team lead to keep the website and app error-free, smooth and consistent for users.',
            'Technologies: Vue 2 & 3, uni-app.',
          ],
        },
        {
          period: 'May 2021 – Apr 2022',
          role: 'Software Engineer',
          company: 'HOMIEE Malaysia · Full-time · Subang Jaya, Selangor (On-site)',
          points: [
            'Refined a rental property website and app with modern full-stack technology and responsive design, including listing search, listing management and built-in SEO.',
            'Helped launch the website and app, keeping one UI design language across Angular and React Native and using Redis to keep booking transactions stable.',
            'Joined daily Agile stand-ups to discuss user stories and tasks, sharing ideas and time estimates for each task.',
            'Technologies: Angular, Node.js, React Native, GraphQL, MongoDB, Redis.',
          ],
        },
        {
          period: 'Aug 2019 – Mar 2021',
          role: 'Java Developer',
          company: 'Confidential · Full-time · Petaling Jaya, Selangor',
          points: [
            'Enhanced and fixed the e-Cover website, the backbone of the insurance platform used by Tokio Marine, Chubb and MPI Generali.',
            'Checked the password encryption feature connected to the Tokio Marine HQ manual system.',
            'Adjusted Motor tariff rates and ensured correct calculations for the Tokio Marine website.',
            'Built the SecureHome website for Tokio Marine through 3 to 5 full-featured revisions, making the most of JavaScript and jQuery.',
            'Improved the Admin Panel system across 100+ code files by updating JSP servlets with no issues during the platform change.',
            'Implemented a new policy issuance process with identity verification, improved backend logic and built the Nomination feature for the MPI Generali website.',
            'Technologies: Java, JSP, J2EE, JavaScript, jQuery.',
          ],
        },
        {
          period: 'Jan 2017 – May 2017',
          role: 'Software Engineer Intern',
          company: 'Nettium Sdn Bhd · Internship · Kuala Lumpur',
          points: [
            'Supported the development and maintenance of a real-time e-gaming website built on ASP.NET.',
            'Created test cases and submitted them to QA for validation, learning the end-to-end workflow of running a real-time website.',
            'Gained practical full-stack experience and a stronger understanding of web development.',
            'Technologies: ASP.NET, MSSQL.',
          ],
        },
      ],
      values: [
        { mark: '01', title: 'Listen first', text: 'Understand the problem before writing a line of code.' },
        { mark: '02', title: 'Ship often', text: 'Small, working releases so you see progress every week.' },
        { mark: '03', title: 'Leave it clean', text: 'Readable, documented code that is easy to hand over.' },
      ],
      // Guess Translate Word demo state
      deck: buildDeck(),
      round: 1,
      score: 0,
      streak: 0,
      picked: null,
      showHint: false,
      feedback: 'Pick the meaning.',
      finished: false,
      contacts: [
        { label: 'Email', value: 'jlinuskl2@gmail.com', href: 'mailto:jlinuskl2@gmail.com' },
        { label: 'GitHub', value: 'github.com/linus5ery', href: 'https://github.com/linus5ery' },
        { label: 'LinkedIn', value: 'linkedin.com/in/linusliewkaile', href: 'https://www.linkedin.com/in/linusliewkaile' }, 
        { label: 'X', value: 'x.com/linus5ery', href: 'https://x.com/linus5ery' },
      ],
    };
  },
  computed: {
    current() {
      return this.deck[this.round - 1];
    },
  },
  created() {
    document.title = 'Linus Liew';
  },
  mounted() {
    this.startTyping();
    this.watchSections();
  },
  beforeUnmount() {
    clearTimeout(this.typeTimer);
    if (this.observer) this.observer.disconnect();
  },
  methods: {
    pick(o) {
      this.picked = o;
      if (o === this.current.answer) {
        this.score++;
        this.streak++;
        this.feedback = 'Correct!';
      } else {
        this.streak = 0;
        this.feedback = 'It means “' + this.current.answer + '”.';
      }
    },
    optClass(o) {
      if (this.picked === null) return '';
      if (o === this.current.answer) return 'right';
      return o === this.picked ? 'wrong' : '';
    },
    next() {
      if (this.round >= this.deck.length) {
        this.finished = true;
        return;
      }
      this.round++;
      this.picked = null;
      this.showHint = false;
      this.feedback = 'Pick the meaning.';
    },
    restart() {
      Object.assign(this, { deck: buildDeck(), round: 1, score: 0, streak: 0, picked: null, showHint: false, finished: false, feedback: 'Pick the meaning.' });
    },
    // Types each role, pauses, deletes it, then moves to the next one.
    startTyping() {
      if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
        this.typed = this.roles[0];
        return;
      }
      let roleIndex = 0;
      let deleting = false;
      const tick = () => {
        const word = this.roles[roleIndex];
        this.typed = deleting ? word.slice(0, this.typed.length - 1) : word.slice(0, this.typed.length + 1);
        let delay = deleting ? 60 : 110;
        if (!deleting && this.typed === word) {
          deleting = true;
          delay = 1600;
        } else if (deleting && this.typed === '') {
          deleting = false;
          roleIndex = (roleIndex + 1) % this.roles.length;
          delay = 300;
        }
        this.typeTimer = setTimeout(tick, delay);
      };
      tick();
    },
    // Highlights the nav link for the section currently on screen.
    watchSections() {
      this.observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((e) => {
            if (e.isIntersecting) this.activeId = e.target.id;
          });
        },
        { rootMargin: '-45% 0px -50% 0px' }
      );
      this.links.forEach((l) => {
        const el = document.getElementById(l.id);
        if (el) this.observer.observe(el);
      });
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,500;12..96,700;12..96,800&family=Figtree:wght@400;500;600&family=Dancing+Script:wght@700&display=swap");

/* Same layout as AY-Tech, recoloured for Linus Liew: deep green-charcoal page, emerald accent, warm cream text. */
:root {
  color-scheme: dark;
  --bg: #1b1f1d;
  --bg-deep: #141716;
  --surface: #242a27;
  --line: #36403b;
  --fg: #faf2df;
  --muted: #b9bdb0;
  --accent: #50c878;
  --accent-deep: #2f9e5a;
  --accent-soft: #a6e8bd;
  --gold: #ece090;
  --font-display: "Bricolage Grotesque", "Segoe UI", system-ui, sans-serif;
  --font-body: "Figtree", "Segoe UI", system-ui, sans-serif;
  --wrap: 1120px;
}
* { box-sizing: border-box; }
html { scroll-behavior: smooth; scroll-padding-top: 72px; }
body {
  margin: 0; background: var(--bg); color: var(--fg);
  font-family: var(--font-body); font-size: 17px; line-height: 1.6;
}
a { color: inherit; }
:focus-visible { outline: 2px solid var(--accent-soft); outline-offset: 3px; border-radius: 6px; }
.wrap { max-width: var(--wrap); margin-inline: auto; padding-inline: 20px; }
h1, h2, h3 { font-family: var(--font-display); line-height: 1.05; text-wrap: balance; margin: 0; }
.eyebrow {
  font-size: 13px; font-weight: 600; letter-spacing: .14em; text-transform: uppercase; color: var(--accent-soft);
}

/* Nav */
.nav {
  position: sticky; top: 0; z-index: 10;
  background: color-mix(in srgb, var(--bg) 88%, transparent); backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--line);
}
.nav .wrap { display: flex; align-items: center; justify-content: space-between; gap: 16px; padding-block: 10px; position: relative; }
.brand { display: flex; align-items: center; gap: 10px; text-decoration: none; font-family: var(--font-display); font-weight: 700; font-size: 20px; letter-spacing: .02em; }
.brand img { width: 44px; height: 44px; border-radius: 10px; object-fit: contain; }
.nav ul { list-style: none; display: flex; gap: 22px; margin: 0; padding: 0; font-weight: 500; }
.nav ul a { text-decoration: none; color: var(--muted); }
.nav ul a:hover, .nav ul a.active { color: var(--fg); }
.menu-btn { display: none; background: none; border: 1px solid var(--line); color: var(--fg); border-radius: 8px; padding: 6px 12px; font: inherit; cursor: pointer; }

/* Hero */
.hero { padding-block: 64px 72px; position: relative; overflow: hidden; }
.hero .wrap { display: grid; grid-template-columns: 1.1fr .9fr; gap: 40px; align-items: center; }
.hero h1 { font-size: clamp(44px, 7vw, 84px); font-weight: 800; letter-spacing: -.02em; margin-block: 14px 20px; }
.hero h1 em { font-style: normal; color: var(--accent); white-space: nowrap; }
.caret {
  display: inline-block; width: .08em; height: .85em; margin-left: .06em; vertical-align: -.05em;
  background: var(--gold); animation: blink .8s step-end infinite;
}
@keyframes blink { 50% { opacity: 0; } }
.hero p.lead { font-size: 19px; color: var(--muted); max-width: 38ch; margin: 0 0 30px; }
.actions { display: flex; flex-wrap: wrap; gap: 12px; }
.btn {
  display: inline-flex; align-items: center; gap: 8px; text-decoration: none; cursor: pointer;
  font: 600 16px var(--font-body); padding: 13px 22px; border-radius: 999px; border: 1.5px solid transparent;
  transition: transform .15s ease, background .15s ease, border-color .15s ease;
}
.btn:hover { transform: translateY(-2px); }
.btn-primary { background: var(--accent); color: #0f2a1a; }
.btn-primary:hover { background: var(--accent-soft); }
.btn-ghost { border-color: var(--line); color: var(--fg); background: transparent; }
.btn-ghost:hover { border-color: var(--accent); }

.portrait-stage { position: relative; aspect-ratio: 1; max-width: 100%; display: grid; place-items: center; }
.portrait-stage::before {
  content: ""; position: absolute; inset: 2%; border-radius: 50%;
  background: radial-gradient(circle, color-mix(in srgb, var(--accent) 26%, transparent), transparent 68%);
}
.portrait {
  position: relative; width: 72%; aspect-ratio: 1; object-fit: cover; border-radius: 50%;
  border: 6px solid var(--surface); box-shadow: 0 0 0 2px var(--accent);
  animation: float 6s ease-in-out infinite;
}
@keyframes float { 0%,100% { transform: translateY(0); } 50% { transform: translateY(-12px); } }
.portrait-tag {
  position: absolute; right: 2%; bottom: 6%; background: var(--bg-deep); border: 1px solid var(--line);
  border-radius: 12px; padding: 10px 14px; font-size: 14px; color: var(--muted); max-width: 220px;
}
.portrait-tag strong { display: flex; align-items: center; gap: 8px; color: var(--fg); font-family: var(--font-display); font-size: 16px; }
.portrait-tag strong::before { content: ""; width: 8px; height: 8px; border-radius: 50%; background: var(--accent); }

/* Stats strip */
.strip { border-block: 1px solid var(--line); background: var(--bg-deep); }
.strip .wrap { display: grid; grid-template-columns: repeat(4, 1fr); gap: 20px; padding-block: 26px; }
.strip div b { display: block; font-family: var(--font-display); font-size: 30px; color: var(--accent-soft); font-variant-numeric: tabular-nums; }
.strip div span { color: var(--muted); font-size: 15px; }

/* Sections */
section.block { padding-block: 88px; }
.head { max-width: 620px; margin-bottom: 44px; }
.head h2 { font-size: clamp(34px, 5vw, 54px); font-weight: 700; margin-top: 10px; }
.head p { color: var(--muted); margin: 16px 0 0; }

/* Services */
.services { display: grid; grid-template-columns: repeat(2, 1fr); gap: 1px; background: var(--line); border: 1px solid var(--line); border-radius: 20px; overflow: hidden; }
.service { background: var(--bg); padding: 30px 28px; display: flex; flex-direction: column; gap: 10px; }
.service svg { width: 40px; height: 40px; }
.service h3 { font-size: 22px; font-weight: 700; }
.service p { margin: 0; color: var(--muted); }

/* Project showcase: Guess Translate Word keeps its own purple brand colours */
.product {
  --purple: #a63fdc; --purple-deep: #7d22b0; --lilac: #f6ecfd; --ok: #7be0a8; --bad: #ff9a8a;
  --font-script: "Dancing Script", "Brush Script MT", cursive;
  background: var(--purple); color: var(--lilac); border-radius: 28px; overflow: hidden;
  display: grid; grid-template-columns: .85fr 1.15fr;
}
.product-intro { padding: 44px 40px; display: flex; flex-direction: column; gap: 18px; background: var(--purple-deep); }
.product-intro img { width: 112px; height: 112px; border-radius: 26px; box-shadow: 0 10px 30px rgba(0,0,0,.25); }
.product-intro h3 { font-family: var(--font-script); font-size: 46px; font-weight: 700; line-height: 1; }
.product-intro p { margin: 0; color: color-mix(in srgb, var(--lilac) 82%, transparent); }
.product-intro .built-with { font-size: 14px; letter-spacing: .08em; text-transform: uppercase; font-weight: 600; }
.chips { display: flex; flex-wrap: wrap; gap: 8px; }
.chip { font-size: 14px; padding: 5px 12px; border-radius: 999px; background: rgba(255,255,255,.14); }
.feature-list { list-style: none; padding: 0; margin: 4px 0 0; display: grid; gap: 10px; }
.feature-list li { display: flex; gap: 10px; }
.feature-list li::before { content: "✓"; font-weight: 700; color: var(--lilac); }
.game { padding: 40px; display: flex; flex-direction: column; gap: 20px; }
.game-top { display: flex; justify-content: space-between; align-items: center; gap: 12px; flex-wrap: wrap; font-size: 14px; }
.game-top .label { letter-spacing: .12em; text-transform: uppercase; font-weight: 600; }
.score { font-variant-numeric: tabular-nums; background: rgba(0,0,0,.18); padding: 5px 12px; border-radius: 999px; }
.card-word { background: var(--lilac); color: #3a1452; border-radius: 20px; padding: 30px 24px; text-align: center; }
.card-word small { display: block; font-size: 13px; letter-spacing: .12em; text-transform: uppercase; color: #8a5aa8; font-weight: 600; }
.card-word .word { font-family: var(--font-script); font-size: clamp(40px, 6vw, 58px); line-height: 1.15; margin-top: 6px; overflow-wrap: anywhere; }
.card-word .hint { font-size: 14px; color: #8a5aa8; margin-top: 4px; min-height: 1.4em; }
.options { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
.opt {
  font: 600 17px var(--font-body); padding: 15px 14px; border-radius: 14px; cursor: pointer;
  border: 2px solid rgba(255,255,255,.35); background: rgba(255,255,255,.08); color: var(--lilac);
  transition: background .15s, border-color .15s, transform .15s;
}
.opt:hover:not(:disabled) { background: rgba(255,255,255,.18); transform: translateY(-1px); }
.opt:disabled { cursor: default; }
.opt.right { background: var(--ok); border-color: var(--ok); color: #0e3a24; }
.opt.wrong { background: var(--bad); border-color: var(--bad); color: #4a120a; }
.game-foot { display: flex; justify-content: space-between; align-items: center; gap: 12px; flex-wrap: wrap; min-height: 48px; }
.feedback { font-weight: 600; }
.btn-light { background: var(--lilac); color: var(--purple-deep); }
.btn-outline-light { background: transparent; color: var(--lilac); border-color: rgba(255,255,255,.4); }
.btn-outline-light:hover { border-color: var(--lilac); }

/* Experience */
.timeline { list-style: none; margin: 0; padding: 0; display: grid; gap: 14px; }
.job {
  display: grid; grid-template-columns: 180px 1fr; gap: 24px; padding: 24px 26px;
  background: var(--surface); border-radius: 16px; border-left: 4px solid var(--accent);
}
.job-period { font-size: 14px; font-weight: 600; letter-spacing: .06em; color: var(--gold); padding-top: 4px; font-variant-numeric: tabular-nums; }
.job h3 { font-size: 22px; }
.job-company { margin: 4px 0 10px; color: var(--accent-soft); font-weight: 500; }
.job ul { margin: 0; padding-left: 20px; color: var(--muted); }

/* About */
.about { display: grid; grid-template-columns: 1fr 1fr; gap: 48px; align-items: start; }
.about p { color: var(--muted); margin: 0 0 16px; max-width: 60ch; }
.values { display: grid; gap: 14px; }
.value { display: grid; grid-template-columns: 52px 1fr; gap: 16px; padding: 18px 20px; background: var(--surface); border-radius: 16px; }
.value .mark { font-family: var(--font-display); font-weight: 800; font-size: 28px; color: var(--accent); line-height: 1.1; font-variant-numeric: tabular-nums; }
.value h3 { font-size: 19px; margin-bottom: 4px; }
.value p { margin: 0; font-size: 15px; }

/* Contact */
.contact { background: var(--bg-deep); border-top: 1px solid var(--line); }
.contact-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 48px; }
.contact-list { display: grid; gap: 12px; align-content: start; }
.contact-item {
  display: flex; justify-content: space-between; align-items: center; gap: 16px; text-decoration: none;
  padding: 16px 20px; background: var(--surface); border: 1px solid var(--line); border-radius: 14px;
  overflow-wrap: anywhere; transition: border-color .15s ease, transform .15s ease;
}
.contact-item small { display: block; font-size: 13px; font-weight: 600; letter-spacing: .1em; text-transform: uppercase; color: var(--muted); }
.contact-item .arrow { color: var(--accent); font-size: 20px; transition: transform .15s ease; }
.contact-item:hover { border-color: var(--accent); }
.contact-item:hover .arrow { transform: translateX(4px); }
footer { padding-block: 28px; border-top: 1px solid var(--line); color: var(--muted); font-size: 14px; background: var(--bg-deep); }
footer .wrap { display: flex; justify-content: space-between; gap: 12px; flex-wrap: wrap; }

@media (max-width: 880px) {
  .hero .wrap, .about, .contact-grid, .product { grid-template-columns: 1fr; }
  .game, .product-intro { padding: 28px 22px; }
  .portrait-stage { max-width: 420px; margin-inline: auto; width: 100%; }
  .services { grid-template-columns: 1fr; }
  .strip .wrap { grid-template-columns: repeat(2, 1fr); }
  .job { grid-template-columns: 1fr; gap: 6px; }
  .menu-btn { display: inline-block; }
  .nav ul { display: none; position: absolute; left: 0; right: 0; top: 100%; flex-direction: column; gap: 0; background: var(--bg-deep); border-bottom: 1px solid var(--line); }
  .nav ul.open { display: flex; }
  .nav ul a { display: block; padding: 14px 20px; }
  section.block { padding-block: 64px; }
}
@media (max-width: 420px) { .options { grid-template-columns: 1fr; } }
@media (prefers-reduced-motion: reduce) {
  .opt:hover:not(:disabled) { transform: none; }
  .portrait, .caret { animation: none; }
  html { scroll-behavior: auto; }
  .btn:hover { transform: none; }
}
</style>
