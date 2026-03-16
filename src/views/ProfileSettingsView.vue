<template>
  <div class="profile-settings">
    <MainHeader />

    <main class="content py-3 py-sm-4 py-md-5 px-2 px-sm-3 px-md-4" role="main">
      <section class="container-fluid px-3">
        <div class="row justify-content-center">
          <div class="col-12 col-lg-10 col-xl-8">
            <div class="header-block surface-card">
              <p class="eyebrow">Profile and preferences</p>
              <h1 class="title">Keep your SafeSpace personal, calm, and secure.</h1>
              <p class="subtitle">Manage display info, notifications, and safety options with a few taps.</p>
            </div>

            <div class="grid">
              <form class="panel surface-card" @submit.prevent="saveProfile" aria-label="Profile information">
                <div class="panel-header">
                  <div>
                    <p class="eyebrow mb-1">Account</p>
                    <h2 class="panel-title">Profile details</h2>
                  </div>
                  <span class="pill">Private</span>
                </div>

                <label class="field">
                  <span>Display name</span>
                  <input v-model="profile.displayName" type="text" required aria-required="true" />
                </label>

                <label class="field">
                  <span>Email</span>
                  <input v-model="profile.email" type="email" required aria-required="true" />
                </label>

                <label class="field">
                  <span>Role</span>
                  <select v-model="profile.role">
                    <option value="youth">Youth</option>
                    <option value="advisor">Advisor</option>
                    <option value="caregiver">Caregiver</option>
                  </select>
                </label>

                <div class="actions">
                  <button class="btn btn-ghost" type="button" @click="resetProfile">Reset</button>
                  <button class="btn btn-brand" type="submit">Save changes</button>
                </div>
                <p v-if="statusMessage" class="status">{{ statusMessage }}</p>
              </form>

              <div class="panel surface-card" aria-label="Notifications and safety">
                <div class="panel-header">
                  <div>
                    <p class="eyebrow mb-1">Preferences</p>
                    <h2 class="panel-title">Notifications and safety</h2>
                  </div>
                </div>

                <div class="toggle">
                  <label>
                    <input type="checkbox" v-model="preferences.journalReminders" />
                    <span>Daily journal reminders</span>
                  </label>
                  <p class="muted">Gentle prompts once a day to log mood and gratitude.</p>
                </div>

                <div class="toggle">
                  <label>
                    <input type="checkbox" v-model="preferences.challengeAlerts" />
                    <span>Daily challenge alerts</span>
                  </label>
                  <p class="muted">Notifies when a new guided challenge is ready.</p>
                </div>

                <div class="toggle">
                  <label>
                    <input type="checkbox" v-model="preferences.moderatorCheckIns" />
                    <span>Moderator check-ins</span>
                  </label>
                  <p class="muted">Allows moderators to reach out when "Need support" is enabled.</p>
                </div>

                <div class="divider"></div>

                <div class="safety-box">
                  <div>
                    <p class="eyebrow mb-1">Safety</p>
                    <h3>Quick calm toolkit</h3>
                    <p class="muted">Save three go-to actions for tough moments. We keep them handy in chat and journaling.</p>
                  </div>
                  <ul>
                    <li v-for="(tool, index) in preferences.toolkit" :key="index">{{ tool }}</li>
                  </ul>
                  <button class="btn btn-ghost" type="button" @click="shuffleToolkit">Shuffle ideas</button>
                </div>
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

const defaultProfile = {
  displayName: "Alex",
  email: "alex@safespace.app",
  role: "youth",
};

const defaultPreferences = {
  journalReminders: true,
  challengeAlerts: true,
  moderatorCheckIns: true,
  toolkit: ["4-7-8 breathing", "Text a friend", "Step outside for 3 minutes"],
};

export default {
  name: "ProfileSettingsView",
  components: { MainHeader },
  setup() {
    const profile = reactive({ ...defaultProfile });
    const preferences = reactive({ ...defaultPreferences });
    const statusMessage = ref("");

    const saveProfile = () => {
      statusMessage.value = "Saved. Preferences are stored on this device.";
      setTimeout(() => {
        statusMessage.value = "";
      }, 2000);
    };

    const resetProfile = () => {
      Object.assign(profile, defaultProfile);
      Object.assign(preferences, defaultPreferences);
      statusMessage.value = "Reset to defaults.";
      setTimeout(() => {
        statusMessage.value = "";
      }, 1500);
    };

    const shuffleToolkit = () => {
      const ideas = [
        "4-7-8 breathing",
        "Step outside for 3 minutes",
        "Write one gratitude",
        "Drink water and stretch",
        "Progressive muscle relaxation",
      ];
      preferences.toolkit = ideas.sort(() => 0.5 - Math.random()).slice(0, 3);
    };

    return {
      profile,
      preferences,
      statusMessage,
      saveProfile,
      resetProfile,
      shuffleToolkit,
    };
  },
};
</script>

<style scoped>
.profile-settings {
  font-family: Arial, sans-serif;
  background-color: var(--surface, #f7f9fc);
  min-height: 100vh;
  color: var(--text-primary, #0f172a);
}

.content {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.header-block {
  background: linear-gradient(135deg, rgba(91, 141, 245, 0.12), rgba(126, 200, 201, 0.12));
  border-radius: 16px;
  padding: 1.5rem;
  margin-bottom: 1rem;
}

.eyebrow {
  text-transform: uppercase;
  letter-spacing: 0.08em;
  font-size: 0.85rem;
  color: #5b708f;
  margin-bottom: 0.4rem;
}

.title {
  font-weight: 700;
  font-size: 2rem;
  margin: 0 0 0.4rem;
}

.subtitle {
  color: #4b5563;
  margin: 0;
}

.grid {
  display: grid;
  gap: 1rem;
}

@media (min-width: 992px) {
  .grid {
    grid-template-columns: 1fr 1fr;
  }
}

.panel {
  border-radius: 14px;
  padding: 1.25rem;
  display: grid;
  gap: 0.75rem;
}

.panel-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 0.75rem;
}

.panel-title {
  margin: 0;
  font-weight: 700;
}

.pill {
  background: rgba(91, 141, 245, 0.12);
  color: #0f172a;
  border-radius: 999px;
  padding: 0.35rem 0.9rem;
  font-weight: 600;
}

.field {
  display: grid;
  gap: 0.35rem;
}

.field span {
  font-weight: 600;
  color: #111827;
}

.field input,
.field select {
  border: 1px solid #e5e7eb;
  border-radius: 10px;
  padding: 0.65rem 0.8rem;
  font-size: 1rem;
  background: #f8fafc;
}

.actions {
  display: flex;
  gap: 0.6rem;
  flex-wrap: wrap;
}

.btn {
  border-radius: 999px;
  padding: 0.7rem 1.3rem;
  font-weight: 600;
  text-decoration: none;
  border: 1px solid transparent;
  transition: all 0.2s ease;
  display: inline-block;
  text-align: center;
}

.status {
  color: #2563eb;
  margin: 0;
}

.toggle {
  background: #f8fafc;
  border: 1px solid #e5e7eb;
  border-radius: 10px;
  padding: 0.9rem;
}

.toggle label {
  font-weight: 700;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #0f172a;
}

.muted {
  color: #4b5563;
  margin: 0.35rem 0 0;
}

.divider {
  height: 1px;
  background: #e5e7eb;
  margin: 0.75rem 0;
}

.safety-box {
  background: #0f172a;
  color: white;
  border-radius: 12px;
  padding: 1rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.safety-box ul {
  margin: 0.5rem 0 1rem;
  padding-left: 1.2rem;
  color: #cbd5e1;
}
</style>
