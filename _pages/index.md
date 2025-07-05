---
layout: default
permalink: /
title: "ExcelFix 24 – Rapid Spreadsheet Rescue"
---
<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="icon" href="{{ '/favicon.svg' | relative_url }}" type="image/svg+xml">

  <!-- Hero -->
  <header class="section hero">
    <h1>Fix dirty spreadsheets&nbsp;in&nbsp;24&nbsp;h.</h1>
    <p class="sub">Upload your file → pay → get a custom macro and Loom walkthrough tomorrow.</p>
    <a class="btn primary" href="https://docs.google.com/forms/d/e/1FAIpQLScXrZ8CXKn3zIAzqjyL3mc3_PKXks1M_hvgyaQtHF3L04s9sw/viewform?usp=header" target="_blank">Get your quote</a>
  </header>

  <!-- How it works -->
  <section class="section three">
    <div class="card">
      <h3>1&nbsp;· Upload</h3><p>Send your Excel/CSV via our form.</p>
    </div>
    <div class="card">
      <h3>2&nbsp;· Pay</h3><p>Fixed price — no hourly surprises.</p>
    </div>
    <div class="card">
      <h3>3&nbsp;· Done</h3><p>Receive a ready-to-run workbook + Loom video.</p>
    </div>
  </section>

  <!-- Pricing -->
  <section class="section pricing">
    <h2>Simple pricing</h2>
    <div class="tiers">
      <div class="tier">
        <h3>Quick</h3><p class="quote">Request a quote</p>
        <p>≤ 1 sheet,<br>2 routines</p>
        <a class="btn" href="https://buy.stripe.com/dRm00j8Jt1MtceC4UP0Ny01">Pay link</a>
      </div>
      <div class="tier">
        <h3>Standard</h3><p class="quote">Request a quote</p>
        <p>≤ 3 sheets,<br>up to 5 routines</p>
        <a class="btn" href="https://buy.stripe.com/7sY4gz0cXdvb0vUaf90Ny02">Pay link</a>
      </div>
      <div class="tier">
        <h3>Complex<br><span class="small">weekly</span></h3><p class="quote">Request a quote</p>
        <p>Multi-sheet automations, API calls, Power Query.</p>
        <a class="btn" href="https://buy.stripe.com/14A28rcZJ9eVbay8710Ny00">Subscribe</a>
      </div>
    </div>
  </section>

  <!-- Testimonials (placeholder) -->
  <section class="section testimonials">
    <h2>What early users say</h2>
    <blockquote>“Saved me two nights of misery formatting exports.”<br><span>— Logistics analyst, Perth</span></blockquote>
    <blockquote>“Macro delivered in 15 h, worked first go.”<br><span>— SME accountant</span></blockquote>
  </section>

  <!-- FAQ -->
  <section class="section faq">
    <h2>FAQ</h2>
    <details><summary>Which versions of Excel?</summary><p>Tested on Excel 2016, 2019, 365 (Win & Mac).</p></details>
    <details><summary>What files can I send?</summary><p>.xlsx, .xlsm, .csv, or zipped folders up to 20 MB.</p></details>
    <details><summary>Refund policy?</summary><p>100 % if we can’t deliver the promised fix within the timeframe.</p></details>
  </section>

  <!-- Footer -->
  <footer class="section footer">
    <p>ABN 12 345 678 901 • <a href="mailto:hello@excelfix24.com">hello@excelfix24.com</a> • <a href="https://www.linkedin.com/in/giuseppecarusi" target="_blank">LinkedIn</a></p>
  </footer>
  <script>
    (function () {
      const locale = navigator.language || 'en-US';
      const currencyMap = {
        'en-US': 'USD',
        'en-GB': 'GBP',
        'en-AU': 'AUD',
        'en-CA': 'CAD',
        'fr-FR': 'EUR',
        'de-DE': 'EUR',
        'es-ES': 'EUR'
      };

      let currency = currencyMap[locale];
      if (!currency) {
        const base = locale.split('-')[0];
        for (const key in currencyMap) {
          if (key.startsWith(base)) {
            currency = currencyMap[key];
            break;
          }
        }
      }

      const rates = { USD: 0.66, GBP: 0.52, EUR: 0.61, CAD: 0.89 };

      async function loadRates() {
        try {
          const res = await fetch('https://open.er-api.com/v6/latest/AUD');
          if (res.ok) {
            const data = await res.json();
            if (data && data.rates) {
              Object.assign(rates, data.rates);
            }
          }
        } catch (e) {
          console.warn('Currency fetch failed', e);
        }
      }

      function formatPrice(aud) {
        const rate = rates[currency];
        const value = rate ? aud * rate : null;
        if (value !== null) {
          try {
            return new Intl.NumberFormat(locale, {
              style: 'currency',
              currency
            }).format(value);
          } catch (e) {
            return null;
          }
        }
        return null;
      }

      async function updatePrices() {
        await loadRates();
        document.querySelectorAll('.price').forEach(el => {
          const text = el.textContent;
          const match = text.replace(/,/g, '').match(/\$([0-9.]+)/);
          if (match) {
            const aud = parseFloat(match[1]);
            const converted = formatPrice(aud);
            if (converted) {
              el.textContent = converted;
            } else if (currency) {
              el.textContent = `$${aud} AUD`;
            } else {
              el.style.display = 'none';
            }
          }
        });
      }
      updatePrices();
    })();
  </script>
{% include analytics.html %}
