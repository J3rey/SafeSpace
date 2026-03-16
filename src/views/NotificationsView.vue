<template>
  <div class="notifications-view">
    <MainHeader />

    <main class="content py-3 py-sm-4 py-md-5 px-2 px-sm-3 px-md-4" role="main">
      <section class="container-fluid px-3">
        <div class="row justify-content-center">
          <div class="col-12 col-lg-10">
            <div class="header-block">
              <p class="eyebrow">Notifications</p>
              <h1 class="title">Stay updated with calm, focused alerts.</h1>
              <p class="subtitle">Gentle reminders for journal, challenges, and community replies. No noise.</p>
            </div>

            <div class="card surface-card feed">
              <div class="feed-row" v-for="item in items" :key="item.id">
                <div class="icon" :class="item.type" aria-hidden="true">{{ item.icon }}</div>
                <div class="body">
                  <p class="heading">{{ item.title }}</p>
                  <p class="muted">{{ item.time }}</p>
                </div>
                <button class="btn btn-ghost small" type="button">Mark read</button>
              </div>
              <div v-if="items.length === 0" class="empty">You are all caught up. ✨</div>
            </div>

            <div class="card surface-card prefs">
              <div class="panel-head">
                <p class="eyebrow mb-1">Preferences</p>
                <h2 class="panel-title">Alert channels</h2>
              </div>
              <div class="toggle" v-for="pref in preferences" :key="pref.key">
                <label>
                  <input type="checkbox" v-model="pref.enabled" />
                  <span>{{ pref.label }}</span>
                </label>
                <p class="muted">{{ pref.desc }}</p>
              </div>
            </div>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
import { reactive } from "vue";
import MainHeader from "../components/MainHeader.vue";

export default {
  name: "NotificationsView",
  components: { MainHeader },
  setup() {
    const items = reactive([
      { id: 1, title: "New daily challenge is ready", time: "Just now", type: "challenge", icon: "⭐" },
      { id: 2, title: "Moderator shared a calming tip", time: "12 min ago", type: "info", icon: "💬" },
      { id: 3, title: "Journal reminder", time: "1 hr ago", type: "journal", icon: "📔" },
    ]);

    const preferences = reactive([
      { key: "journal", label: "Journal reminders", desc: "One gentle ping per day to log mood.", enabled: true },
      { key: "challenge", label: "Daily challenges", desc: "Alert when a new guided exercise is live.", enabled: true },
      { key: "chat", label: "Community replies", desc: "Notify when someone replies in your room.", enabled: false },
    ]);

    return { items, preferences };
  },
};
</script>

<style scoped>
.notifications-view {
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

.header-block {
  background: var(--gradient-soft, linear-gradient(135deg, rgba(44, 110, 178, 0.12), rgba(168, 200, 228, 0.18)));
  border-radius: 16px;
  padding: 1.25rem 1.4rem;
  box-shadow: var(--shadow-soft, 0 10px 24px rgba(44, 110, 178, 0.12));
  margin-bottom: 1rem;
}

.eyebrow {
  text-transform: uppercase;
  letter-spacing: 0.08em;
  font-size: 0.85rem;
  color: var(--brand-primary, #2c6eb2);
  margin-bottom: 0.35rem;
  font-weight: 700;
}

.title {
  font-weight: 700;
  font-size: 1.9rem;
  margin: 0 0 0.35rem;
}

.subtitle {
  color: var(--text-muted, #475569);
  margin: 0;
}

.card {
  border-radius: var(--radius-base, 16px);
  padding: 1rem;
}

.feed {
  display: grid;
  gap: 0.75rem;
}

.feed-row {
  display: grid;
  grid-template-columns: auto 1fr auto;
  gap: 0.75rem;
  align-items: center;
}

.icon {
  width: 38px;
  height: 38px;
  border-radius: 12px;
  display: grid;
  place-items: center;
  font-size: 1.1rem;
  background: rgba(44, 110, 178, 0.12);
}

.icon.challenge {
  background: rgba(44, 110, 178, 0.15);
}

.icon.info {
  background: rgba(116, 169, 216, 0.18);
}

.icon.journal {
  background: rgba(168, 200, 228, 0.2);
}

.body .heading {
  margin: 0;
  font-weight: 700;
}

.muted {
  color: var(--text-muted, #475569);
  margin: 0;
}

.btn {
  border-radius: 999px;
  padding: 0.55rem 1rem;
  font-weight: 700;
  text-decoration: none;
  border: 1px solid transparent;
  transition: all 0.2s ease;
  background: transparent;
  cursor: pointer;
}

.btn-ghost.small,
.btn.small {
  padding: 0.45rem 0.9rem;
  font-size: 0.9rem;
}

.prefs {
  margin-top: 1rem;
  display: grid;
  gap: 0.75rem;
}

.panel-head {
  border-bottom: 1px solid rgba(44, 110, 178, 0.14);
  padding-bottom: 0.4rem;
}

.panel-title {
  margin: 0;
  font-weight: 700;
}

.toggle {
  background: rgba(44, 110, 178, 0.05);
  border-radius: 12px;
  padding: 0.8rem;
  border: 1px solid rgba(44, 110, 178, 0.12);
}

.toggle label {
  font-weight: 700;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.empty {
  color: var(--text-muted, #475569);
  text-align: center;
  padding: 0.5rem 0;
}
</style>
