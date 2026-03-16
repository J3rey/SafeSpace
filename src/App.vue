<template>
  <div id="app" class="w-100 app-shell has-bottom-nav">
    <router-view />
    <BottomNav />
  </div>
</template>

<script>
import BottomNav from "./components/BottomNav.vue";

export default {
  name: "AppShell",
  components: { BottomNav },
};
</script>

<style>
.app-shell {
  background: var(--surface);
}

.has-bottom-nav {
  /* Reserve space for the mobile bottom nav to prevent overlap */
  padding-bottom: 88px;
}

@media (min-width: 992px) {
  .has-bottom-nav {
    padding-bottom: 0;
  }
}
</style>
