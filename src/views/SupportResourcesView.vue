<template>
  <div class="support-resources">
    <MainHeader />

    <main class="content py-3 py-sm-4 py-md-5 px-2 px-sm-3 px-md-4" role="main">
      <section class="hero container-fluid px-3">
        <div class="row justify-content-center align-items-center g-3 g-md-4">
          <div class="col-12 col-lg-7 text-center text-lg-start">
            <p class="eyebrow">Support and resources</p>
            <h1 class="hero-title">Find the right help, with calm guidance and clear next steps.</h1>
            <p class="hero-subtitle">Crisis contacts, resource library, and community spaces designed to keep students and caregivers supported.</p>
            <div class="d-flex flex-column flex-sm-row gap-2 justify-content-center justify-content-lg-start">
              <router-link class="btn primary" to="/help-now" aria-label="Open crisis resources">Crisis contacts</router-link>
              <a class="btn ghost" href="#library" aria-label="Jump to resource library">Resource library</a>
              <router-link class="btn ghost" to="/community-chat" aria-label="Open community chat">Community chat</router-link>
            </div>
          </div>
          <div class="col-12 col-lg-5">
            <div class="status-card" aria-label="Live support highlights">
              <div class="status-row">
                <div class="dot" aria-hidden="true"></div>
                <div>
                  <p class="status-label">Available 24/7</p>
                  <p class="status-value">Text, chat, and phone crisis lines</p>
                </div>
              </div>
              <div class="status-row">
                <div class="dot green" aria-hidden="true"></div>
                <div>
                  <p class="status-label">Educator toolkit</p>
                  <p class="status-value">Guidelines, scripts, and classroom plans</p>
                </div>
              </div>
              <div class="status-row">
                <div class="dot teal" aria-hidden="true"></div>
                <div>
                  <p class="status-label">Community care</p>
                  <p class="status-value">Peer-safe chat with moderation guardrails</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section class="container-fluid px-3 py-4 py-md-5" aria-label="Immediate support">
        <div class="row g-3 g-md-4 justify-content-center">
          <div class="col-12 col-md-6 col-xl-4">
            <div class="card soft">
              <div class="icon" aria-hidden="true">📞</div>
              <h3>Hotlines and chat</h3>
              <p class="muted">Direct links to crisis text, phone, and chat plus hours and privacy details.</p>
              <router-link class="btn link" to="/help-now">Open crisis contacts</router-link>
            </div>
          </div>
          <div class="col-12 col-md-6 col-xl-4">
            <div class="card soft">
              <div class="icon" aria-hidden="true">🧭</div>
              <h3>Response playbooks</h3>
              <p class="muted">Step-by-step guidance for de-escalation, warm handoffs, and after-care plans.</p>
              <router-link class="btn link" to="/guidelines">View guidelines</router-link>
            </div>
          </div>
          <div class="col-12 col-md-6 col-xl-4">
            <div class="card soft">
              <div class="icon" aria-hidden="true">🎓</div>
              <h3>Teaching resources</h3>
              <p class="muted">Slides, scripts, and tracking templates to run classroom sessions confidently.</p>
              <router-link class="btn link" to="/teaching-resources">Browse resources</router-link>
            </div>
          </div>
        </div>
      </section>

      <section id="library" class="container-fluid px-3 py-4 py-md-5" aria-label="Resource library">
        <div class="row justify-content-center mb-3 mb-md-4">
          <div class="col-12 col-lg-8 text-center">
            <p class="eyebrow">Library</p>
            <h2 class="section-title">Curated support kits</h2>
            <p class="muted">Downloadable templates and guided experiences you can use immediately.</p>
          </div>
        </div>
        <div class="row g-3 g-md-4 justify-content-center">
          <div class="col-12 col-md-6 col-xl-4">
            <div class="card dark">
              <div class="tag">Students</div>
              <h3>Wellness journal + calendar</h3>
              <p class="muted">Track mood, gratitude, and commitments in one place.</p>
              <div class="actions">
                <router-link class="btn primary" to="/journal-log">Open journal</router-link>
                <router-link class="btn ghost" to="/calendar">Wellness calendar</router-link>
              </div>
            </div>
          </div>
          <div class="col-12 col-md-6 col-xl-4">
            <div class="card dark">
              <div class="tag">Guided</div>
              <h3>Breathing and grounding set</h3>
              <p class="muted">Follow bite-sized guided exercises built for busy moments.</p>
              <router-link class="btn primary" to="/interactive-tools">Start exercises</router-link>
            </div>
          </div>
          <div class="col-12 col-md-6 col-xl-4">
            <div class="card dark">
              <div class="tag">Community</div>
              <h3>Moderated peer chat</h3>
              <p class="muted">Join a calm space with clear boundaries and safety prompts.</p>
              <router-link class="btn primary" to="/community-chat">Enter chat</router-link>
            </div>
          </div>
        </div>
      </section>

      <section class="container-fluid px-3 py-4 py-md-5" aria-label="Community and professionals">
        <div class="row g-3 g-md-4 justify-content-center">
          <div class="col-12 col-md-6">
            <div class="card soft">
              <div class="icon" aria-hidden="true">🤝</div>
              <h3>Caregiver and educator hub</h3>
              <p class="muted">Share updates with caregivers, find scripts for tough calls, and track follow-ups.</p>
              <div class="actions">
                <router-link class="btn ghost" to="/guidelines">Support scripts</router-link>
                <router-link class="btn ghost" to="/teaching-resources">Planning tools</router-link>
              </div>
            </div>
          </div>
          <div class="col-12 col-md-6">
            <div class="card soft">
              <div class="icon" aria-hidden="true">💬</div>
              <h3>Community chat etiquette</h3>
              <p class="muted">See the safety rules, reporting steps, and moderation standards that keep the space calm.</p>
              <router-link class="btn link" to="/community-chat">View chat space</router-link>
            </div>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
import MainHeader from "../components/MainHeader.vue";

export default {
  name: "SupportResourcesView",
  components: { MainHeader },
};
</script>

<style scoped>
.support-resources {
  font-family: Arial, sans-serif;
  background-color: var(--surface, #f7f9fc);
  min-height: 100vh;
  color: var(--text-primary, #0f172a);
}

.content {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.hero {
  background: linear-gradient(135deg, rgba(44, 110, 178, 0.16), rgba(116, 169, 216, 0.18));
  border-radius: 18px;
  padding: 2rem 1.5rem;
}

.eyebrow {
  text-transform: uppercase;
  letter-spacing: 0.08em;
  font-size: 0.85rem;
  color: #5b708f;
  margin-bottom: 0.5rem;
}

.hero-title {
  font-weight: 700;
  font-size: 2rem;
  line-height: 1.3;
  margin-bottom: 0.75rem;
}

.hero-subtitle {
  color: #4b5563;
  margin-bottom: 1rem;
}

.status-card {
  background: white;
  border: 1px solid #e5e7eb;
  border-radius: 14px;
  padding: 1.25rem;
  box-shadow: 0 10px 24px rgba(15, 23, 42, 0.08);
  display: grid;
  gap: 0.75rem;
}

.status-row {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0.75rem;
  align-items: center;
}

.dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: #5b8def;
}

.dot.green {
  background: #7ec8a5;
}

.dot.teal {
  background: #7ec8c9;
}

.status-label {
  font-size: 0.95rem;
  font-weight: 600;
  color: #111827;
  margin: 0;
}

.status-value {
  margin: 0;
  color: #4b5563;
  font-size: 0.95rem;
}

.btn {
  border-radius: 999px;
  padding: 0.75rem 1.4rem;
  font-weight: 600;
  text-decoration: none;
  border: 1px solid transparent;
  transition: all 0.2s ease;
  display: inline-block;
  text-align: center;
}

.btn.primary {
  background: var(--brand-primary, #2c6eb2);
  color: white;
  border-color: var(--brand-primary, #2c6eb2);
}

.btn.ghost {
  background: white;
  color: var(--brand-primary, #2c6eb2);
  border-color: rgba(44, 110, 178, 0.28);
}

.btn.link {
  background: transparent;
  color: #5b8def;
  border-color: transparent;
  padding-left: 0;
}

.btn:hover {
  transform: translateY(-1px);
  box-shadow: 0 8px 18px rgba(15, 23, 42, 0.08);
}

.card {
  background: white;
  border: 1px solid rgba(44, 110, 178, 0.12);
  border-radius: 14px;
  padding: 1.4rem;
  height: 100%;
  box-shadow: var(--shadow-soft, 0 10px 24px rgba(44, 110, 178, 0.12));
}

.card.soft {
  background: #f7f9fc;
}

.card.dark {
  background: #0f172a;
  color: white;
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.card.dark .muted {
  color: #cbd5e1;
}

.icon {
  width: 48px;
  height: 48px;
  border-radius: 12px;
  background: rgba(44, 110, 178, 0.12);
  display: grid;
  place-items: center;
  font-size: 1.2rem;
  margin-bottom: 0.75rem;
}

.tag {
  display: inline-block;
  background: rgba(255, 255, 255, 0.14);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 999px;
  padding: 0.25rem 0.75rem;
  margin-bottom: 0.75rem;
  font-size: 0.9rem;
}

.section-title {
  font-weight: 700;
  color: #0f172a;
  margin-bottom: 0.4rem;
}

.muted {
  color: #4b5563;
  margin-bottom: 1rem;
}

.actions {
  display: flex;
  gap: 0.6rem;
  flex-wrap: wrap;
}

@media (max-width: 991.98px) {
  .hero-title {
    text-align: center;
  }
  .hero-subtitle {
    text-align: center;
  }
}
</style>
