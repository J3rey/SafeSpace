<template>
  <div class="teaching-resources-container">
    <MainHeader />
    
    <main class="content py-3 py-sm-4 py-md-5 px-2 px-sm-3 px-md-4">
      <div class="container-fluid px-3">
        <div class="row justify-content-center">
          <div class="col-12 col-lg-10 col-xl-9">
            <div class="content-wrapper surface-card p-3 p-md-5">
              <!-- Header Section -->
              <div class="page-header text-center mb-5">
                <div class="header-icon mb-3">📚</div>
                <h1 class="page-title">Teaching Resources</h1>
                <p class="page-subtitle">Comprehensive materials to support mental health education in your classroom</p>
              </div>

              <div class="row g-3 g-md-4 mb-4">
                <div class="col-12 col-md-6 col-xl-4">
                  <div class="resource-card surface-card h-100" aria-label="Lesson plans">
                    <div class="resource-icon" aria-hidden="true">🗂️</div>
                    <div class="resource-title">Lesson bundles (45-60 min)</div>
                    <p class="resource-description">Ready-to-use slides, scripts, and student handouts for stress, sleep, and digital wellbeing.</p>
                    <ul class="resource-items">
                      <li>Intro to emotions (grades 6–9)</li>
                      <li>Grounding and breathing practice</li>
                      <li>Healthy online boundaries</li>
                    </ul>
                    <button class="btn btn-brand w-100" type="button">Download ZIP</button>
                  </div>
                </div>
                <div class="col-12 col-md-6 col-xl-4">
                  <div class="resource-card surface-card h-100" aria-label="Classroom scripts">
                    <div class="resource-icon" aria-hidden="true">🗣️</div>
                    <div class="resource-title">Scripts for tough moments</div>
                    <p class="resource-description">Concise language for check-ins, de-escalation, and caregiver calls that keeps students safe and respected.</p>
                    <ul class="resource-items">
                      <li>One-minute emotional check-in</li>
                      <li>De-escalation phrases</li>
                      <li>Caregiver outreach templates</li>
                    </ul>
                    <button class="btn btn-brand w-100" type="button">Download PDF</button>
                  </div>
                </div>
                <div class="col-12 col-md-6 col-xl-4">
                  <div class="resource-card surface-card h-100" aria-label="Data and reporting">
                    <div class="resource-icon" aria-hidden="true">📈</div>
                    <div class="resource-title">Data and reporting aids</div>
                    <p class="resource-description">Simple forms to log observations, note handoffs, and capture follow-up plans that comply with school policy.</p>
                    <ul class="resource-items">
                      <li>Observation log (print + digital)</li>
                      <li>Warm handoff form</li>
                      <li>Re-entry plan template</li>
                    </ul>
                    <button class="btn btn-brand w-100" type="button">Get templates</button>
                  </div>
                </div>
              </div>

              <div class="info-section">
                <div class="row g-3 g-md-4 align-items-stretch">
                  <div class="col-12 col-lg-6">
                    <div class="info-card surface-card h-100">
                      <h4>Training and PD</h4>
                      <p>Request a 45-minute virtual training on crisis response, trauma-informed communication, and classroom de-escalation.</p>
                      <button class="btn btn-ghost" type="button">Request training</button>
                    </div>
                  </div>
                  <div class="col-12 col-lg-6">
                    <div class="info-card surface-card h-100">
                      <h4>Monthly educator newsletter</h4>
                      <p>Lesson drops, conversation starters, and policy updates curated for advisors and teachers.</p>
                      <button class="btn btn-ghost" type="button">Join the list</button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import MainHeader from '../components/MainHeader.vue'

export default {
  name: 'TeachingResourcesView',
  components: {
    MainHeader
  }
}
</script>

<style scoped>
.teaching-resources-container {
  font-family: Arial, sans-serif;
  min-height: 100vh;
  background-color: #f8f9fa;
}

.content-wrapper {
  border-radius: 12px;
  box-shadow: none;
}

.page-header {
  border-bottom: 2px solid #e9ecef;
  padding-bottom: 2rem;
}

.header-icon {
  font-size: 4rem;
}

.page-title {
  font-size: 2.5rem;
  font-weight: 700;
  color: #212529;
  margin-bottom: 1rem;
}

.page-subtitle {
  font-size: 1.2rem;
  color: #6c757d;
  margin: 0;
}

.resource-card {
  border-radius: 12px;
  padding: 2rem;
  height: 100%;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  text-align: center;
}

.resource-card:hover {
  transform: translateY(-3px);
  box-shadow: var(--shadow-soft, 0 10px 24px rgba(44, 110, 178, 0.12));
}

.resource-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.resource-title {
  font-size: 1.4rem;
  font-weight: 600;
  color: #212529;
  margin-bottom: 1rem;
}

.resource-description {
  color: #6c757d;
  margin-bottom: 1.5rem;
  line-height: 1.6;
}

.resource-items {
  list-style: none;
  padding: 0;
  margin-bottom: 2rem;
  text-align: left;
}

.resource-items li {
  padding: 0.5rem 0;
  color: #495057;
  position: relative;
  padding-left: 1.5rem;
}

.resource-items li:before {
  content: "•";
  color: #007bff;
  font-weight: bold;
  position: absolute;
  left: 0;
}



.emergency-btn {
  background-color: #dc3545;
  border-color: #dc3545;
}

.emergency-btn:hover {
  background-color: #c82333;
  border-color: #c82333;
}

.info-section {
  border-top: 2px solid #e9ecef;
  padding-top: 2rem;
}

.info-card {
  border-radius: 8px;
  padding: 1.5rem;
  text-align: center;
  height: 100%;
  margin-bottom: 1rem;
}

.info-card h4 {
  color: #212529;
  margin-bottom: 1rem;
}

.info-card p {
  color: #6c757d;
  margin-bottom: 1.5rem;
}



</style>
