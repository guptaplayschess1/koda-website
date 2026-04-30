# Koda Property Group — Website Build Tasks

## Project Location
`real-estate-crm/website/` — separate folder, separate git repo.
Do not touch anything outside the website/ folder.

## Deployment
- Host: Netlify (free)
- Domain: kodapropertygroup.com
- Deploy method: drag and drop OR Netlify CLI (`netlify deploy --prod`)
- After every session: deploy to Netlify and verify live site looks correct

## The Mission
Content-first real estate investor site. Positioning:
"We help Florida property owners find the fastest, simplest exit —
whatever their situation."

Advisor first, buyer second. Every page answers a question a motivated
seller is actually Googling. No generic "we buy ugly houses" language.
No hollow sales pitch. Real information that builds trust before the call.

## Design System (apply consistently across all pages)
```
Fonts:
  Display: Playfair Display (elegant, editorial, trustworthy)
  Body: DM Sans (clean, readable at length)

Colors:
  --cream: #f7f4ef        (page background — warm, not harsh white)
  --black: #111111        (headlines)
  --text: #3a3a3a         (body text)
  --red: #c8392b          (accents, CTAs, brand)
  --grey: #888888         (secondary text)
  --grey-light: #eeebe4   (dividers, subtle backgrounds)
  --green: #2d6a4f        (trust signals, positive outcomes)

Layout:
  Max content width: 780px (blog/article pages)
  Max site width: 1140px (homepage, market pages)
  Section padding: 96px vertical, 48px horizontal
  Mobile padding: 64px vertical, 24px horizontal

Components:
  - Nav: fixed, cream background, logo left, links right
  - CTA button: red, no border-radius (sharp corners = decisive)
  - Section labels: 11px, red, letter-spacing 0.18em, uppercase
  - Cards: cream background, 1px border rgba(0,0,0,0.1), no drop shadow
  - Blog post previews: title + 2-line excerpt + read time + date

Rules:
  - No stock photo people (use property photos or abstract textures)
  - No purple, no gradients, no rounded everything
  - Every page has exactly one primary CTA above the fold
  - Every page links to the contact page
  - Privacy policy and SMS disclosure on every page footer
```

## File Structure
```
website/
  index.html
  about.html
  how-it-works.html
  contact.html
  privacy-policy.html
  terms.html
  markets/
    charlotte-county.html
    sarasota-county.html
    lee-county.html
    polk-county.html
    pasco-county.html
    seminole-county.html
  deals/
    placida-golf-lot.html
    port-charlotte-waterfront.html
  blog/
    florida-foreclosure-timeline.html
    inherited-property-florida.html
    sell-vacant-lot-florida.html
    behind-on-mortgage-florida.html
    fixer-upper-florida.html
    cash-sale-timeline-florida.html
  css/
    style.css             ← shared design system
    article.css           ← blog/long-form specific styles
  js/
    main.js               ← nav, scroll behavior, minimal interactions
  images/
    (placeholder — add real photos later)
  sitemap.xml             ← generated in Session 7
```

---

## SESSION 1 — Foundation + Homepage + Deploy  ← START HERE

**Goal:** Live site on kodapropertygroup.com by end of session.

### 1A — Project Setup
```
mkdir -p website/{markets,deals,blog,css,js,images}
cd website
git init
echo "node_modules/" > .gitignore
```

### 1B — Shared CSS (`css/style.css`)
Full design system as variables + base styles:
- CSS custom properties for all colors, fonts, spacing
- Reset (box-sizing, margins, font smoothing)
- Typography scale (h1-h4, body, small, label)
- Nav component (fixed, cream, logo left, links right, mobile hamburger)
- Button components (primary = red, secondary = outline)
- Footer component (3-column: logo+tagline | nav links | legal)
- SMS disclosure bar (thin red bar at very top with opt-out language)
- Utility classes (.section, .section-inner, .section-label, .fade-in)
- Responsive breakpoints (768px mobile, 1024px tablet)

### 1C — Homepage (`index.html`)
Not a brochure. Answers the question: "I need to sell my property fast
in Florida — what are my options and who can help?"

Sections in order:

**SMS Bar (top):**
"By texting us, you consent to receive SMS messages. Reply STOP to
opt out. Msg & data rates may apply."

**Nav:**
Logo (KODA PROPERTY GROUP) | How It Works | Markets | Blog | Contact Us

**Hero:**
Headline: "There's a Faster Way to Sell Your Florida Property"
Sub: "No repairs. No commissions. No waiting. We buy directly from
owners across Florida — and we close on your schedule."
CTA: [Get a Cash Offer] → /contact.html
Secondary line: "Or call/text: [PHONE]"
No hero image. Clean typography on cream background.
Thin red left-border accent on the headline block.

**Situations We Help With (the content hook):**
Section label: "WHO WE HELP"
Headline: "Every Property Has a Story"
Six situation cards, each one sentence of empathy + one sentence of
what we can do:
- Facing foreclosure or behind on payments
- Inherited a property you don't want to maintain
- Vacant land sitting unused and costing you money
- Divorce or life change requiring a fast sale
- Property needs too many repairs to list traditionally
- Moving and need to close before your deadline

Each card links to a relevant blog post (internal link).

**How It Works (abbreviated — links to full page):**
3 steps: Contact us → Receive an offer → Close on your date
[See the full process →] → /how-it-works.html

**Markets:**
Section label: "WHERE WE BUY"
Headline: "Serving Sellers Across Florida"
County pills/chips linking to each market page:
Charlotte County · Sarasota County · Lee County · Polk County ·
Pasco County · Seminole County · "and surrounding areas"

**Why Work With Us (trust signals):**
4 items in a 2x2 grid:
- No fees or commissions (vs. 5-6% with an agent)
- As-is purchases (no repairs, no cleaning)
- Cash offers (no financing contingencies)
- Flexible closing (your timeline, not ours)

**Recent Deals (social proof stub — expands in Session 4):**
Headline: "Properties We've Helped"
2 deal cards (Port Charlotte, Placida) — address, situation, outcome,
days to close. Keep it factual and simple.

**Footer:**
Logo + tagline | Nav links | Legal links
SMS disclosure paragraph
© 2026 Koda Property Group LLC · Colorado LLC · All rights reserved

### 1D — Contact Page (`contact.html`)
This is the most important conversion page.

Headline: "Tell Us About Your Property"
Sub: "No obligation. No pressure. We'll review your property and
get back to you with options — usually within 24 hours."

Contact form (Netlify Forms — add `netlify` attribute to form tag,
Netlify handles submission and emails Julian automatically):
Fields:
- Your Name (required)
- Phone Number (required)
- Email Address
- Property Address (required)
- What's your situation? (dropdown):
  Facing foreclosure / Behind on payments
  Inherited property
  Vacant land / lot
  Divorce or life change
  Property needs repairs
  Moving / relocation
  Other
- Anything else we should know? (textarea, optional)
- [x] I agree to receive SMS messages from Koda Property Group
  (checkbox, required for SMS consent documentation)
Submit: [Submit — We'll Be in Touch Within 24 Hours]

After submission → thank-you page:
"We received your information. Expect a call or text from us within
24 hours. If it's urgent, call us directly at [PHONE]."

### 1E — Privacy Policy (`privacy-policy.html`)
Full privacy policy including:
- What data is collected (name, phone, email, address, IP)
- How it's used (property evaluation, SMS outreach, no third-party sales)
- SMS consent and opt-out (STOP to unsubscribe)
- Data retention policy
- Contact for data requests

### 1F — Terms of Service (`terms.html`)
Full terms including:
- No obligation language
- Accuracy of property information
- SMS consent terms
- Limitation of liability
- Governing law (Colorado)

### 1G — Deploy
1. Create Netlify account at netlify.com
2. Drag website/ folder onto Netlify deploy zone
3. Set custom domain: kodapropertygroup.com
4. Add nameservers to Namecheap
5. Verify SSL is active
6. Test contact form submission
7. git add -A && git commit -m "Session 1: Foundation + homepage + contact + deploy"

**Acceptance:**
- kodapropertygroup.com loads correctly on desktop and mobile
- Contact form submits and Julian receives an email
- Privacy policy and terms live at their URLs
- Zero broken links
- SMS disclosure visible on every page

---

## SESSION 2 — Market Pages

**Goal:** Six county-specific pages that can rank for local searches.

Each market page follows this template but with unique local content:

**URL:** `/markets/[county-name].html`

**Sections:**
1. Hero: "We Buy Properties in [County], Florida"
   Sub: one sentence about what makes this market distinct
   CTA: [Get a Cash Offer in [County]]

2. About this market (2-3 paragraphs of real local information):
   - County seat, major cities, population context
   - Real estate market conditions (use data from research)
   - What types of properties are common / what you buy there

3. Situations we see in this market (2-3 specific to the county):
   Charlotte County: retirement community, hurricane damage, vacant lots
   Sarasota: rising prices but maintenance costs, snowbird second homes
   Lee County: Cape Coral canal lots, Lehigh Acres distressed inventory
   Polk County: inland affordability, first-time owner distress
   Pasco County: rapid development pressure, long-time homeowners
   Seminole County: foreclosure pipeline, Lis Pendens activity

4. Property types we buy in [County]:
   Specific to what the scraper actually pulls for that county

5. Recent activity (stub — "We're active in [County] right now")

6. FAQ for this county (3-4 questions with real answers):
   e.g., "How does the foreclosure process work in Charlotte County?"
   Link to relevant blog posts for full answers

7. CTA: Contact form or [Get Offer] button

**Research required per county:**
Claude Code should web-search each county before writing its page:
- Population, county seat, major cities
- Current median home prices
- Notable real estate market conditions
- Any county-specific programs or timelines
  (e.g., Seminole County Lis Pendens process)

**Files:** 6 market pages + update homepage market pills with real links

**git commit -m "Session 2: Six county market pages"**

---

## SESSION 3 — How It Works + About

### How It Works (`how-it-works.html`)
This page converts fence-sitters. It needs to answer every objection.

Sections:
1. Hero: "Here's Exactly What Happens When You Contact Us"
   No mystery, no vague promises

2. The 3-step process (detailed version):
   Step 1: You reach out (phone, text, or form)
     - What happens: we look up your property, research comps,
       review condition
     - What we need from you: address, basic situation, your timeline
     - How long: we respond within 24 hours
   Step 2: We present an offer
     - How we calculate it: ARV, condition, carrying costs, we're
       transparent about the math
     - No obligation to accept
     - Offer is all-cash, no financing contingencies
   Step 3: Close on your date
     - You pick the date (as fast as 7 days, or longer if you need it)
     - We work with a title company — fully legal, fully protected
     - You receive funds at closing

3. What we buy:
   Property types (SFH, vacant lots, multi-family, mobile homes
   with land) — with brief explanation of each

4. What we don't buy:
   Be honest — mobile homes in parks, commercial, outside Florida
   This builds credibility

5. Common questions:
   - Do I need to make repairs? No.
   - What if there's a tenant? We handle it.
   - What if I have a mortgage? We pay it off at closing.
   - What if the title has issues? We work through it with title.
   - Is this legal? Yes — assignment contracts are standard in FL.
   - Will you lowball me? Honest answer: we need room to make money,
     but we're transparent about how we calculate the offer.

6. CTA

### About (`about.html`)
Tone: genuine, direct, human. Not corporate.

Sections:
1. Headline: "We're Direct Buyers, Not Middlemen"

2. The story (write in first person, Julian's voice):
   - Why you got into real estate investing
   - What gap you saw in how sellers are served
   - The belief that there should be a faster, simpler option
     for people who need to move a property without the traditional
     process
   - Where you operate and why Florida

3. What "direct buyer" means:
   Explain the difference between a realtor (lists your property,
   takes a commission) and a direct buyer (purchases it outright).
   No jargon, just plain English.

4. The promise:
   - We'll give you a real offer, not a number we'll renegotiate later
   - We'll be straight about whether we can help
   - If we can't help, we'll tell you that too

5. Contact CTA

**Note to Claude Code:** Julian will fill in the personal details of
his story. Write the structure and placeholder text. Mark sections
with [JULIAN TO FILL IN: ...] where personal details are needed.

**git commit -m "Session 3: How It Works + About pages"**

---

## SESSION 4 — Deal Case Studies

**Goal:** Real social proof. Numbers, timelines, outcomes.

### Deal page template (`deals/template`)
Sections:
1. Hero: "[Property Type] in [City] — Closed in [X] Days"
   (factual, specific, no hype)

2. The situation:
   How the seller came to us, what their challenge was,
   what they needed (anonymized — no full name, just first name
   or "the seller")

3. The property:
   Type, location, condition, relevant details

4. The numbers:
   Our offer, asking price (if applicable), assignment fee
   (only include what Julian is comfortable making public)

5. The timeline:
   Day 1: first contact
   Day X: offer presented
   Day X: contract signed
   Day X: closed
   Total: X days from first contact to close

6. The outcome:
   What the seller was able to do (move forward, pay off debt,
   relocate — whatever is true and shareable)

7. CTA: "Have a similar situation? Let's talk."

### Deal 1: Port Charlotte Waterfront Lot (`deals/port-charlotte-waterfront.html`)
Julian fills in the real details from 1289 Underhill Circle.

### Deal 2: Placida Golf-Front Lot (`deals/placida-golf-lot.html`)
Julian fills in the real details from 8 Windward Place once closed.

**Note to Claude Code:** Build the template and page structures.
Mark all specific deal details with [JULIAN TO FILL IN: ...].
The HTML structure, design, and boilerplate copy should be complete.

**git commit -m "Session 4: Deal case study pages"**

---

## SESSION 5 — Blog Posts 1-3

Each blog post is a genuine resource. 800-1200 words. Real information.
Not SEO spam — actually useful to someone in that situation.

### Post 1: `blog/florida-foreclosure-timeline.html`
Title: "Florida Foreclosure Timeline: What Every Homeowner Should Know"
Target search: "florida foreclosure process timeline"
Outline:
- What is foreclosure (brief, plain English)
- Florida is a judicial foreclosure state — what that means
- The stages: missed payment → Lis Pendens filing → lawsuit →
  judgment → auction
- Typical timeline: 6 months to 3+ years
- What you can do at each stage
- How selling before auction can stop the process
- When to contact a lawyer vs. a direct buyer
- CTA: "If you're in the early stages, we may be able to help"

### Post 2: `blog/inherited-property-florida.html`
Title: "Inherited a Property in Florida? Here Are Your Options"
Target search: "inherited property florida what to do"
Outline:
- The probate process in Florida (simplified)
- Your three main options: sell traditionally, rent, sell directly
- The costs of holding an inherited property (taxes, insurance,
  maintenance)
- The emotional component — it's okay to sell
- What happens if there's a mortgage on the property
- How to sell an inherited property without doing repairs
- CTA

### Post 3: `blog/sell-vacant-lot-florida.html`
Title: "How to Sell a Vacant Lot in Florida (Without a Realtor)"
Target search: "sell vacant lot florida"
Outline:
- Why vacant lots are harder to sell traditionally
  (smaller buyer pool, agents less motivated, longer DOM)
- What buyers actually look for in a vacant lot
  (utilities, zoning, access, flood zone)
- How to price it (county appraiser, recent comps, MLS actives)
- The realtor route vs. direct sale comparison
- What carrying costs are eating your return while you wait
- CTA: we buy vacant lots in Charlotte, Sarasota, Lee, Polk,
  Pasco, Seminole counties

**Blog post design spec:**
- Article width: 780px centered
- Large readable body font (DM Sans 18px, 1.8 line height)
- Pull quotes for key points
- Table of contents at top (anchor links)
- Author byline: "Koda Property Group"
- Estimated read time
- Published date
- Related posts at bottom (link to other blog posts)
- CTA box mid-article and at end

**git commit -m "Session 5: Blog posts 1-3"**

---

## SESSION 6 — Blog Posts 4-6

### Post 4: `blog/behind-on-mortgage-florida.html`
Title: "Behind on Your Mortgage in Florida? Here's What to Do"
Target: "behind on mortgage florida options"

### Post 5: `blog/fixer-upper-florida.html`
Title: "Selling a Fixer-Upper in Florida: The Real Cost Breakdown"
Target: "sell fixer upper florida as-is"

### Post 6: `blog/cash-sale-timeline-florida.html`
Title: "How Fast Can You Really Close a Cash Sale in Florida?"
Target: "how fast cash sale close florida"

**git commit -m "Session 6: Blog posts 4-6"**

---

## SESSION 7 — SEO Infrastructure

### Sitemap (`sitemap.xml`)
Auto-generate sitemap listing all HTML pages with:
- lastmod dates
- changefreq (monthly for blog, yearly for static pages)
- priority (1.0 homepage, 0.8 market pages, 0.6 blog, 0.4 legal)

### Meta tags audit
Every page must have:
- Unique, keyword-rich title tag (50-60 chars)
- Meta description (150-160 chars, includes CTA)
- Canonical URL
- OG tags (og:title, og:description, og:url, og:type)
- Twitter card tags

### Schema markup
- Homepage: LocalBusiness schema (name, phone, email, area served)
- Blog posts: Article schema (headline, author, datePublished)
- How It Works: FAQPage schema for the questions section
- Market pages: LocalBusiness schema with serviceArea

### Robots.txt
Allow all, point to sitemap.

### Google Search Console
Write a plain-English setup guide as SEARCH_CONSOLE_SETUP.md:
1. Go to search.google.com/search-console
2. Add property → URL prefix → kodapropertygroup.com
3. Verify via HTML file (Claude Code creates the verification file)
4. Submit sitemap
5. Check for crawl errors after 48 hours

**git commit -m "Session 7: SEO infrastructure, sitemap, schema, meta tags"**

---

## SESSION 8 — Performance + Polish

- Compress any images (use imagemin or manual optimization)
- Minify CSS and JS for production
- Run Lighthouse audit in Chrome DevTools — target 90+ on all scores
- Fix any mobile layout issues found during audit
- Verify all internal links work (no 404s)
- Add favicon (simple KPG monogram or K in red)
- Verify Netlify form submissions are working
- Add Google Analytics (GA4) — write setup guide as ANALYTICS_SETUP.md
- Cross-browser check: Chrome, Safari, Firefox, mobile Chrome

**git commit -m "Session 8: Performance, polish, favicon, analytics"**

---

## SESSION 9 — Lead Capture Enhancement

### Netlify Forms upgrade
- Add form to every market page (simplified: name, phone, address)
- Add inline form to blog posts (mid-article CTA):
  "Have a property situation we can help with?"
  Name + Phone + [Get Help] — that's it, low friction

### CRM integration (future-ready)
Add a hidden field `source` to every form that captures
which page the lead came from. This passes to the email notification
so Julian knows "this lead came from the Charlotte County page"
vs. "this lead came from the foreclosure blog post."

Format: `source = "market/charlotte-county"` or `source = "blog/foreclosure"`

When the CRM's /api/leads endpoint is ready, the form can POST
directly to it. For now, Netlify handles it.

### Thank you page
Dedicated /thank-you.html:
- Confirms submission received
- Sets expectation: "We'll reach out within 24 hours"
- Offers immediate call option
- Links back to blog posts ("While you wait, these might help")

**git commit -m "Session 9: Lead capture forms on all pages, thank you page"**

---

## SESSION 10 — Content Expansion (data-driven)

By Session 10, the site has been live for several weeks.
Before starting, check Google Search Console for:
- Which pages are getting impressions
- Which keywords are showing up
- Which pages have high impressions but low click-through
  (need better title/meta description)

Then:
- Write 3 new blog posts targeting keywords with actual impressions
- Expand any market page that's getting traction (add more content,
  more FAQs, more local detail)
- Add a new deal case study if another deal has closed
- Fix any title/meta description that has low CTR

**git commit -m "Session 10: Data-driven content expansion"**

---

## Rules for Claude Code (website project)

1. This is a separate git repo from the CRM. Never mix the two.
2. Every page must load fast — no unnecessary JS, no large images
3. Every page must work perfectly on mobile
4. Netlify Forms handles all form submissions — no backend needed
5. Mark all personal details Julian needs to fill in with:
   [JULIAN TO FILL IN: description of what goes here]
6. After every session: deploy to Netlify, verify live, then commit
7. Never add placeholder Lorem Ipsum text to anything that will
   go live — write real copy or mark it for Julian to fill in
8. Research before writing — web search real county data before
   writing market pages and blog posts
9. One session = one commit. Label commits clearly.

## Contact Details to Use Throughout
Phone: [JULIAN TO ADD]
Email: [JULIAN TO ADD]
LLC: Koda Property Group LLC (Colorado)
Service area: Florida statewide
Markets: Charlotte, Sarasota, Lee, Polk, Pasco, Seminole counties