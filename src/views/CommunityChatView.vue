<template>
  <div class="community-chat">
    <MainHeader />

    <main class="content py-3 py-sm-4 py-md-5 px-2 px-sm-3 px-md-4" role="main">
      <section class="hero container-fluid px-3">
        <div class="row justify-content-center align-items-center g-3 g-md-4">
          <div class="col-12 col-lg-7">
            <p class="eyebrow">Community chat</p>
            <h1 class="hero-title">A calm, moderated space to share and support.</h1>
            <p class="hero-subtitle">Light-touch prompts, clear boundaries, and quick reporting keep this space safe and respectful.</p>
            <div class="d-flex flex-column flex-sm-row gap-2">
              <a class="btn primary" href="#chat" aria-label="Jump to chat window">Jump to chat</a>
              <a class="btn ghost" href="#rules" aria-label="View community rules">View rules</a>
            </div>
          </div>
          <div class="col-12 col-lg-5">
            <div class="safety-card" id="rules" aria-label="Community safety rules">
              <h2 class="card-title">Safety rules</h2>
              <ul>
                <li>No identifying info; use first names only.</li>
                <li>Support over advice; ask before offering steps.</li>
                <li>Flag crisis words to mods automatically.</li>
                <li>Use the "Need support" toggle for moderator check-ins.</li>
              </ul>
            </div>
          </div>
        </div>
      </section>

      <section id="chat" class="container-fluid px-3 py-4 py-md-5" aria-label="Chat interface">
        <div class="row g-3 g-md-4 justify-content-center">
          <div class="col-12 col-lg-4">
            <div class="panel">
              <h2 class="panel-title">Rooms</h2>
              <ul class="room-list" role="list">
                <li v-for="room in rooms" :key="room.id" :class="['room', room.id === activeRoom ? 'active' : '']" @click="setRoom(room.id)" tabindex="0" role="button" :aria-pressed="room.id === activeRoom">
                  <div class="room-name">{{ room.name }}</div>
                  <p class="room-desc">{{ room.desc }}</p>
                </li>
              </ul>
            </div>
          </div>
          <div class="col-12 col-lg-8">
            <div class="chat-window">
              <div class="chat-header d-flex align-items-center justify-content-between">
                <div>
                  <p class="eyebrow mb-1">Room</p>
                  <h3 class="chat-title">{{ activeRoomName }}</h3>
                </div>
                <label class="support-toggle">
                  <input type="checkbox" v-model="needsSupport" />
                  <span>Need support check-in</span>
                </label>
              </div>

              <div class="message-list" role="log" aria-live="polite">
                <div v-for="message in visibleMessages" :key="message.id" :class="['message', message.sender === 'You' ? 'self' : 'peer']">
                  <div class="meta">
                    <span class="sender">{{ message.sender }}</span>
                    <span class="time">{{ message.time }}</span>
                  </div>
                  <p class="body">{{ message.text }}</p>
                </div>
              </div>

              <form class="composer" @submit.prevent="sendMessage" aria-label="Send a message">
                <div class="input-shell">
                  <input
                    v-model="draft"
                    type="text"
                    placeholder="Share a thought, question, or encouragement..."
                    aria-label="Message text"
                  />
                </div>
                <button class="btn primary" type="submit" :disabled="draft.trim() === ''">Send</button>
              </form>
            </div>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
import { ref, computed } from "vue";
import MainHeader from "../components/MainHeader.vue";

export default {
  name: "CommunityChatView",
  components: { MainHeader },
  setup() {
    const rooms = ref([
      { id: "check-ins", name: "Daily check-ins", desc: "Light updates and encouragement." },
      { id: "grounding", name: "Grounding space", desc: "Share breathing or calming ideas." },
      { id: "study", name: "Study and focus", desc: "Cozy accountability and breaks." },
    ]);
    const messages = ref([
      { id: 1, room: "check-ins", sender: "Mia", time: "10:12", text: "Starting the day with 5 deep breaths. Anyone joining?" },
      { id: 2, room: "check-ins", sender: "Ravi", time: "10:13", text: "Yes! Did a short stretch, feeling calmer." },
      { id: 3, room: "grounding", sender: "Leah", time: "09:55", text: "Box breathing helped during a tough call." },
      { id: 4, room: "study", sender: "Jon", time: "09:40", text: "25-minute focus timer on. Break at :05?" },
    ]);
    const activeRoom = ref("check-ins");
    const draft = ref("");
    const needsSupport = ref(false);

    const activeRoomName = computed(() => rooms.value.find((r) => r.id === activeRoom.value)?.name || "");

    const visibleMessages = computed(() => messages.value.filter((m) => m.room === activeRoom.value));

    const setRoom = (roomId) => {
      activeRoom.value = roomId;
      draft.value = "";
    };

    const sendMessage = () => {
      if (draft.value.trim() === "") return;
      const id = Date.now();
      messages.value.push({
        id,
        room: activeRoom.value,
        sender: "You",
        time: new Date().toLocaleTimeString([], { hour: "2-digit", minute: "2-digit" }),
        text: draft.value.trim(),
      });
      draft.value = "";
    };

    return {
      rooms,
      messages,
      activeRoom,
      draft,
      needsSupport,
      activeRoomName,
      visibleMessages,
      setRoom,
      sendMessage,
    };
  },
};
</script>

<style scoped>
.community-chat {
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
  background: linear-gradient(135deg, rgba(44, 110, 178, 0.14), rgba(116, 169, 216, 0.14));
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

.safety-card {
  background: white;
  border: 1px solid #e5e7eb;
  border-radius: 14px;
  padding: 1.4rem;
  box-shadow: 0 10px 24px rgba(15, 23, 42, 0.08);
}

.safety-card ul {
  padding-left: 1.2rem;
  color: #4b5563;
}

.card-title {
  margin: 0 0 0.75rem;
  font-weight: 700;
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

.btn:hover {
  transform: translateY(-1px);
  box-shadow: 0 8px 18px rgba(15, 23, 42, 0.08);
}

.panel, .chat-window {
  background: white;
  border: 1px solid rgba(44, 110, 178, 0.12);
  border-radius: 14px;
  padding: 1.25rem;
  box-shadow: var(--shadow-soft, 0 10px 24px rgba(44, 110, 178, 0.12));
  height: 100%;
}

.panel-title {
  font-weight: 700;
  margin-bottom: 0.75rem;
}

.room-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  gap: 0.5rem;
}

.room {
  padding: 0.75rem 0.9rem;
  border: 1px solid #e5e7eb;
  border-radius: 10px;
  background: #f8fafc;
  cursor: pointer;
  transition: all 0.2s ease;
}

.room:hover {
  border-color: #5b8def;
}

.room.active {
  border-color: #5b8def;
  background: rgba(91, 141, 245, 0.12);
}

.room-name {
  font-weight: 700;
  margin-bottom: 0.2rem;
}

.room-desc {
  margin: 0;
  color: #4b5563;
}

.chat-window {
  display: grid;
  grid-template-rows: auto 1fr auto;
  gap: 1rem;
  min-height: 520px;
}

.chat-header {
  border-bottom: 1px solid #e5e7eb;
  padding-bottom: 0.75rem;
}

.chat-title {
  margin: 0;
  font-weight: 700;
}

.support-toggle {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  font-weight: 600;
  color: #2563eb;
}

.message-list {
  background: #f8fafc;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 1rem;
  overflow-y: auto;
  display: grid;
  gap: 0.75rem;
}

.message {
  background: white;
  border: 1px solid rgba(44, 110, 178, 0.12);
  border-radius: 10px;
  padding: 0.75rem;
  box-shadow: 0 4px 12px rgba(44, 110, 178, 0.08);
}

.message.self {
  border-color: #c7d2fe;
  background: rgba(91, 141, 245, 0.08);
}

.meta {
  display: flex;
  justify-content: space-between;
  font-size: 0.85rem;
  color: #6b7280;
  margin-bottom: 0.25rem;
}

.body {
  margin: 0;
  color: #0f172a;
}

.composer {
  display: flex;
  gap: 0.75rem;
  align-items: center;
}

.input-shell {
  flex: 1;
  background: #f8fafc;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 0.75rem 0.9rem;
}

.input-shell input {
  width: 100%;
  border: none;
  background: transparent;
  outline: none;
  font-size: 1rem;
}

@media (max-width: 991.98px) {
  .chat-window {
    min-height: 420px;
  }
}
</style>
