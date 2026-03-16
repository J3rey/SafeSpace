<template>
  <div class="main-container">
    <MainHeader />

    <main id="main-content" class="content py-3 py-sm-4 py-md-5 px-2 px-sm-3 px-md-4" role="main" aria-label="Welcome to SafeSpace">
      <section class="hero container-fluid px-3">
        <div class="row justify-content-center align-items-center">
          <div class="col-12 col-lg-6 text-center text-lg-start mb-4 mb-lg-0">
            <p class="eyebrow">Mental health support for students, caregivers, and educators</p>
            <h1 class="main-heading display-5 fw-bold mb-3">Your SafeSpace for immediate help, daily wellbeing, and trusted guidance.</h1>
            <p class="lead text-muted mb-4">
              Access crisis resources, journaling tools, teaching materials, and community support designed with student safety and privacy in mind.
            </p>
            <div class="d-flex flex-column flex-sm-row gap-2 justify-content-center justify-content-lg-start">
              <router-link class="btn cta-primary" to="/help-now" aria-label="Get help now">Get help now</router-link>
              <router-link class="btn cta-secondary" to="/interactive-tools" aria-label="Try interactive wellbeing tools">Explore tools</router-link>
            </div>
          </div>
          <div class="col-12 col-lg-5">
            <div class="trust-card">
              <div class="trust-header">
                <span aria-hidden="true">🛡️</span>
                <div>
                  <p class="trust-eyebrow mb-1">Safety first</p>
                  <p class="trust-title mb-0">Anonymous support with vetted resources</p>
                </div>
              </div>
              <ul class="trust-list" aria-label="Highlights of SafeSpace features">
                <li>
                  <span class="dot" aria-hidden="true"></span>
                  Immediate links to crisis text, chat, and phone lines.
                </li>
                <li>
                  <span class="dot" aria-hidden="true"></span>
                  Private journaling, mood tracking, and a wellness calendar for students.
                </li>
                <li>
                  <span class="dot" aria-hidden="true"></span>
                  Lesson-ready resources and response protocols for educators.
                </li>
                <li>
                  <span class="dot" aria-hidden="true"></span>
                  Donation transparency with up-to-date impact stats.
                </li>
              </ul>
              <div class="trust-footer">
                 <router-link to="/donation-statistics" class="link-inline">View donation impact -></router-link>
                 <router-link to="/about-us" class="link-inline">Read our mission -></router-link>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section class="container-fluid px-3 py-4 py-md-5" aria-label="Key actions">
        <div class="row g-3 g-md-4 justify-content-center">
          <div class="col-12 col-md-6 col-xl-4">
            <div class="action-card">
              <div class="icon-circle" aria-hidden="true">🚨</div>
              <h3 class="action-title">Need urgent help?</h3>
              <p class="text-muted mb-3">Find crisis contacts, quick safety steps, and supportive scripts you can use right now.</p>
              <router-link class="btn action-btn" to="/help-now">Go to Help Now</router-link>
            </div>
          </div>
          <div class="col-12 col-md-6 col-xl-4">
            <div class="action-card">
              <div class="icon-circle" aria-hidden="true">📝</div>
              <h3 class="action-title">Track your wellbeing</h3>
              <p class="text-muted mb-3">Use journaling prompts, habit tracking, and a wellness calendar tailored for youth.</p>
              <div class="d-flex gap-2">
                <router-link class="btn action-btn" to="/journal-log">Open Journal</router-link>
                <router-link class="btn action-btn ghost" to="/calendar">Wellness Calendar</router-link>
              </div>
            </div>
          </div>
          <div class="col-12 col-md-6 col-xl-4">
            <div class="action-card">
              <div class="icon-circle" aria-hidden="true">🎓</div>
              <h3 class="action-title">Teach with confidence</h3>
              <p class="text-muted mb-3">Grab lesson plans, classroom scripts, and response protocols for sensitive moments.</p>
              <div class="d-flex gap-2 flex-wrap">
                <router-link class="btn action-btn" to="/teaching-resources">Teaching Resources</router-link>
                <router-link class="btn action-btn ghost" to="/guidelines">Support Guidelines</router-link>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section class="container-fluid px-3 py-4 py-md-5" aria-label="Featured resources">
        <div class="row justify-content-center mb-4">
          <div class="col-12 col-lg-8 text-center">
            <p class="eyebrow">Featured</p>
            <h2 class="section-title">Guides, tools, and ways to support</h2>
            <p class="text-muted">Browse our most-requested resources to use in class, at home, or with community partners.</p>
          </div>
        </div>
        <div class="row g-3 g-md-4 justify-content-center">
          <div class="col-12 col-md-6 col-xl-4">
            <div class="resource-card">
              <div class="resource-tag">Guide</div>
              <h3 class="resource-title">Managing Stress Toolkit</h3>
              <p class="text-muted">Short breathing scripts, grounding exercises, and de-escalation steps you can use with students.</p>
                <router-link to="/guides/managing-stress" class="link-inline">Open guide -></router-link>
            </div>
          </div>
          <div class="col-12 col-md-6 col-xl-4">
            <div class="resource-card">
              <div class="resource-tag">Interactive</div>
              <h3 class="resource-title">Mindful Reading Pathway</h3>
              <p class="text-muted">A calming, self-paced reading flow that pairs gentle prompts with progress tracking.</p>
                <router-link to="/guides/mindful-reading" class="link-inline">Try it -></router-link>
            </div>
          </div>
          <div class="col-12 col-md-6 col-xl-4">
            <div class="resource-card">
              <div class="resource-tag">Impact</div>
              <h3 class="resource-title">Donation Transparency</h3>
              <p class="text-muted">See where contributions go, view current needs, and keep SafeSpace services free for students.</p>
                <router-link to="/donation-statistics" class="link-inline">View stats -></router-link>
            </div>
          </div>
        </div>
      </section>

      <div
        class="contact position-fixed bottom-0 start-0 m-2 m-sm-3 m-lg-4 fs-6 fs-sm-5"
        role="contentinfo"
        aria-label="Contact information"
      >
        <a href="mailto:support@safespace.com" aria-label="Contact us via email">Contact us</a>
      </div>
    </main>
  </div>
</template>

<script>
import MainHeader from "../components/MainHeader.vue";

export default {
  name: "HomeView",
  components: {
    MainHeader,
  },
};
</script>

<style scoped>
.main-container {
  font-family: Arial, sans-serif;
  position: relative;
  min-height: 100vh;
}

.content {
    display: flex;
    flex-direction: column;
    gap: 2.5rem;
    padding: 2.5rem 1.25rem 5rem;
    max-width: 1200px;
    margin: 0 auto;
}

.hero {
    background: radial-gradient(circle at 18% 18%, rgba(44, 110, 178, 0.14) 0, rgba(116, 169, 216, 0.08) 36%, #ffffff 100%);
    border-radius: 18px;
    padding: 2.2rem 1.6rem;
    box-shadow: 0 16px 40px rgba(44, 110, 178, 0.08);
}

.eyebrow {
  text-transform: uppercase;
  letter-spacing: 0.08em;
  font-size: 0.85rem;
  color: #6c757d;
  margin-bottom: 0.5rem;
}

.main-heading {
  color: #0f172a;
  line-height: 1.2;
}

.trust-card {
    background: white;
    border: 1px solid rgba(44, 110, 178, 0.1);
    border-radius: 16px;
    padding: 1.6rem;
    box-shadow: var(--shadow-soft, 0 10px 24px rgba(44, 110, 178, 0.12));
}

.trust-header {
  display: flex;
  gap: 0.75rem;
  align-items: center;
  margin-bottom: 1rem;
}

.trust-eyebrow {
  font-size: 0.85rem;
  color: #475569;
}

.trust-title {
  font-weight: 700;
  color: #0f172a;
}

.trust-list {
  list-style: none;
  padding: 0;
  margin: 0 0 1rem;
  display: grid;
  gap: 0.75rem;
}

.trust-list li {
    display: flex;
    gap: 0.5rem;
    color: #334155;
    align-items: center;
    line-height: 1.5;
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: var(--brand-primary, #2c6eb2);
  flex-shrink: 0;
}

.trust-footer {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.cta-primary {
  background-color: var(--brand-primary, #2c6eb2);
  color: white;
  border: none;
  padding: 0.85rem 1.5rem;
  border-radius: 30px;
  font-weight: 600;
  text-decoration: none;
}

.cta-secondary {
  border: 2px solid var(--brand-primary, #2c6eb2);
  color: var(--brand-primary, #2c6eb2);
  padding: 0.85rem 1.5rem;
  border-radius: 30px;
  font-weight: 600;
  text-decoration: none;
}

.action-card {
    background: white;
    border: 1px solid rgba(44, 110, 178, 0.12);
    border-radius: 16px;
    padding: 1.6rem;
    box-shadow: var(--shadow-soft, 0 10px 24px rgba(44, 110, 178, 0.12));
    height: 100%;
}

.icon-circle {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background: rgba(44, 110, 178, 0.12);
  display: grid;
  place-items: center;
  font-size: 1.25rem;
  margin-bottom: 0.75rem;
}

.action-title {
  font-weight: 700;
  color: #0f172a;
}

.action-btn {
  background-color: var(--brand-primary, #2c6eb2);
  color: white;
  border: none;
  padding: 0.7rem 1.2rem;
  border-radius: 10px;
  font-weight: 600;
  text-decoration: none;
  display: inline-block;
}

.action-btn.ghost {
  background: white;
  color: var(--brand-primary, #2c6eb2);
  border: 1px solid var(--brand-primary, #2c6eb2);
}

.section-title {
  font-weight: 700;
  color: #0f172a;
}

.resource-card {
    background: linear-gradient(135deg, #0f172a 0%, #13233b 100%);
    color: white;
    border-radius: 16px;
    padding: 1.5rem;
    height: 100%;
    box-shadow: 0 16px 36px rgba(15, 23, 42, 0.3);
    border: 1px solid rgba(255, 255, 255, 0.06);
}
.resource-card p,
.resource-card .text-muted {
  color: #dbeafe;
}

.resource-tag {
    display: inline-block;
    background: rgba(255, 255, 255, 0.14);
    border: 1px solid rgba(255, 255, 255, 0.24);
    color: white;
    border-radius: 999px;
    padding: 0.25rem 0.75rem;
    margin-bottom: 0.75rem;
    font-size: 0.9rem;
}

.resource-title {
    font-weight: 700;
    margin-bottom: 0.5rem;
}

.link-inline {
    color: var(--brand-primary, #2c6eb2);
    text-decoration: none;
    font-weight: 700;
}

.link-inline:hover {
  text-decoration: underline;
}

.contact {
  color: #666;
  cursor: pointer;
  font-size: 1rem;
  font-weight: 500;
  transition: color 0.3s ease;
  z-index: 10;
}

.contact:hover {
  color: var(--brand-primary, #2c6eb2);
}

@media (max-width: 991.98px) {
  .hero {
    text-align: center;
  }

  .trust-footer {
    justify-content: center;
  }
}
</style>
