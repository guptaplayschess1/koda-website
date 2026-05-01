# Google Analytics 4 Setup

## Step 1: Create a GA4 Property

1. Go to https://analytics.google.com
2. Admin > Create > Property
3. Property name: "Koda Property Group"
4. Time zone: Eastern Time
5. Currency: USD
6. Continue through setup

## Step 2: Get Your Measurement ID

After creating the property, GA4 gives you a Measurement ID like `G-XXXXXXXXXX`.
Copy it.

## Step 3: Add GA4 to the Site

Open `website/js/main.js` and add this at the top of the file:

```javascript
// Google Analytics 4
(function() {
  var s = document.createElement('script');
  s.async = true;
  s.src = 'https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX';
  document.head.appendChild(s);
})();
window.dataLayer = window.dataLayer || [];
function gtag(){dataLayer.push(arguments);}
gtag('js', new Date());
gtag('config', 'G-XXXXXXXXXX');
```

Replace `G-XXXXXXXXXX` with your actual Measurement ID (twice).

Then redeploy: `netlify deploy --prod --dir .`

## Step 4: Verify It's Working

1. Open your site in a browser
2. In GA4: Reports > Realtime
3. You should see yourself as an active user within 30 seconds

## Key Events to Track (already collected automatically by GA4)

- `page_view` — every page load
- `scroll` — 90% scroll depth
- `click` — outbound link clicks

## Custom Events Worth Adding Later

Once basic GA4 is working, add these custom events in `main.js`:

**Form submission tracking:**
```javascript
// In your Netlify form success handler
gtag('event', 'generate_lead', {
  'event_category': 'contact',
  'event_label': 'contact_form'
});
```

**Phone click tracking:**
```javascript
document.querySelectorAll('a[href^="tel:"]').forEach(function(el) {
  el.addEventListener('click', function() {
    gtag('event', 'click', {
      'event_category': 'contact',
      'event_label': 'phone_click'
    });
  });
});
```

## Reports to Watch Weekly

1. **Acquisition > Traffic acquisition**: Where visitors come from (organic, direct, referral)
2. **Engagement > Pages and screens**: Which pages get the most views
3. **Acquisition > Organic Google**: What search terms bring visitors (after 2-3 weeks)

## Connecting GA4 to Search Console

After both are set up:
1. GA4: Admin > Property > Search Console Links
2. Link your Search Console property
3. This lets you see search queries in GA4 Reports

## What Success Looks Like at 90 Days

- 200+ organic sessions/month from blog posts
- Charlotte County / Seminole County market pages showing impressions in GSC
- At least 1 contact form submission per week from organic traffic
