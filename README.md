Skip to main content

Youth Launchpad

Details


Added Skipped Questions
Jun 18, 10:21 PM

Created
robots.txt
User-agent: *
Allow: /

Created
hero-workshop.jpg


Created
AppShell.tsx
import { Link } from "@tanstack/react-router";
import type { ReactNode } from "react";
export function AppShell({ children }: { children: ReactNode }) {
  return (
    <div className="min-h-screen bg-background text-foreground pb-28">
      <header className="sticky top-0 z-40 bg-background/85 backdrop-blur-md border-b border-burnt-light/40">
        <div className="max-w-6xl mx-auto px-5 py-4 flex items-center justify-between">
          <Link to="/" className="flex items-center gap-2">
            <div className="size-9 rounded-xl bg-burnt-dark text-burnt-light grid place-items-center font-display font-extrabold">V</div>
            <div className="leading-tight">
              <div className="font-display font-extrabold tracking-tight">VUKA</div>
              <div className="text-[10px] uppercase tracking-widest text-burnt-primary">Township Portal · SA</div>
            </div>
          </Link>
          <nav className="hidden sm:flex items-center gap-1 text-sm font-medium">
            <NavLink to="/" label="Home" />
            <NavLink to="/opportunities" label="Opportunities" />
            <NavLink to="/centers" label="Skills Centers" />
            <NavLink to="/arduino" label="Arduino Buzzer" />
          </nav>
        </div>
      </header>
      <main className="max-w-6xl mx-auto px-5 pt-6">{children}</main>
      <nav className="sm:hidden fixed bottom-4 left-4 right-4 z-50 bg-burnt-dark text-burnt-light rounded-2xl px-4 py-3 shadow-2xl flex justify-between">
        <BottomLink to="/" label="Home" />
        <BottomLink to="/opportunities" label="Jobs" />
        <BottomLink to="/centers" label="Skills" />
        <BottomLink to="/arduino" label="Buzzer" />
      </nav>
    </div>
  );
}
function NavLink({ to, label }: { to: string; label: string }) {
  return (
    <Link
      to={to}
      activeOptions={{ exact: to === "/" }}
      className="px-3 py-1.5 rounded-lg text-foreground/70 hover:text-burnt-dark hover:bg-burnt-light/30 transition-colors"
      activeProps={{ className: "px-3 py-1.5 rounded-lg bg-burnt-dark text-burnt-light" }}
    >
      {label}
    </Link>
  );
}
function BottomLink({ to, label }: { to: string; label: string }) {
  return (
    <Link
      to={to}
      activeOptions={{ exact: to === "/" }}
      className="flex-1 text-center text-[11px] font-bold uppercase tracking-wider opacity-60"
      activeProps={{ className: "flex-1 text-center text-[11px] font-bold uppercase tracking-wider opacity-100" }}
    >
      {label}
    </Link>
  );
}

Created
OpportunityCard.tsx
import type { Opportunity } from "@/lib/data";
const typeStyles: Record<Opportunity["type"], string> = {
  learnership: "bg-burnt-dark text-burnt-light",
  internship: "bg-burnt-mid text-white",
  job: "bg-burnt-light text-burnt-dark",
};
export function OpportunityCard({ o }: { o: Opportunity }) {
  return (
    <article className="bg-card rounded-2xl border border-burnt-light/50 p-5 shadow-sm hover:shadow-md transition-shadow">
      <div className="flex items-start justify-between gap-3 mb-3">
        <div className="min-w-0">
          <span className={`inline-block text-[10px] font-bold uppercase tracking-wider px-2 py-1 rounded ${typeStyles[o.type]}`}>
            {o.type}
          </span>
          <h3 className="font-display font-bold text-lg mt-2 leading-tight truncate">{o.title}</h3>
          <p className="text-sm text-muted-foreground">{o.company} · {o.location}</p>
        </div>
      </div>
      <p className="text-sm text-foreground/80 leading-relaxed mb-4">{o.summary}</p>
      <div className="flex items-center justify-between text-xs">
        <div className="flex flex-col">
          {o.stipend && <span className="font-bold text-burnt-primary">{o.stipend}</span>}
          <span className="text-muted-foreground">Closes: {o.closing}</span>
        </div>
        <button className="bg-burnt-dark text-burnt-light px-4 py-2 rounded-xl text-xs font-bold hover:bg-burnt-primary transition-colors">
          Apply
        </button>
      </div>
    </article>
  );
}

Created
data.ts
export type OppType = "learnership" | "internship" | "job";
export interface Opportunity {
  id: string;
  type: OppType;
  title: string;
  company: string;
  location: string;
  stipend?: string;
  closing: string;
  summary: string;
}
export interface Course {
  id: string;
  title: string;
  center: string;
  duration: string;
  practical: string;
}
export interface Center {
  id: string;
  name: string;
  township: string;
  focus: string[];
  contact: string;
}
export const opportunities: Opportunity[] = [
  { id: "o1", type: "learnership", title: "Junior Solar Installation Tech", company: "Green Energy SA", location: "Soweto, GP", stipend: "R4 500 / month", closing: "30 Jul 2026", summary: "12-month NQF L3 learnership. Practical install training plus theory at the Diepkloof Skills Hub." },
  { id: "o2", type: "internship", title: "UX/UI Design Intern", company: "Kasi Creative Lab", location: "Tembisa, GP", stipend: "R3 000 / month", closing: "12 Jul 2026", summary: "6-month studio internship. Shadow designers on real client work. Laptop provided." },
  { id: "o3", type: "job", title: "Retail Sales Associate", company: "Township Market Co.", location: "Khayelitsha, WC", stipend: "R5 200 / month", closing: "Open", summary: "Entry-level full-time. Friendly attitude required. Training on the job." },
  { id: "o4", type: "learnership", title: "Plumbing Apprentice (NQF 2)", company: "BuildRight Trades", location: "Mamelodi, GP", stipend: "R3 800 / month", closing: "05 Aug 2026", summary: "18 months. Mix of on-site work and classroom modules. Grade 10 minimum." },
  { id: "o5", type: "internship", title: "Junior Data Analyst", company: "Cape Insights", location: "Gugulethu, WC", stipend: "R6 000 / month", closing: "20 Jul 2026", summary: "Excel + SQL crash course included. Matric required." },
  { id: "o6", type: "job", title: "Coffee Shop Barista", company: "Vuka Café", location: "Alexandra, GP", stipend: "R4 800 + tips", closing: "Open", summary: "Morning and afternoon shifts. Free barista certification after 3 months." },
];
export const courses: Course[] = [
  { id: "c1", title: "Master Barista Basics", center: "Hospitality Hub Soweto", duration: "2 weeks", practical: "60% practical on real espresso machines" },
  { id: "c2", title: "Intro to Web Development", center: "Empower Skills Hub", duration: "4 weeks", practical: "Build & deploy a real portfolio site" },
  { id: "c3", title: "Welding Fundamentals", center: "Kliptown Works", duration: "3 weeks", practical: "Workshop hours on MIG & arc welders" },
  { id: "c4", title: "Sewing & Textile Design", center: "Orlando East Skills Lab", duration: "3 weeks", practical: "Produce 3 finished garments" },
  { id: "c5", title: "Basic Electrical Wiring", center: "Mamelodi Trade Centre", duration: "5 weeks", practical: "Wire a full demo board to code" },
  { id: "c6", title: "Arduino & Electronics 101", center: "Maker Lab Tembisa", duration: "2 weeks", practical: "Build a buzzer alert circuit" },
];
export const centers: Center[] = [
  { id: "k1", name: "Empower Skills Hub", township: "Soweto", focus: ["Digital", "Design", "Coding"], contact: "011 555 0101" },
  { id: "k2", name: "Hospitality Hub Soweto", township: "Soweto", focus: ["Barista", "Cooking", "Service"], contact: "011 555 0102" },
  { id: "k3", name: "Kliptown Works", township: "Soweto", focus: ["Welding", "Metalwork"], contact: "011 555 0103" },
  { id: "k4", name: "Orlando East Skills Lab", township: "Soweto", focus: ["Textiles", "Sewing"], contact: "011 555 0104" },
  { id: "k5", name: "Maker Lab Tembisa", township: "Tembisa", focus: ["Electronics", "Arduino", "IoT"], contact: "011 555 0105" },
  { id: "k6", name: "Mamelodi Trade Centre", township: "Mamelodi", focus: ["Electrical", "Plumbing"], contact: "012 555 0106" },
];

Created
arduino.tsx
import { createFileRoute } from "@tanstack/react-router";
import { AppShell } from "@/components/AppShell";
export const Route = createFileRoute("/arduino")({
  head: () => ({
    meta: [
      { title: "Arduino Buzzer — Notification Setup · VUKA" },
      { name: "description", content: "Step-by-step guide to wire your Arduino + breadboard + buzzer prototype to the VUKA app and get a physical buzz on every new opportunity." },
      { property: "og:title", content: "Arduino Buzzer Setup · VUKA" },
      { property: "og:description", content: "Hook your Arduino prototype to VUKA opportunity alerts." },
    ],
  }),
  component: ArduinoPage,
});
function ArduinoPage() {
  return (
    <AppShell>
      <header className="max-w-3xl">
        <span className="text-[10px] font-bold text-burnt-primary uppercase tracking-widest">Maker Mode</span>
        <h1 className="font-display text-3xl sm:text-4xl font-extrabold mt-2">Wire your Arduino buzzer to VUKA</h1>
        <p className="text-muted-foreground mt-2">
          You'll build a notification buzzer: every time VUKA has a new opportunity that matches you, your Arduino on the bench buzzes for half a second. The Arduino polls a small JSON endpoint over Wi-Fi (ESP8266/ESP32) or Serial (Uno + laptop bridge).
        </p>
      </header>
      <section className="mt-8 grid lg:grid-cols-2 gap-4">
        <Card title="What you need">
          <ul className="list-disc pl-5 space-y-1 text-sm">
            <li>1 × Arduino Uno <em>or</em> ESP8266 / ESP32 (Wi-Fi makes it standalone)</li>
            <li>1 × breadboard</li>
            <li>1 × active piezo buzzer (3–5 V)</li>
            <li>2 × jumper wires</li>
            <li>1 × 100 Ω resistor (optional, protects the pin)</li>
            <li>USB cable + laptop</li>
          </ul>
        </Card>
        <Card title="How it works">
          <ol className="list-decimal pl-5 space-y-1 text-sm">
            <li>VUKA exposes a tiny JSON feed at <Code>/api/alerts.json</Code>.</li>
            <li>Arduino asks that URL every 30 seconds.</li>
            <li>If the <Code>newCount</Code> went up since last check, the buzzer beeps.</li>
          </ol>
        </Card>
      </section>
      <Step n={1} title="Wire the circuit">
        <p>On the breadboard:</p>
        <ul className="list-disc pl-5 space-y-1 text-sm mt-2">
          <li>Buzzer <b>+</b> (long leg) → Arduino digital pin <Code>D8</Code> (through the 100 Ω resistor if you have one).</li>
          <li>Buzzer <b>–</b> (short leg) → Arduino <Code>GND</Code>.</li>
        </ul>
        <p className="text-xs text-muted-foreground mt-2">That's it — same wiring you already have. We're just changing what makes it buzz.</p>
      </Step>
      <Step n={2} title="Flash the Arduino sketch">
        <p>Open the Arduino IDE and pick the version that matches your board.</p>
        <h4 className="font-bold mt-4 mb-2 text-sm">Option A · ESP8266 / ESP32 (Wi-Fi, standalone)</h4>
        <Pre>{`#include <ESP8266WiFi.h>      // ESP32: #include <WiFi.h>
#include <ESP8266HTTPClient.h> // ESP32: #include <HTTPClient.h>
const char* WIFI_SSID = "YOUR_WIFI";
const char* WIFI_PASS = "YOUR_PASSWORD";
const char* VUKA_URL  = "https://YOUR-VUKA-DOMAIN/api/alerts.json";
const int BUZZER = 8;
int lastCount = 0;
void buzz(int ms) {
  digitalWrite(BUZZER, HIGH);
  delay(ms);
  digitalWrite(BUZZER, LOW);
}
void setup() {
  pinMode(BUZZER, OUTPUT);
  Serial.begin(115200);
  WiFi.begin(WIFI_SSID, WIFI_PASS);
  while (WiFi.status() != WL_CONNECTED) { delay(500); Serial.print("."); }
  Serial.println("\\nWi-Fi connected");
}
void loop() {
  WiFiClient client;
  HTTPClient http;
  http.begin(client, VUKA_URL);
  int code = http.GET();
  if (code == 200) {
    String body = http.getString();
    // very small parse: look for "newCount":N
    int idx = body.indexOf("\\"newCount\\":");
    if (idx >= 0) {
      int count = body.substring(idx + 11).toInt();
      if (count > lastCount) buzz(500);
      lastCount = count;
    }
  }
  http.end();
  delay(30000); // poll every 30s
}`}</Pre>
        <h4 className="font-bold mt-6 mb-2 text-sm">Option B · Arduino Uno (no Wi-Fi — use Serial bridge)</h4>
        <p className="text-sm">Uno listens on Serial. A small Node script on your laptop fetches VUKA and writes <Code>1\n</Code> when there's a new match.</p>
        <Pre>{`const int BUZZER = 8;
void setup() {
  pinMode(BUZZER, OUTPUT);
  Serial.begin(9600);
}
void loop() {
  if (Serial.available()) {
    char c = Serial.read();
    if (c == '1') {
      digitalWrite(BUZZER, HIGH);
      delay(500);
      digitalWrite(BUZZER, LOW);
    }
  }
}`}</Pre>
        <p className="text-sm mt-3">Bridge script (Node, run on your laptop):</p>
        <Pre>{`// npm i serialport node-fetch
import { SerialPort } from "serialport";
import fetch from "node-fetch";
const port = new SerialPort({ path: "/dev/ttyUSB0", baudRate: 9600 });
let last = 0;
setInterval(async () => {
  const r = await fetch("https://YOUR-VUKA-DOMAIN/api/alerts.json");
  const { newCount } = await r.json();
  if (newCount > last) port.write("1\\n");
  last = newCount;
}, 30000);`}</Pre>
      </Step>
      <Step n={3} title="Add the /api/alerts.json endpoint to VUKA">
        <p>The Arduino just needs a tiny JSON payload. Add a server route:</p>
        <Pre>{`// src/routes/api/alerts.json.ts
import { createFileRoute } from "@tanstack/react-router";
export const Route = createFileRoute("/api/alerts/json")({
  server: {
    handlers: {
      GET: async () => {
        // TODO: replace with a real query (Lovable Cloud)
        const newCount = Math.floor(Date.now() / 60000) % 7;
        return new Response(
          JSON.stringify({ newCount, ts: Date.now() }),
          { headers: { "Content-Type": "application/json" } }
        );
      },
    },
  },
});`}</Pre>
        <p className="text-xs text-muted-foreground mt-2">Once you turn on Lovable Cloud, swap the stub for a real query that counts opportunities created since the user's last visit.</p>
      </Step>
      <Step n={4} title="Test the loop">
        <ol className="list-decimal pl-5 space-y-1 text-sm">
          <li>Upload the sketch. Open Serial Monitor — you should see "Wi-Fi connected" (Option A) or the bridge script logs (Option B).</li>
          <li>Open VUKA in the browser and post a new opportunity (or bump <Code>newCount</Code> in the stub).</li>
          <li>Within ~30 seconds the buzzer beeps for half a second. 🎉</li>
        </ol>
      </Step>
      <Step n={5} title="Make it yours">
        <ul className="list-disc pl-5 space-y-1 text-sm">
          <li>Different beep patterns per type: 1 beep = job, 2 = internship, 3 = learnership.</li>
          <li>Add an LED next to the buzzer that stays on until you press a button to acknowledge.</li>
          <li>Filter the JSON by township so you only buzz for opportunities near you.</li>
        </ul>
      </Step>
      <div className="my-10 p-5 bg-burnt-light/30 border border-burnt-light rounded-2xl text-sm">
        <b>Heads-up:</b> the polling endpoint shown here is a stub. To make it count real new opportunities per user, enable Lovable Cloud — then we can store opportunities, the user's last-seen timestamp, and return an accurate <Code>newCount</Code>.
      </div>
    </AppShell>
  );
}
function Card({ title, children }: { title: string; children: React.ReactNode }) {
  return (
    <div className="bg-card border border-burnt-light/60 rounded-2xl p-5">
      <h3 className="font-display font-bold text-lg mb-2">{title}</h3>
      {children}
    </div>
  );
}
function Step({ n, title, children }: { n: number; title: string; children: React.ReactNode }) {
  return (
    <section className="mt-10">
      <div className="flex items-center gap-3 mb-3">
        <div className="size-9 rounded-xl bg-burnt-dark text-burnt-light grid place-items-center font-display font-extrabold">{n}</div>
        <h2 className="font-display text-xl sm:text-2xl font-extrabold">{title}</h2>
      </div>
      <div className="pl-12 text-foreground/90">{children}</div>
    </section>
  );
}
function Code({ children }: { children: React.ReactNode }) {
  return <code className="px-1.5 py-0.5 rounded bg-burnt-light/40 text-burnt-dark text-[0.85em] font-mono">{children}</code>;
}
function Pre({ children }: { children: string }) {
  return (
    <pre className="mt-3 bg-burnt-dark text-burnt-light rounded-xl p-4 text-xs overflow-x-auto font-mono leading-relaxed">
      <code>{children}</code>
    </pre>
  );
}

Created
centers.tsx
import { createFileRoute } from "@tanstack/react-router";
import { AppShell } from "@/components/AppShell";
import { centers, courses } from "@/lib/data";
export const Route = createFileRoute("/centers")({
  head: () => ({
    meta: [
      { title: "Skills Centers & Short Courses · VUKA" },
      { name: "description", content: "Find a township skills development center near you and enroll in short, practical courses while you wait for an opportunity response." },
      { property: "og:title", content: "Skills Centers · VUKA" },
      { property: "og:description", content: "Practical short courses run by local township skills hubs." },
    ],
  }),
  component: CentersPage,
});
function CentersPage() {
  return (
    <AppShell>
      <h1 className="font-display text-3xl sm:text-4xl font-extrabold">Skills Centers</h1>
      <p className="text-muted-foreground mt-1 max-w-xl">
        While you wait for a response from an employer, sharpen your hands at a center close to home. All courses include real practicals.
      </p>
      <section className="mt-8">
        <h2 className="font-display text-xl font-extrabold mb-4">Short courses on offer</h2>
        <div className="grid sm:grid-cols-2 lg:grid-cols-3 gap-4">
          {courses.map(c => (
            <article key={c.id} className="bg-card border border-burnt-light/60 rounded-2xl p-5">
              <div className="size-10 rounded-xl bg-burnt-light grid place-items-center text-burnt-dark font-display font-extrabold mb-3">
                {c.title.charAt(0)}
              </div>
              <h3 className="font-display font-bold text-lg leading-tight">{c.title}</h3>
              <p className="text-xs text-burnt-primary font-bold uppercase tracking-wider mt-1">{c.duration}</p>
              <p className="text-sm text-muted-foreground mt-2">{c.center}</p>
              <p className="text-sm mt-3 text-foreground/80">{c.practical}</p>
            </article>
          ))}
        </div>
      </section>
      <section className="mt-12">
        <h2 className="font-display text-xl font-extrabold mb-4">Centers near you</h2>
        <div className="grid sm:grid-cols-2 gap-4">
          {centers.map(c => (
            <article key={c.id} className="bg-burnt-dark text-burnt-light rounded-2xl p-5">
              <h3 className="font-display font-bold text-lg">{c.name}</h3>
              <p className="text-burnt-light/70 text-sm">{c.township}</p>
              <div className="flex flex-wrap gap-2 mt-3">
                {c.focus.map(f => (
                  <span key={f} className="text-[11px] px-2 py-1 rounded bg-burnt-light/15 font-bold uppercase tracking-wider">{f}</span>
                ))}
              </div>
              <p className="text-xs text-burnt-light/70 mt-4">📞 {c.contact}</p>
            </article>
          ))}
        </div>
      </section>
    </AppShell>
  );
}

Created
opportunities.tsx
import { createFileRoute } from "@tanstack/react-router";
import { useState } from "react";
import { AppShell } from "@/components/AppShell";
import { OpportunityCard } from "@/components/OpportunityCard";
import { opportunities, type OppType } from "@/lib/data";
export const Route = createFileRoute("/opportunities")({
  head: () => ({
    meta: [
      { title: "Opportunities — Learnerships, Internships & Jobs · VUKA" },
      { name: "description", content: "Browse all live learnerships, internships and entry-level jobs for unemployed youth in South African townships." },
      { property: "og:title", content: "Opportunities · VUKA" },
      { property: "og:description", content: "Filter learnerships, internships and jobs in SA townships." },
    ],
  }),
  component: OpportunitiesPage,
});
function OpportunitiesPage() {
  const [filter, setFilter] = useState<OppType | "all">("all");
  const [query, setQuery] = useState("");
  const filtered = opportunities.filter(o => {
    if (filter !== "all" && o.type !== filter) return false;
    if (query && !`${o.title} ${o.company} ${o.location}`.toLowerCase().includes(query.toLowerCase())) return false;
    return true;
  });
  const tabs: Array<{ id: OppType | "all"; label: string }> = [
    { id: "all", label: "All" },
    { id: "learnership", label: "Learnerships" },
    { id: "internship", label: "Internships" },
    { id: "job", label: "Jobs" },
  ];
  return (
    <AppShell>
      <h1 className="font-display text-3xl sm:text-4xl font-extrabold">Opportunities</h1>
      <p className="text-muted-foreground mt-1">Updated daily by partner employers and skills hubs.</p>
      <div className="mt-6 flex flex-col sm:flex-row gap-3">
        <input
          value={query}
          onChange={e => setQuery(e.target.value)}
          placeholder="Search role, company or township..."
          className="flex-1 bg-card border border-burnt-light/60 rounded-xl px-4 py-3 text-sm focus:border-burnt-mid outline-none"
        />
        <div className="flex gap-2 flex-wrap">
          {tabs.map(t => (
            <button
              key={t.id}
              onClick={() => setFilter(t.id)}
              className={`px-4 py-2 rounded-xl text-xs font-bold uppercase tracking-wider transition-colors ${
                filter === t.id ? "bg-burnt-dark text-burnt-light" : "bg-card border border-burnt-light/60 text-burnt-dark hover:bg-burnt-light/30"
              }`}
            >
              {t.label}
            </button>
          ))}
        </div>
      </div>
      <div className="mt-6 grid sm:grid-cols-2 lg:grid-cols-3 gap-4">
        {filtered.map(o => <OpportunityCard key={o.id} o={o} />)}
        {filtered.length === 0 && (
          <p className="col-span-full text-center text-muted-foreground py-12">No opportunities match — try a different filter.</p>
        )}
      </div>
    </AppShell>
  );
}

Modified
routeTree.gen.ts
import { Route as rootRouteImport } from './routes/__root'
import { Route as OpportunitiesRouteImport } from './routes/opportunities'
import { Route as CentersRouteImport } from './routes/centers'
import { Route as ArduinoRouteImport } from './routes/arduino'
import { Route as IndexRouteImport } from './routes/index'
const OpportunitiesRoute = OpportunitiesRouteImport.update({
  id: '/opportunities',
  path: '/opportunities',
  getParentRoute: () => rootRouteImport,
} as any)
const CentersRoute = CentersRouteImport.update({
  id: '/centers',
  path: '/centers',
  getParentRoute: () => rootRouteImport,
} as any)
const ArduinoRoute = ArduinoRouteImport.update({
  id: '/arduino',
  path: '/arduino',
  getParentRoute: () => rootRouteImport,
} as any)
const IndexRoute = IndexRouteImport.update({
  id: '/',
export interface FileRoutesByFullPath {
  '/': typeof IndexRoute
  '/arduino': typeof ArduinoRoute
  '/centers': typeof CentersRoute
  '/opportunities': typeof OpportunitiesRoute
}
export interface FileRoutesByTo {
  '/': typeof IndexRoute
  '/arduino': typeof ArduinoRoute
  '/centers': typeof CentersRoute
  '/opportunities': typeof OpportunitiesRoute
}
export interface FileRoutesById {
  __root__: typeof rootRouteImport
  '/': typeof IndexRoute
  '/arduino': typeof ArduinoRoute
  '/centers': typeof CentersRoute
  '/opportunities': typeof OpportunitiesRoute
}
export interface FileRouteTypes {
  fileRoutesByFullPath: FileRoutesByFullPath
  fullPaths: '/'
  fullPaths: '/' | '/arduino' | '/centers' | '/opportunities'
  fileRoutesByTo: FileRoutesByTo
  to: '/'
  id: '__root__' | '/'
  to: '/' | '/arduino' | '/centers' | '/opportunities'
  id: '__root__' | '/' | '/arduino' | '/centers' | '/opportunities'
  fileRoutesById: FileRoutesById
}
export interface RootRouteChildren {
  IndexRoute: typeof IndexRoute
  ArduinoRoute: typeof ArduinoRoute
  CentersRoute: typeof CentersRoute
  OpportunitiesRoute: typeof OpportunitiesRoute
}
declare module '@tanstack/react-router' {
  interface FileRoutesByPath {
    '/opportunities': {
      id: '/opportunities'
      path: '/opportunities'
      fullPath: '/opportunities'
      preLoaderRoute: typeof OpportunitiesRouteImport
      parentRoute: typeof rootRouteImport
    }
    '/centers': {
      id: '/centers'
      path: '/centers'
      fullPath: '/centers'
      preLoaderRoute: typeof CentersRouteImport
      parentRoute: typeof rootRouteImport
    }
    '/arduino': {
      id: '/arduino'
      path: '/arduino'
      fullPath: '/arduino'
      preLoaderRoute: typeof ArduinoRouteImport
      parentRoute: typeof rootRouteImport
    }
    '/': {
      id: '/'
const rootRouteChildren: RootRouteChildren = {
  IndexRoute: IndexRoute,
  ArduinoRoute: ArduinoRoute,
  CentersRoute: CentersRoute,
  OpportunitiesRoute: OpportunitiesRoute,
}
export const routeTree = rootRouteImport
  ._addFileChildren(rootRouteChildren)
  ._addFileTypes<FileRouteTypes>()
import type { getRouter } from './router.tsx'
import type { startInstance } from './start.ts'
declare module '@tanstack/react-start' {
  interface Register {
    ssr: true
    router: Awaited<ReturnType<typeof getRouter>>
    config: Awaited<ReturnType<typeof startInstance.getOptions>>
  }
}

Modified
__root.tsx
      { charSet: "utf-8" },
      { name: "viewport", content: "width=device-width, initial-scale=1" },
      { title: "Lovable App" },
      { name: "description", content: "Lovable Generated Project" },
      { name: "author", content: "Lovable" },
      { property: "og:title", content: "Lovable App" },
      { property: "og:description", content: "Lovable Generated Project" },
      { title: "VUKA — Township Youth Opportunities" },
      { name: "description", content: "Learnerships, internships, jobs and short skills courses for unemployed youth across South African townships." },
      { name: "author", content: "VUKA" },
      { property: "og:title", content: "VUKA — Township Youth Opportunities" },
      { property: "og:description", content: "Learnerships, internships, jobs and practical short courses for SA township youth." },
      { property: "og:type", content: "website" },
      { name: "twitter:card", content: "summary" },
      { name: "twitter:site", content: "@Lovable" },
      { name: "twitter:card", content: "summary_large_image" },
    ],
    links: [
      {
        rel: "stylesheet",
        href: appCss,
      },
      { rel: "stylesheet", href: appCss },
      { rel: "preconnect", href: "https://fonts.googleapis.com" },
      { rel: "preconnect", href: "https://fonts.gstatic.com", crossOrigin: "anonymous" },
      { rel: "stylesheet", href: "https://fonts.googleapis.com/css2?family=Sora:wght@600;700;800&family=Manrope:wght@400;500;600;700&display=swap" },
    ],
  }),

Modified
src/routes/index.tsx
import { createFileRoute } from "@tanstack/react-router";
import { createFileRoute, Link } from "@tanstack/react-router";
import { AppShell } from "@/components/AppShell";
import { OpportunityCard } from "@/components/OpportunityCard";
import { opportunities, courses, centers } from "@/lib/data";
import heroImg from "@/assets/hero-workshop.jpg";
export const Route = createFileRoute("/")({
  head: () => ({
    meta: [
      { title: "Your App" },
      { name: "description", content: "Replace this with a one-sentence description of your app." },
      { property: "og:title", content: "Your App" },
      { property: "og:description", content: "Replace this with a one-sentence description of your app." },
      { title: "VUKA — Jobs, Learnerships & Skills for Township Youth" },
      { name: "description", content: "Browse learnerships, internships and jobs in South African townships. While you wait, learn a practical skill at a local skills development center." },
      { property: "og:title", content: "VUKA — Township Youth Opportunities" },
      { property: "og:description", content: "Learnerships, internships, jobs and practical short courses for unemployed youth in SA townships." },
    ],
  }),
  component: Index,
  component: Home,
});
// IMPORTANT: Replace this placeholder. See ./README.md for routing conventions.
function Index() {
function Home() {
  const featured = opportunities[0];
  const stats = {
    learnerships: opportunities.filter(o => o.type === "learnership").length,
    internships: opportunities.filter(o => o.type === "internship").length,
    jobs: opportunities.filter(o => o.type === "job").length,
    centers: centers.length,
  };
  const course = courses[5]; // Arduino course of the week
  return (
    <div
      className="flex min-h-screen items-center justify-center"
      style={{ backgroundColor: "#fcfbf8" }}
    >
      <img
        data-lovable-blank-page-placeholder="REMOVE_THIS"
        src="https://cdn.gpteng.co/blank-app-v1.svg"
        alt="Your app will live here!"
      />
    <AppShell>
      {/* Hero */}
      <section className="mb-6">
        <h1 className="font-display text-4xl sm:text-5xl font-extrabold leading-[1.05] text-balance max-w-2xl">
          Your next <span className="text-burnt-primary">big move</span> starts in the kasi.
        </h1>
        <p className="mt-3 text-muted-foreground max-w-xl">
          Learnerships, internships and jobs across South African townships — plus practical short courses to keep you sharp while you wait.
        </p>
      </section>
      {/* Bento grid */}
      <section className="grid grid-cols-4 gap-3 mb-10">
        {/* Featured */}
        <div className="col-span-4 lg:col-span-3 rounded-3xl overflow-hidden bg-burnt-dark text-burnt-light relative shadow-xl">
          <img src={heroImg} alt="Youth at a township skills workshop" className="absolute inset-0 w-full h-full object-cover opacity-30" />
          <div className="relative z-10 p-7 sm:p-10 max-w-lg">
            <span className="inline-block px-2 py-1 bg-burnt-mid text-white text-[10px] font-bold rounded uppercase tracking-wider">Featured Learnership</span>
            <h2 className="font-display text-2xl sm:text-3xl font-extrabold mt-3 leading-tight">{featured.title}</h2>
            <p className="text-burnt-light/80 mt-2 text-sm">{featured.company} · {featured.location}</p>
            <p className="text-burnt-light/90 mt-4 text-sm">{featured.summary}</p>
            <Link to="/opportunities" className="inline-block mt-6 px-5 py-3 bg-burnt-light text-burnt-dark font-bold rounded-xl text-sm hover:bg-cream transition-colors">
              View all opportunities →
            </Link>
          </div>
        </div>
        {/* Alerts */}
        <div className="col-span-2 lg:col-span-1 bg-card border border-burnt-light/60 rounded-3xl p-5 flex flex-col justify-between">
          <div className="flex justify-between items-start">
            <span className="text-[10px] font-bold text-burnt-primary uppercase tracking-wider">Buzzer alerts</span>
            <span className="size-2 bg-burnt-mid rounded-full animate-pulse" />
          </div>
          <div>
            <p className="font-display font-extrabold text-4xl text-burnt-dark">{stats.learnerships + stats.internships}</p>
            <p className="text-xs text-muted-foreground mt-1 leading-snug">New matches today. Pair with Arduino buzzer for live alerts.</p>
          </div>
          <Link to="/arduino" className="text-xs font-bold text-burnt-primary">Set it up →</Link>
        </div>
        {/* Stat tiles */}
        <StatTile label="Learnerships" value={stats.learnerships} tone="dark" />
        <StatTile label="Internships" value={stats.internships} tone="mid" />
        <StatTile label="Jobs" value={stats.jobs} tone="light" />
        <StatTile label="Skills Centers" value={stats.centers} tone="muted" />
        {/* Course of the week */}
        <div className="col-span-4 lg:col-span-2 bg-burnt-mid/15 border-2 border-dashed border-burnt-mid/40 rounded-3xl p-6">
          <span className="text-[10px] font-bold text-burnt-primary uppercase tracking-wider">Course of the week</span>
          <h3 className="font-display font-extrabold text-xl mt-2">{course.title}</h3>
          <p className="text-sm text-muted-foreground mt-1">{course.center} · {course.duration}</p>
          <p className="text-sm mt-3">{course.practical}</p>
          <Link to="/centers" className="inline-block mt-4 text-sm font-bold text-burnt-primary">Browse all courses →</Link>
        </div>
        {/* CTA Arduino */}
        <div className="col-span-4 lg:col-span-2 bg-burnt-dark text-burnt-light rounded-3xl p-6 flex flex-col justify-between">
          <div>
            <span className="text-[10px] font-bold text-burnt-light/70 uppercase tracking-wider">Maker Mode</span>
            <h3 className="font-display font-extrabold text-xl mt-2">Hook your Arduino buzzer to VUKA</h3>
            <p className="text-sm text-burnt-light/80 mt-2">Get a physical buzz on your bench every time a new opportunity matches you.</p>
          </div>
          <Link to="/arduino" className="mt-4 inline-block bg-burnt-light text-burnt-dark px-4 py-2 rounded-xl text-xs font-bold w-fit">
            Open step-by-step guide
          </Link>
        </div>
      </section>
      {/* Recent opportunities */}
      <section className="mb-12">
        <div className="flex items-end justify-between mb-4">
          <h2 className="font-display text-2xl font-extrabold">Latest opportunities</h2>
          <Link to="/opportunities" className="text-sm font-bold text-burnt-primary">See all →</Link>
        </div>
        <div className="grid sm:grid-cols-2 lg:grid-cols-3 gap-4">
          {opportunities.slice(0, 6).map(o => <OpportunityCard key={o.id} o={o} />)}
        </div>
      </section>
    </AppShell>
  );
}
function StatTile({ label, value, tone }: { label: string; value: number; tone: "dark" | "mid" | "light" | "muted" }) {
  const toneClass = {
    dark: "bg-burnt-dark text-burnt-light",
    mid: "bg-burnt-mid text-white",
    light: "bg-burnt-light text-burnt-dark",
    muted: "bg-card border border-burnt-light/60 text-burnt-dark",
  }[tone];
  return (
    <div className={`col-span-2 lg:col-span-1 rounded-3xl p-5 ${toneClass}`}>
      <p className="font-display font-extrabold text-3xl">{value}</p>
      <p className="text-xs font-bold uppercase tracking-wider mt-1 opacity-80">{label}</p>
    </div>
  );

Modified
src/styles.css
@custom-variant dark (&:is(.dark *));
/*
 * Design system definition.
 *
 * The @theme inline block maps CSS custom properties to Tailwind utility
 * classes (e.g. --color-primary -> bg-primary, text-primary).
 *
 * The :root and .dark blocks define the actual color values using oklch.
 * All colors MUST use oklch format.
 *
 * To add a new semantic color:
 * 1. Add the variable to :root (light value) and .dark (dark value)
 * 2. Register it in @theme inline as --color-<name>: var(--<name>)
 */
@theme inline {
  --font-display: "Sora", ui-sans-serif, system-ui, sans-serif;
  --font-body: "Manrope", ui-sans-serif, system-ui, sans-serif;
  --font-sans: "Manrope", ui-sans-serif, system-ui, sans-serif;
  --radius-sm: calc(var(--radius) - 4px);
  --radius-md: calc(var(--radius) - 2px);
  --radius-2xl: calc(var(--radius) + 8px);
  --radius-3xl: calc(var(--radius) + 12px);
  --radius-4xl: calc(var(--radius) + 16px);
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-input: var(--input);
  --color-ring: var(--ring);
  --color-ring-offset-background: var(--background);
  --color-chart-1: var(--chart-1);
  --color-chart-2: var(--chart-2);
  --color-chart-3: var(--chart-3);
  --color-chart-4: var(--chart-4);
  --color-chart-5: var(--chart-5);
  --color-sidebar: var(--sidebar);
  --color-sidebar-foreground: var(--sidebar-foreground);
  --color-sidebar-primary: var(--sidebar-primary);
  --color-sidebar-primary-foreground: var(--sidebar-primary-foreground);
  --color-sidebar-accent: var(--sidebar-accent);
  --color-sidebar-accent-foreground: var(--sidebar-accent-foreground);
  --color-sidebar-border: var(--sidebar-border);
  --color-sidebar-ring: var(--sidebar-ring);
  /* Burnt Sienna brand tokens */
  --color-burnt-dark: var(--burnt-dark);
  --color-burnt-primary: var(--burnt-primary);
  --color-burnt-mid: var(--burnt-mid);
  --color-burnt-light: var(--burnt-light);
  --color-cream: var(--cream);
}
:root {
  --radius: 0.625rem;
  --background: oklch(1 0 0);
  --foreground: oklch(0.129 0.042 264.695);
  --card: oklch(1 0 0);
  --card-foreground: oklch(0.129 0.042 264.695);
  --popover: oklch(1 0 0);
  --popover-foreground: oklch(0.129 0.042 264.695);
  --primary: oklch(0.208 0.042 265.755);
  --primary-foreground: oklch(0.984 0.003 247.858);
  --secondary: oklch(0.968 0.007 247.896);
  --secondary-foreground: oklch(0.208 0.042 265.755);
  --muted: oklch(0.968 0.007 247.896);
  --muted-foreground: oklch(0.554 0.046 257.417);
  --accent: oklch(0.968 0.007 247.896);
  --accent-foreground: oklch(0.208 0.042 265.755);
  --destructive: oklch(0.577 0.245 27.325);
  --destructive-foreground: oklch(0.984 0.003 247.858);
  --border: oklch(0.929 0.013 255.508);
  --input: oklch(0.929 0.013 255.508);
  --ring: oklch(0.704 0.04 256.788);
  --chart-1: oklch(0.646 0.222 41.116);
  --chart-2: oklch(0.6 0.118 184.704);
  --chart-3: oklch(0.398 0.07 227.392);
  --chart-4: oklch(0.828 0.189 84.429);
  --chart-5: oklch(0.769 0.188 70.08);
  --sidebar: oklch(0.984 0.003 247.858);
  --sidebar-foreground: oklch(0.129 0.042 264.695);
  --sidebar-primary: oklch(0.208 0.042 265.755);
  --sidebar-primary-foreground: oklch(0.984 0.003 247.858);
  --sidebar-accent: oklch(0.968 0.007 247.896);
  --sidebar-accent-foreground: oklch(0.208 0.042 265.755);
  --sidebar-border: oklch(0.929 0.013 255.508);
  --sidebar-ring: oklch(0.704 0.04 256.788);
}
  --radius: 0.875rem;
.dark {
  --background: oklch(0.129 0.042 264.695);
  --foreground: oklch(0.984 0.003 247.858);
  --card: oklch(0.208 0.042 265.755);
  --card-foreground: oklch(0.984 0.003 247.858);
  --popover: oklch(0.208 0.042 265.755);
  --popover-foreground: oklch(0.984 0.003 247.858);
  --primary: oklch(0.929 0.013 255.508);
  --primary-foreground: oklch(0.208 0.042 265.755);
  --secondary: oklch(0.279 0.041 260.031);
  --secondary-foreground: oklch(0.984 0.003 247.858);
  --muted: oklch(0.279 0.041 260.031);
  --muted-foreground: oklch(0.704 0.04 256.788);
  --accent: oklch(0.279 0.041 260.031);
  --accent-foreground: oklch(0.984 0.003 247.858);
  --destructive: oklch(0.704 0.191 22.216);
  --destructive-foreground: oklch(0.984 0.003 247.858);
  --border: oklch(1 0 0 / 10%);
  --input: oklch(1 0 0 / 15%);
  --ring: oklch(0.551 0.027 264.364);
  --chart-1: oklch(0.488 0.243 264.376);
  --chart-2: oklch(0.696 0.17 162.48);
  --chart-3: oklch(0.769 0.188 70.08);
  --chart-4: oklch(0.627 0.265 303.9);
  --chart-5: oklch(0.645 0.246 16.439);
  --sidebar: oklch(0.208 0.042 265.755);
  --sidebar-foreground: oklch(0.984 0.003 247.858);
  --sidebar-primary: oklch(0.488 0.243 264.376);
  --sidebar-primary-foreground: oklch(0.984 0.003 247.858);
  --sidebar-accent: oklch(0.279 0.041 260.031);
  --sidebar-accent-foreground: oklch(0.984 0.003 247.858);
  --sidebar-border: oklch(1 0 0 / 10%);
  --sidebar-ring: oklch(0.551 0.027 264.364);
  /* Burnt Sienna palette in oklch */
  --burnt-dark: oklch(0.36 0.07 40);     /* #6b3a2a */
  --burnt-primary: oklch(0.5 0.115 47);  /* #a0522d */
  --burnt-mid: oklch(0.63 0.13 55);      /* #cd7f32 */
  --burnt-light: oklch(0.82 0.09 78);    /* #e8c07a */
  --cream: oklch(0.98 0.012 80);
  --background: oklch(0.985 0.008 80);
  --foreground: oklch(0.26 0.04 40);
  --card: oklch(1 0 0);
  --card-foreground: oklch(0.26 0.04 40);
  --popover: oklch(1 0 0);
  --popover-foreground: oklch(0.26 0.04 40);
  --primary: var(--burnt-dark);
  --primary-foreground: oklch(0.98 0.012 80);
  --secondary: oklch(0.94 0.025 75);
  --secondary-foreground: var(--burnt-dark);
  --muted: oklch(0.95 0.018 75);
  --muted-foreground: oklch(0.5 0.04 50);
  --accent: var(--burnt-mid);
  --accent-foreground: oklch(0.98 0.012 80);
  --destructive: oklch(0.55 0.22 27);
  --destructive-foreground: oklch(0.98 0.012 80);
  --border: oklch(0.9 0.025 75);
  --input: oklch(0.92 0.025 75);
  --ring: var(--burnt-mid);
}
@layer base {
  * {
    border-color: var(--color-border);
  }
  body {
  * { border-color: var(--color-border); }
  html, body {
    background-color: var(--color-background);
    color: var(--color-foreground);
    font-family: var(--font-body);
    -webkit-font-smoothing: antialiased;
  }
  h1, h2, h3, h4, h5, h6 { font-family: var(--font-display); letter-spacing: -0.01em; }
}
