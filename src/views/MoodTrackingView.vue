<template>
  <div class="mood-view">
    <MainHeader />

    <main class="content py-3 py-sm-4 py-md-5 px-2 px-sm-3 px-md-4" role="main">
      <section class="hero container-fluid px-3">
        <div class="row justify-content-center g-3 g-md-4 align-items-center">
          <div class="col-12 col-lg-7">
            <p class="eyebrow">Mood tracking</p>
            <h1 class="hero-title">Track feelings, spot patterns, and stay balanced.</h1>
            <p class="hero-subtitle">Log your mood, add quick notes, and watch weekly trends with gentle visual feedback.</p>
            <div class="actions">
              <button class="btn btn-brand" @click="saveEntry" aria-label="Save mood entry">Save entry</button>
              <router-link class="btn btn-ghost" to="/journal-log">Open journal</router-link>
            </div>
            <p v-if="toast" class="toast">{{ toast }}</p>
          </div>
          <div class="col-12 col-lg-5">
            <div class="card surface-card stats">
              <p class="eyebrow mb-1">This week</p>
              <h2 class="stat-number">{{ weeklyAverage }}/10</h2>
              <p class="muted">Average mood</p>
              <div class="bar">
                <div class="fill" :style="{ width: `${weeklyAverage * 10}%` }"></div>
              </div>
              <ul class="mini-list">
                <li v-for="(item, index) in recent" :key="index">
                  <span class="dot" :style="{ background: item.color }"></span>
                  <span>{{ item.label }}</span>
                  <span class="muted">{{ item.time }}</span>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </section>

      <section class="container-fluid px-3 py-4 py-md-5" aria-label="Log mood">
        <div class="row g-3 g-md-4">
          <div class="col-12 col-lg-6">
            <div class="card surface-card form-card">
              <label class="field">
                <span>Mood (1-10)</span>
                <input type="range" min="1" max="10" v-model="entry.mood" />
                <div class="range-values">
                  <span>1</span>
                  <strong>{{ entry.mood }}</strong>
                  <span>10</span>
                </div>
              </label>
              <label class="field">
                <span>Energy</span>
                <div class="chips">
                  <button v-for="level in energyLevels" :key="level" :class="['chip', entry.energy === level ? 'active' : '']" @click="entry.energy = level" type="button">{{ level }}</button>
                </div>
              </label>
              <label class="field">
                <span>Notes</span>
                <textarea v-model="entry.notes" rows="3" placeholder="What influenced your mood today?"></textarea>
              </label>
            </div>
          </div>
          <div class="col-12 col-lg-6">
            <div class="card surface-card grid-card">
              <div class="grid-head d-flex align-items-center justify-content-between">
                <h3>Recent entries</h3>
                <router-link class="btn link" to="/journal-log">View all</router-link>
              </div>
              <div class="entry-list">
                <div v-for="item in log" :key="item.id" class="entry-row">
                  <div class="pill" :style="{ background: item.color }">{{ item.mood }}/10</div>
                  <div class="entry-body">
                    <p class="entry-title">{{ item.title }}</p>
                    <p class="muted">{{ item.time }}</p>
                  </div>
                </div>
                <div v-if="log.length === 0" class="empty">No entries yet. Start with a quick log above.</div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
import { reactive, ref } from "vue";
import MainHeader from "../components/MainHeader.vue";

export default {
  name: "MoodTrackingView",
  components: { MainHeader },
  setup() {
    const entry = reactive({ mood: 6, energy: "Balanced", notes: "" });
    const energyLevels = ["Low", "Balanced", "High"];
    const log = ref([]);
    const toast = ref("");

    const colors = {
      Low: "#74a9d8",
      Balanced: "#2c6eb2",
      High: "#a8c8e4",
    };

    const weeklyAverage = 7.2;
    const recent = [
      { label: "Today", color: colors.Balanced, time: "9:00" },
      { label: "Yesterday", color: colors.Low, time: "20:10" },
      { label: "Mon", color: colors.High, time: "18:45" },
    ];

    const saveEntry = () => {
      const newItem = {
        id: Date.now(),
        mood: entry.mood,
        energy: entry.energy,
        title: `${entry.energy} energy`
          .replace("Low", "Low energy")
          .replace("High", "High energy"),
        time: new Date().toLocaleTimeString([], { hour: "2-digit", minute: "2-digit" }),
        color: colors[entry.energy] || colors.Balanced,
      };
      log.value = [newItem, ...log.value].slice(0, 6);
      toast.value = "Mood saved.";
      setTimeout(() => (toast.value = ""), 1800);
    };

    return {
      entry,
      energyLevels,
      log,
      toast,
      weeklyAverage,
      recent,
      saveEntry,
    };
  },
};
</script>

<style scoped>
.mood-view {
  font-family: "Segoe UI", "Inter", system-ui, sans-serif;
  background: var(--surface, #eaf2fa);
  min-height: 100vh;
  color: var(--text-primary, #0f172a);
}

.content {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.hero {
  background: var(--gradient-soft, linear-gradient(135deg, rgba(44, 110, 178, 0.12), rgba(116, 169, 216, 0.12)));
  border-radius: 18px;
  padding: 1.75rem 1.5rem;
  box-shadow: var(--shadow-soft, 0 10px 24px rgba(44, 110, 178, 0.12));
}

.eyebrow {
  text-transform: uppercase;
  letter-spacing: 0.08em;
  font-size: 0.85rem;
  color: var(--brand-primary, #2c6eb2);
  margin-bottom: 0.35rem;
  font-weight: 700;
}

.hero-title {
  font-weight: 700;
  font-size: 1.9rem;
  margin-bottom: 0.5rem;
}

.hero-subtitle {
  color: var(--text-muted, #475569);
  margin-bottom: 0.9rem;
}

.actions {
  display: flex;
  gap: 0.6rem;
  flex-wrap: wrap;
  align-items: center;
}

.toast {
  color: var(--brand-primary, #2c6eb2);
  margin-top: 0.5rem;
}

.card {
  border-radius: var(--radius-base, 16px);
  padding: 1.2rem;
}

.stats {
  display: grid;
  gap: 0.75rem;
}

.stat-number {
  font-size: 2.4rem;
  margin: 0;
  color: var(--brand-primary, #2c6eb2);
}

.bar {
  background: rgba(44, 110, 178, 0.1);
  border-radius: 999px;
  height: 10px;
  overflow: hidden;
}

.bar .fill {
  background: var(--brand-primary, #2c6eb2);
  height: 100%;
  border-radius: 999px;
}

.mini-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  gap: 0.35rem;
}

.mini-list li {
  display: grid;
  grid-template-columns: auto 1fr auto;
  gap: 0.5rem;
  align-items: center;
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: var(--brand-accent, #a8c8e4);
}

.muted {
  color: var(--text-muted, #475569);
  margin: 0;
}

.btn {
  border-radius: 999px;
  padding: 0.7rem 1.3rem;
  font-weight: 700;
  text-decoration: none;
  border: 1px solid transparent;
  transition: all 0.2s ease;
  display: inline-block;
  text-align: center;
}

.btn.link {
  background: transparent;
  color: var(--brand-primary, #2c6eb2);
  border: none;
  padding-left: 0;
}

.form-card .field {
  display: grid;
  gap: 0.35rem;
  margin-bottom: 0.85rem;
}

.field span {
  font-weight: 700;
}

input[type="range"] {
  width: 100%;
}

.range-values {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-weight: 700;
  color: var(--brand-primary, #2c6eb2);
}

.chips {
  display: flex;
  gap: 0.5rem;
}

.chip {
  border-radius: 999px;
  border: 1px solid rgba(44, 110, 178, 0.18);
  padding: 0.35rem 0.8rem;
  background: rgba(44, 110, 178, 0.08);
  color: var(--text-primary, #0f172a);
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s ease;
}

.chip.active {
  background: var(--brand-primary, #2c6eb2);
  color: white;
  border-color: var(--brand-primary, #2c6eb2);
}

textarea {
  width: 100%;
  border-radius: 12px;
  border: 1px solid rgba(44, 110, 178, 0.2);
  padding: 0.75rem;
  font-family: inherit;
  resize: vertical;
}

.grid-card {
  display: grid;
  gap: 0.75rem;
}

.grid-head {
  border-bottom: 1px solid rgba(44, 110, 178, 0.14);
  padding-bottom: 0.35rem;
}

.entry-list {
  display: grid;
  gap: 0.65rem;
}

.entry-row {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0.75rem;
  align-items: center;
}

.pill {
  border-radius: 999px;
  padding: 0.4rem 0.8rem;
  color: #0f172a;
  font-weight: 700;
}

.entry-body {
  display: grid;
  gap: 0.15rem;
}

.entry-title {
  margin: 0;
  font-weight: 700;
}

.empty {
  color: var(--text-muted, #475569);
}

@media (max-width: 991.98px) {
  .hero-title {
    font-size: 1.6rem;
  }
}
</style>
