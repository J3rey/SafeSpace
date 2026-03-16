<template>
  <nav class="bottom-nav" aria-label="Primary navigation">
    <router-link class="nav-item" to="/" aria-label="Home">
      <span class="icon" aria-hidden="true">🏠</span>
      <span class="label">Home</span>
    </router-link>
    <router-link class="nav-item" to="/mood" aria-label="Mood tracking">
      <span class="icon" aria-hidden="true">📈</span>
      <span class="label">Mood</span>
    </router-link>
    <router-link class="nav-item" to="/interactive-tools" aria-label="Guided exercises">
      <span class="icon" aria-hidden="true">🧘</span>
      <span class="label">Guides</span>
    </router-link>
    <router-link class="nav-item" to="/community-chat" aria-label="Community chat">
      <span class="icon" aria-hidden="true">💬</span>
      <span class="label">Chat</span>
    </router-link>
    <router-link class="nav-item" to="/notifications" aria-label="Notifications">
      <span class="icon" aria-hidden="true">🔔</span>
      <span class="label">Alerts</span>
    </router-link>
    <router-link class="nav-item" to="/profile" aria-label="Profile and settings">
      <span class="icon" aria-hidden="true">👤</span>
      <span class="label">Profile</span>
    </router-link>
  </nav>
</template>

<script>
export default {
  name: "BottomNav",
};
</script>

<style scoped>
.bottom-nav {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 0.25rem;
  background: var(--surface-strong, #ffffff);
  border-top: 1px solid rgba(44, 110, 178, 0.14);
  box-shadow: var(--shadow-soft, 0 10px 24px rgba(44, 110, 178, 0.12));
  padding: 0.5rem 0.75rem calc(env(safe-area-inset-bottom) + 0.35rem);
  z-index: 1000;
}

.nav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.15rem;
  text-decoration: none;
  color: var(--text-muted, #475569);
  padding: 0.35rem 0.25rem;
  border-radius: 12px;
  transition: background 0.2s ease, transform 0.2s ease, color 0.2s ease;
  font-weight: 600;
  font-size: 0.8rem;
}

.nav-item .icon {
  font-size: 1.1rem;
}

.nav-item.router-link-active {
  background: rgba(44, 110, 178, 0.12);
  color: var(--brand-primary, #2c6eb2);
  transform: translateY(-2px);
}

.nav-item:hover {
  background: rgba(44, 110, 178, 0.1);
  color: var(--brand-primary, #2c6eb2);
}

@media (min-width: 992px) {
  /* Hide mobile nav on desktop to reduce navigation duplication with header */
  .bottom-nav {
    display: none;
  }
}
</style>
