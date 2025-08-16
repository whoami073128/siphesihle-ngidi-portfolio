# siphesihle-ngidi-portfolio

import React, { useMemo, useState } from "react";
import { motion, AnimatePresence } from "framer-motion";
import { GraduationCap, Briefcase, Download, Mail, Phone, MapPin, Link as LinkIcon, Award, ChevronDown, ExternalLink } from "lucide-react";

// --- Utility Components ---
const Section = ({ id, title, subtitle, children }) => (
  <section id={id} className="scroll-mt-24 py-16 md:py-24">
    <div className="max-w-6xl mx-auto px-4">
      <div className="mb-10">
        <h2 className="text-3xl md:text-4xl font-bold tracking-tight">{title}</h2>
        {subtitle && <p className="text-muted-foreground mt-2 max-w-3xl">{subtitle}</p>}
      </div>
      {children}
    </div>
  </section>
);

const Card = ({ children, className = "" }) => (
  <div className={`rounded-2xl border bg-card text-card-foreground shadow-sm ${className}`}>{children}</div>
);

const Pill = ({ children }) => (
  <span className="inline-flex items-center rounded-full border px-3 py-1 text-xs md:text-sm">{children}</span>
);

const Anchor = ({ href, children }) => (
  <a href={href} target="_blank" rel="noreferrer" className="inline-flex items-center gap-1 underline-offset-4 hover:underline">
    {children} <ExternalLink className="h-4 w-4" />
  </a>
);

// --- Data from CV ---
const profile = {
  name: "Siphesihle Ngidi",
  tagline: "Aspiring Chemical Engineer | Innovator | Problem Solver",
  summary:
    "Fourth-year Chemical Engineering student at the University of KwaZulu-Natal. Passionate about innovation, laboratory practice, and applying analytical thinking to real-world process challenges. Comfortable across Python, Aspen Plus, and web technologies.",
  contacts: {
    phone: "073 128 2898",
    emails: ["221012418@stu.ukzn.ac.za", "siphesihlengidi510@gmail.com", "sphesihleowakhe6@gmail.com"],
    studyAddress: "63 Elgie Rd, Umbilo, Berea, 4075",
    homeAddress: "134403 Ogunjini Village, Ndwedwe 4342",
  },
};

const experiences = [
  {
    title: "Laboratory Services – Chemical Engineering",
    org: "University of KwaZulu-Natal",
    range: "2021 – Present",
    points: [
      "Designed and executed experiments: sensor calibration (thermal, pressure, flow), heat exchangers, evaporators, and flow devices.",
      "Data acquisition & analysis using regression and error reporting; authored formal lab reports and posters.",
      "Hands-on with cooling towers, pumps, fans; residence time distribution, mass transfer, and fluidisation studies.",
      "Collaborated in team-based experiments; delivered oral and poster presentations.",
    ],
    tags: ["Process Labs", "Data Analysis", "Teamwork"],
  },
  {
    title: "Sales Representative",
    org: "Asmalls",
    range: "Nov 25, 2022 – Jan 5, 2023",
    points: [
      "Improved customer communication and needs discovery in a high-footfall retail environment.",
      "Built confidence and product knowledge under pressure.",
    ],
    tags: ["Customer Service", "Communication"],
  },
  {
    title: "Cashier (Seasonal)",
    org: "Asmalls",
    range: "Nov 18, 2023 – Jan 16, 2024",
    points: [
      "Processed high-volume transactions accurately; maintained queue flow and till compliance.",
      "Resolved customer queries swiftly; supported a fast-paced team environment.",
    ],
    tags: ["POS", "Accuracy", "Teamwork"],
  },
  {
    title: "Cashier (Seasonal)",
    org: "Asmalls",
    range: "Nov 19, 2024 – Jan 16, 2025",
    points: [
      "Returned based on reliability and performance; upheld service standards across peak periods.",
    ],
    tags: ["Reliability", "Service Excellence"],
  },
];

const education = {
  institution: "University of KwaZulu-Natal",
  degree: "BSc Eng (Chemical Engineering)",
  status: "In progress",
  highlights: [
    { code: "ENCH4RT", name: "Applied Reactor Technology", mark: 69, year: 2025 },
    { code: "ENCH2MB", name: "Mass & Energy Balances", mark: 73, year: 2022 },
    { code: "ENEL2CM", name: "Applied Computer Methods", mark: 84, year: 2022 },
    { code: "MATH131", name: "Mathematics 1A (Eng)", mark: 82, year: 2021 },
    { code: "ENCH4LA", name: "Laboratory/Industry Project 1", mark: 64, year: 2025 },
  ],
};

const skills = [
  "Python",
  "JavaScript",
  "HTML",
  "CSS",
  "AutoCAD",
  "Aspen Plus",
  "Octave",
  "Excel",
  "PowerPoint",
  "Machine Learning (beginner)",
  "Writing Proficiency",
  "PHP (basic)",
  "Critical Analysis",
  "Creative Thinking",
  "Teamwork",
  "Time Management",
  "Empathy",
];

const projects = [
  {
    title: "Python Fundamentals Mini-Projects",
    desc: "Applied arithmetic operations, data types, and file handling in small utilities and problem sets.",
    stack: ["Python"],
    link: null,
  },
  {
    title: "Web Basics & Game Dev Learnings",
    desc: "Built simple static pages with JavaScript interactivity; experimented with game loops and canvas.",
    stack: ["HTML", "CSS", "JavaScript"],
    link: null,
  },
];

const certificates = [
  { title: "Python for Beginners", issuer: "SoloLearn / Similar", date: "Sep 4, 2022", id: "CT-BVKCWEGA" },
  { title: "Introduction to CSS", issuer: "SoloLearn / Similar", date: "Jul 24, 2025", id: "CC-VYO9731G" },
  { title: "Tech Society – Membership & Contribution", issuer: "UKZN Tech Society", date: "2021–2025", id: "Member" },
];

// --- Components ---
const Nav = () => {
  const items = [
    { id: "home", label: "Home" },
    { id: "about", label: "About" },
    { id: "experience", label: "Experience" },
    { id: "education", label: "Education" },
    { id: "skills", label: "Skills" },
    { id: "projects", label: "Projects" },
    { id: "certs", label: "Certificates" },
    { id: "contact", label: "Contact" },
  ];
  return (
    <div className="sticky top-0 z-50 backdrop-blur supports-[backdrop-filter]:bg-background/60 border-b">
      <div className="max-w-6xl mx-auto px-4 h-16 flex items-center justify-between">
        <a href="#home" className="font-semibold">SN</a>
        <nav className="hidden md:flex gap-6 text-sm">
          {items.map((it) => (
            <a key={it.id} href={`#${it.id}`} className="text-muted-foreground hover:text-foreground">
              {it.label}
            </a>
          ))}
        </nav>
        <a
          href="/cv/Siphesihle_Ngidi_CV.pdf"
          className="inline-flex items-center gap-2 rounded-xl border px-3 py-2 text-sm hover:bg-accent"
        >
          <Download className="h-4 w-4" /> Download CV
        </a>
      </div>
    </div>
  );
};

const Hero = () => (
  <div className="relative overflow-hidden">
    <div className="absolute inset-0 -z-10 opacity-40 bg-gradient-to-tr from-primary/20 via-transparent to-primary/20" />
    <div className="max-w-6xl mx-auto px-4 pt-16 md:pt-24 pb-10 md:pb-16">
      <motion.h1
        initial={{ opacity: 0, y: 20 }}
        animate={{ opacity: 1, y: 0 }}
        transition={{ duration: 0.6 }}
        className="text-4xl md:text-6xl font-extrabold tracking-tight"
      >
        {profile.name}
      </motion.h1>
      <motion.p
        initial={{ opacity: 0, y: 10 }}
        animate={{ opacity: 1, y: 0 }}
        transition={{ delay: 0.1, duration: 0.6 }}
        className="mt-4 text-xl text-muted-foreground max-w-2xl"
      >
        {profile.tagline}
      </motion.p>
      <motion.p
        initial={{ opacity: 0, y: 10 }}
        animate={{ opacity: 1, y: 0 }}
        transition={{ delay: 0.2, duration: 0.6 }}
        className="mt-6 max-w-3xl"
      >
        {profile.summary}
      </motion.p>
      <div className="mt-8 flex flex-wrap gap-3">
        <Pill><Phone className="h-4 w-4 mr-2" /> {profile.contacts.phone}</Pill>
        {profile.contacts.emails.map((e) => (
          <Pill key={e}><Mail className="h-4 w-4 mr-2" /> {e}</Pill>
        ))}
        <Pill><MapPin className="h-4 w-4 mr-2" /> {profile.contacts.studyAddress}</Pill>
      </div>
    </div>
  </div>
);

const TimelineItem = ({ item }) => (
  <motion.li
    initial={{ opacity: 0, x: -12 }}
    whileInView={{ opacity: 1, x: 0 }}
    viewport={{ once: true }}
    transition={{ duration: 0.4 }}
    className="relative pl-8"
  >
    <div className="absolute left-0 top-1.5 h-3 w-3 rounded-full bg-primary" />
    <div className="flex flex-col md:flex-row md:items-center md:justify-between gap-2">
      <h4 className="font-semibold">{item.title} <span className="text-muted-foreground font-normal">— {item.org}</span></h4>
      <span className="text-sm text-muted-foreground">{item.range}</span>
    </div>
    <ul className="mt-2 list-disc pl-5 space-y-1 text-sm md:text-base">
      {item.points.map((p, i) => (
        <li key={i}>{p}</li>
      ))}
    </ul>
    <div className="mt-3 flex flex-wrap gap-2">
      {item.tags.map((t) => (
        <Pill key={t}>{t}</Pill>
      ))}
    </div>
  </motion.li>
);

const Experience = () => (
  <Section id="experience" title="Experience" subtitle="A blend of laboratory proficiency and customer-facing reliability.">
    <div className="relative">
      <div className="absolute left-1.5 top-0 bottom-0 w-px bg-border" />
      <ol className="space-y-8">
        {experiences.map((it, i) => (<TimelineItem key={i} item={it} />))}
      </ol>
    </div>
  </Section>
);

const Education = () => {
  const [open, setOpen] = useState(false);
  return (
    <Section id="education" title="Education" subtitle="Key modules and outcomes from my degree.">
      <Card className="p-6">
        <div className="flex items-start md:items-center justify-between gap-4">
          <div>
            <div className="flex items-center gap-3">
              <GraduationCap className="h-6 w-6" />
              <h3 className="text-xl font-semibold">{education.degree}</h3>
            </div>
            <p className="text-muted-foreground mt-1">{education.institution} — {education.status}</p>
          </div>
          <a href="#certs" className="underline underline-offset-4">See Certificates</a>
        </div>
        <div className="mt-6 grid md:grid-cols-2 gap-4">
          {education.highlights.map((m) => (
            <div key={m.code} className="flex items-center justify-between rounded-xl border p-4">
              <div>
                <p className="font-medium">{m.code} — {m.name}</p>
                <p className="text-sm text-muted-foreground">Year {m.year}</p>
              </div>
              <div className="text-2xl font-bold">{m.mark}</div>
            </div>
          ))}
        </div>
        <button
          onClick={() => setOpen((v) => !v)}
          className="mt-6 inline-flex items-center gap-2 rounded-xl border px-4 py-2 hover:bg-accent"
        >
          <ChevronDown className={`h-4 w-4 transition-transform ${open ? "rotate-180" : ""}`} />
          {open ? "Hide full module list (excerpt)" : "View more modules (excerpt)"}
        </button>
        <AnimatePresence>
          {open && (
            <motion.div initial={{ height: 0, opacity: 0 }} animate={{ height: "auto", opacity: 1 }} exit={{ height: 0, opacity: 0 }} className="overflow-hidden">
              <div className="mt-4 grid md:grid-cols-2 gap-3 text-sm">
                {[
                  "ENCH3MT Mass Transfer (55)",
                  "ENCH3TH Thermodynamics 2 (63)",
                  "ENCH3HE Heat Transfer (61)",
                  "ENCH3CP Practicals 2 (61)",
                  "ENCH3ED Design (55)",
                  "ENCH3SL Safety & Loss Prevention (51)",
                  "ENCH3FS Fluid & Solids Transport (51)",
                  "ENCH4MP Mineral Processing (50)",
                  "ENEL4EB Engineering Business (50)",
                  "STAT370 Engineering Statistics (61)",
                  "MATH354 Mathematics 3A (62)",
                  "MATH248/238/132/131 (various)",
                  "CHEM161/171/241/251/261 (various)",
                ].map((t) => (
                  <div key={t} className="rounded-xl border p-3 bg-muted/30">{t}</div>
                ))}
              </div>
            </motion.div>
          )}
        </AnimatePresence>
      </Card>
    </Section>
  );
};

const Skills = () => (
  <Section id="skills" title="Skills" subtitle="Tools, technologies, and strengths I work with.">
    <div className="grid sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-3">
      {skills.map((s) => (
        <div key={s} className="rounded-xl border p-3 text-sm flex items-center justify-between">
          <span>{s}</span>
          <div className="h-2 w-24 bg-muted rounded-full overflow-hidden">
            <div className="h-full w-3/4 bg-primary/70" />
          </div>
        </div>
      ))}
    </div>
  </Section>
);

const Projects = () => (
  <Section id="projects" title="Projects" subtitle="Selected academic and self-led work.">
    <div className="grid md:grid-cols-2 gap-6">
      {projects.map((p) => (
        <Card key={p.title} className="p-6">
          <h4 className="text-lg font-semibold">{p.title}</h4>
          <p className="mt-2 text-sm text-muted-foreground">{p.desc}</p>
          <div className="mt-4 flex flex-wrap gap-2">
            {p.stack.map((t) => (
              <Pill key={t}>{t}</Pill>
            ))}
          </div>
          {p.link && (
            <div className="mt-4">
              <Anchor href={p.link}>View project</Anchor>
            </div>
          )}
        </Card>
      ))}
    </div>
  </Section>
);

const Certificates = () => (
  <Section id="certs" title="Certificates & Achievements" subtitle="Recognition of learning and contribution.">
    <div className="grid md:grid-cols-3 gap-6">
      {certificates.map((c) => (
        <Card key={c.title} className="p-6">
          <div className="flex items-center gap-3">
            <Award className="h-6 w-6" />
            <h4 className="text-lg font-semibold">{c.title}</h4>
          </div>
          <p className="mt-2 text-sm text-muted-foreground">{c.issuer}</p>
          <p className="text-sm mt-1">{c.date}</p>
          <p className="text-xs text-muted-foreground mt-2">ID: {c.id}</p>
        </Card>
      ))}
    </div>
  </Section>
);

const Contact = () => (
  <Section id="contact" title="Contact" subtitle="Let’s talk about opportunities, collaboration, or ideas.">
    <Card className="p-6">
      <div className="grid md:grid-cols-2 gap-6">
        <div>
          <h4 className="font-semibold">Direct</h4>
          <div className="mt-3 space-y-2 text-sm">
            <div className="flex items-center gap-2"><Phone className="h-4 w-4" /> {profile.contacts.phone}</div>
            {profile.contacts.emails.map((e) => (
              <div key={e} className="flex items-center gap-2"><Mail className="h-4 w-4" /> <a href={`mailto:${e}`} className="underline underline-offset-4">{e}</a></div>
            ))}
            <div className="flex items-center gap-2"><MapPin className="h-4 w-4" /> {profile.contacts.homeAddress}</div>
          </div>
        </div>
        <form className="grid gap-3">
          <div>
            <label className="text-sm">Name</label>
            <input className="mt-1 w-full rounded-xl border px-3 py-2 bg-background" placeholder="Your name" />
          </div>
          <div>
            <label className="text-sm">Email</label>
            <input type="email" className="mt-1 w-full rounded-xl border px-3 py-2 bg-background" placeholder="you@example.com" />
          </div>
          <div>
            <label className="text-sm">Message</label>
            <textarea rows={4} className="mt-1 w-full rounded-xl border px-3 py-2 bg-background" placeholder="Say hello..." />
          </div>
          <button type="button" onClick={() => alert("Thanks! This demo form does not send yet.")} className="rounded-xl border px-4 py-2 hover:bg-accent w-fit">Send Message</button>
        </form>
      </div>
    </Card>
  </Section>
);

const About = () => (
  <Section id="about" title="About Me" subtitle="A short professional snapshot.">
    <div className="grid md:grid-cols-3 gap-6 items-start">
      <Card className="p-6 md:col-span-2">
        <p>
          From an early interest in how chemical processes shape daily life, I’ve grown into an analytical, hands-on
          engineer-in-training. I enjoy solving problems systematically and communicating results clearly—whether in
          lab reports, presentations, or team discussions. I’m excited by sustainable solutions in mining & processing and
          the opportunity to learn from experienced professionals.
        </p>
        <div className="mt-6 flex flex-wrap gap-2">
          <Pill>Innovation</Pill>
          <Pill>Process Thinking</Pill>
          <Pill>Continuous Learning</Pill>
        </div>
      </Card>
      <Card className="p-6">
        <h4 className="font-semibold">Quick Links</h4>
        <ul className="mt-3 space-y-2 text-sm">
          <li><a className="underline underline-offset-4" href="#projects">See Projects</a></li>
          <li><a className="underline underline-offset-4" href="#experience">Experience Timeline</a></li>
          <li><a className="underline underline-offset-4" href="#skills">Technical Skills</a></li>
          <li><a className="underline underline-offset-4" href="#certs">Certificates</a></li>
        </ul>
      </Card>
    </div>
  </Section>
);

export default function PortfolioSiphesihle() {
  // Ensure smooth scrolling
  React.useEffect(() => {
    document.documentElement.classList.add("scroll-smooth");
  }, []);

  return (
    <div className="min-h-screen bg-background text-foreground">
      <Nav />
      <main id="home">
        <Hero />
        <About />
        <Experience />
        <Education />
        <Skills />
        <Projects />
        <Certificates />
        <Contact />
      </main>
      <footer className="border-t py-10">
        <div className="max-w-6xl mx-auto px-4 flex flex-col md:flex-row md:items-center md:justify-between gap-4">
          <p className="text-sm text-muted-foreground">© {new Date().getFullYear()} {profile.name}. All rights reserved.</p>
          <div className="flex items-center gap-4 text-sm">
            <Anchor href="https://vercel.com">Deploy on Vercel</Anchor>
            <Anchor href="https://pages.github.com/">Host on GitHub Pages</Anchor>
          </div>
        </div>
      </footer>
    </div>
  );
}
