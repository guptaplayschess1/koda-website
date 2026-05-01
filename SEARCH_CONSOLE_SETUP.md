# Google Search Console Setup

## Step 1: Add the Property

1. Go to https://search.google.com/search-console
2. Click "Add Property"
3. Choose "URL prefix" and enter: `https://kodapropertygroup.com`
4. Click Continue

## Step 2: Verify Ownership (Netlify method)

1. Download the HTML verification file Google provides (looks like `google1234abcd.html`)
2. Add it to your `website/` root directory
3. Push to Netlify: `cd website && git add google*.html && git commit -m "Add GSC verification file" && netlify deploy --prod --dir .`
4. Back in Search Console, click Verify

## Step 3: Submit Sitemap

1. In GSC left sidebar: Sitemaps
2. Enter: `sitemap.xml`
3. Click Submit

Google will crawl the sitemap and report which URLs it has indexed.

## Step 4: Configure Coverage Report

After 1–2 weeks, check:
- **Coverage > Valid**: All 20 pages should appear here
- **Coverage > Excluded**: `thank-you.html` should be here (blocked by robots.txt)
- **Coverage > Error**: Fix any errors shown

## Step 5: Watch for in GSC After Launch

- **Performance**: which queries bring impressions/clicks (takes 2-4 weeks)
- **Core Web Vitals**: page speed signals from real users
- **Mobile Usability**: any mobile rendering issues

## Key Pages to Monitor

| Page | Target Keywords |
|------|----------------|
| charlotte-county.html | sell house Charlotte County FL, cash buyer Port Charlotte |
| seminole-county.html | sell house Seminole County FL, cash buyer Sanford FL |
| blog/florida-foreclosure-timeline.html | Florida foreclosure timeline, lis pendens Florida |
| blog/inherited-property-florida.html | inherited property Florida, probate real estate Florida |
| blog/sell-vacant-lot-florida.html | sell vacant lot Florida, sell land Charlotte County |

## After 30 Days

Look at Search Console Performance to see:
1. Which blog posts are getting impressions first
2. What queries are triggering market pages
3. Whether the homepage is ranking for brand searches

Use that data to decide what Session 10 content to write.
