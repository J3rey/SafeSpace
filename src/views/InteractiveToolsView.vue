<template>
  <div class="interactive-tools-container">
    <MainHeader />

    <main
      id="main-content"
      class="tools-content py-3 py-sm-4 py-md-5 px-2 px-sm-3 px-md-4"
      role="main"
    >
      <div class="container-fluid px-3">
        <div class="row justify-content-center">
          <div class="col-12 col-lg-10 col-xl-9">
            <div class="content-wrapper surface-card p-3 p-md-5">
              <h1 class="sr-only">Interactive Mental Health Tools and Guides</h1>

              <div class="row g-4">
                <div class="col-12 col-lg-6">
                  <div class="tools-section" role="region" aria-labelledby="guides-heading">
                    <div class="section-header d-flex flex-column flex-md-row align-items-center text-center text-md-start">
                      <div class="section-icon me-0 me-md-3 mb-2 mb-md-0" aria-hidden="true">📋</div>
                      <h2 id="guides-heading" class="section-title">Step-by-Step Guides</h2>
                    </div>

                    <nav class="guides-list" aria-label="Step-by-step guides navigation">
                      <div class="guide-item">
                        <button
                          class="guide-btn surface-card"
                          @click="openGuide('wellbeing-map')"
                          aria-label="Open Wellbeing Map guide"
                        >
                          Wellbeing Map
                        </button>
                      </div>

                      <div class="guide-item">
                        <button
                          class="guide-btn surface-card"
                          @click="openGuide('healthy-sleep-habits')"
                          aria-label="Open Building Healthy Sleep Habits guide"
                        >
                          Building Healthy Sleep Habits
                        </button>
                      </div>

                      <div class="guide-item">
                        <button
                          class="guide-btn surface-card"
                          @click="openGuide('managing-stress')"
                          aria-label="Open Managing Stress guide"
                        >
                          Managing Stress
                        </button>
                      </div>

                      <div class="guide-item">
                        <button
                          class="guide-btn surface-card"
                          @click="openGuide('daily-positivity')"
                          aria-label="Open Daily Positivity Message guide"
                        >
                          Daily Positivity Message
                        </button>
                      </div>

                      <div class="guide-item">
                        <button
                          class="guide-btn surface-card"
                          @click="openGuide('mindful-reading')"
                          aria-label="Open Mindful Reading guide"
                        >
                          Mindful Reading
                        </button>
                      </div>
                    </nav>
                  </div>
                </div>

                <div class="col-12 col-lg-6">
                  <div class="tools-section" role="region" aria-labelledby="challenge-heading">
                    <div class="section-header d-flex flex-column flex-md-row align-items-center text-center text-md-start">
                      <div class="section-icon me-0 me-md-3 mb-2 mb-md-0" aria-hidden="true">⭐</div>
                      <h2 id="challenge-heading" class="section-title">Daily Challenge</h2>
                    </div>

                    <div class="challenge-card surface-card h-100">
                      <div class="challenge-content">
                        <div class="challenge-text">
                          <p>{{ dailyChallenge.text }}</p>
                        </div>

                        <div class="challenge-actions d-flex flex-column flex-md-row gap-3">
                          <button
                            class="btn btn-brand challenge-complete-btn"
                            @click="completeChallenge"
                            :disabled="challengeCompleted"
                          >
                            {{ challengeCompleted ? "✅ Completed!" : "Mark as Complete" }}
                          </button>

                          <button
                            class="btn btn-ghost challenge-new-btn"
                            @click="generateNewChallenge"
                            :disabled="loading"
                          >
                            {{ loading ? "Loading..." : "New Challenge" }}
                          </button>
                        </div>
                        <div v-if="fetchError" class="mt-2 text-danger">{{ fetchError }}</div>
                      </div>
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
import { ref, onMounted } from "vue";
import { useRouter } from "vue-router";
import MainHeader from "../components/MainHeader.vue";

export default {
  name: "InteractiveToolsView",
  components: {
    MainHeader,
  },
  setup() {
    const router = useRouter();
    const challengeCompleted = ref(false);
    const dailyChallenge = ref({
      text: "Loading your daily challenge...",
    });

    const loading = ref(false);
    const fetchError = ref(null);

    const GEMINI_API_KEY = import.meta.env.VITE_GEMINI_API_KEY || "";
    const MODEL_NAME = "gemini-2.0-flash-001";
    const GEMINI_API_URL = `https://generativelanguage.googleapis.com/v1/models/${MODEL_NAME}:generateContent?key=${GEMINI_API_KEY}`;

    const fallbackChallenges = [
      "Spend five minutes writing down three things you're grateful for today.",
      "Send a kind message to someone you appreciate.",
      "Take a 10-minute mindful walk and notice five calming details around you.",
      "Do a 5-minute breathing exercise: inhale 4, hold 4, exhale 6.",
      "Write a supportive note to your future self about something you're working on.",
      "Pause and stretch for three minutes, focusing on how your body feels.",
      "Listen to one favorite song without multitasking and notice how it makes you feel.",
    ];

    const getFallbackChallenge = () => {
      const index = Math.floor(Math.random() * fallbackChallenges.length);
      return fallbackChallenges[index];
    };

    const fetchGeminiChallenge = async () => {
      // If no API key is set, use a local fallback challenge silently.
      if (!GEMINI_API_KEY) {
        return { text: getFallbackChallenge(), fromFallback: true };
      }

      const prompt = "Generate a short, actionable daily positivity challenge that can be done in 5-15 minutes. Focus on gratitude, mindfulness, kindness, creativity, or connection. Make it one sentence only.";

      try {
        const response = await fetch(GEMINI_API_URL, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            contents: [
              {
                role: "user",
                parts: [{
                  text: prompt,
                }],
              },
            ],
            generationConfig: {
              temperature: 0.7,
              maxOutputTokens: 50,
              topP: 0.8,
              topK: 40,
            },
          }),
        });

        const responseText = await response.text();

        if (!response.ok) {
          throw new Error(`Gemini API error: ${response.status} ${response.statusText}`);
        }

        const data = JSON.parse(responseText);
        if (data.candidates && data.candidates[0] && data.candidates[0].content && data.candidates[0].content.parts) {
          const text = data.candidates[0].content.parts[0].text;
          const cleanedText = text.replace(/^[*#>\s-]+|[\n\r]+.*$/g, "").trim();
          return { text: cleanedText || getFallbackChallenge(), fromFallback: false };
        }

        throw new Error("Invalid response format from Gemini API");
      } catch (error) {
        return { text: getFallbackChallenge(), fromFallback: true };
      }
    };

    const completeChallenge = () => {
      challengeCompleted.value = true;
      const today = new Date().toDateString();
      localStorage.setItem(`challenge_completed_${today}`, "true");
    };

    const generateNewChallenge = async () => {
      challengeCompleted.value = false;
      const today = new Date().toDateString();
      localStorage.removeItem(`challenge_completed_${today}`);

      loading.value = true;
      fetchError.value = null;

      try {
        const { text, fromFallback } = await fetchGeminiChallenge();
        dailyChallenge.value.text = text;
        fetchError.value = fromFallback ? null : null;
      } catch (err) {
        fetchError.value = "Unable to generate a new challenge. Please try again later.";
        dailyChallenge.value.text = getFallbackChallenge();
      } finally {
        loading.value = false;
      }
    };

    const openGuide = (guideId) => {
      const routeMap = {
        "wellbeing-map": "/guides/wellbeing-map",
        "healthy-sleep-habits": "/guides/healthy-sleep-habits",
        "managing-stress": "/guides/managing-stress",
        "daily-positivity": "/guides/daily-positivity",
        "mindful-reading": "/guides/mindful-reading",
      };

      const routePath = routeMap[guideId];
      if (routePath) {
        router.push(routePath);
      }
    };

    onMounted(async () => {
      const today = new Date().toDateString();
      const completed = localStorage.getItem(`challenge_completed_${today}`);
      if (completed) {
        challengeCompleted.value = true;
      }

      loading.value = true;
      try {
        const { text } = await fetchGeminiChallenge();
        dailyChallenge.value.text = text;
        fetchError.value = null;
      } catch (err) {
        fetchError.value = "Unable to load daily challenge. Please try again later.";
        dailyChallenge.value.text = getFallbackChallenge();
      } finally {
        loading.value = false;
      }
    });

    return {
      challengeCompleted,
      dailyChallenge,
      completeChallenge,
      generateNewChallenge,
      openGuide,
      loading,
      fetchError,
    };
  },
};
</script>

<style scoped>
.interactive-tools-container {
  font-family: "Segoe UI", "Inter", system-ui, -apple-system, sans-serif;
  min-height: 100vh;
  background-color: var(--surface, #eaf2fa);
}

.tools-content {
  padding-top: 2rem;
}

.content-wrapper {
  border-radius: 20px;
  box-shadow: none;
}

.tools-section {
  height: 100%;
}

.section-header {
  margin-bottom: 1.5rem;
  padding-bottom: 1rem;
  border-bottom: 2px solid rgba(44, 110, 178, 0.12);
}

.section-icon {
  font-size: 2rem;
}

.section-title {
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--text-primary, #0f172a);
  margin: 0;
}

.guides-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.guide-item {
  width: 100%;
}

.guide-btn {
  width: 100%;
  border-radius: 16px;
  padding: 0.9rem 1.2rem;
  font-weight: 700;
  color: var(--text-primary, #0f172a);
  cursor: pointer;
  transition: transform 0.2s ease, box-shadow 0.2s ease, border-color 0.2s ease;
  text-align: center;
  font-size: 0.95rem;
  border: 1px solid rgba(44, 110, 178, 0.16);
  background: #fff;
}

.guide-btn:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-soft, 0 10px 24px rgba(44, 110, 178, 0.12));
  border-color: rgba(44, 110, 178, 0.35);
}

.challenge-card {
  border-radius: 16px;
  padding: 1.5rem;
  height: 100%;
  min-height: 200px;
  display: flex;
  align-items: center;
}

.challenge-content {
  width: 100%;
}

.challenge-text {
  margin-bottom: 1.5rem;
}

.challenge-text p {
  font-size: 1.05rem;
  line-height: 1.6;
  color: var(--text-muted, #475569);
  margin: 0;
  font-style: italic;
}

.challenge-actions {
  margin-top: 1rem;
}

.challenge-complete-btn:disabled,
.challenge-new-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}
</style>
