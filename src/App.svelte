<script>
  import { onMount } from 'svelte';

  // Predefined negative situations with their positive flips
  const moodData = [
    {
      id: 1,
      negative: "I'm stuck in traffic",
      positive: "🚗 Congratulations! You've been selected for a free meditation session! Your car is now a zen pod. Use this time to practice your Grammy acceptance speech or plan your next vacation. Traffic jams are just life's way of saying 'slow down and enjoy the radio!'"
    },
    {
      id: 2,
      negative: "I spilled coffee on my shirt",
      positive: "☕ You've just created a unique, one-of-a-kind fashion statement! Coffee stains are the new tie-dye. You're basically a walking work of art now. Plus, you smell like a cozy café - people will want to hang around you all day!"
    },
    {
      id: 3,
      negative: "My phone battery died",
      positive: "🔋 Your phone has given you the gift of digital detox! You're now free from the tyranny of notifications. This is your chance to make eye contact with humans, notice the sky, or rediscover the ancient art of... thinking. You're living like royalty from the 1990s!"
    },
    {
      id: 4,
      negative: "I'm running late",
      positive: "⏰ You're not late, you're making a grand entrance! Fashionably late is a classic for a reason. You're building suspense, creating anticipation. When you arrive, everyone will be so happy to see you that they'll forget about the time!"
    },
    {
      id: 5,
      negative: "I failed a test",
      positive: "📚 Plot twist: You didn't fail, you just found multiple ways that don't work! You're basically a scientist now. Edison failed 1,000 times before inventing the light bulb. You're in excellent company! This is just your origin story."
    },
    {
      id: 6,
      negative: "I got rejected",
      positive: "💫 Rejection is just redirection in disguise! You've been saved from settling for less than you deserve. The universe is clearing the path for something amazing. Think of it as a cosmic 'swipe left' - your perfect match is still out there!"
    },
    {
      id: 7,
      negative: "It's raining on my day off",
      positive: "🌧️ Mother Nature has declared it an official cozy day! You now have a legitimate excuse to stay in pajamas, drink hot chocolate, and binge-watch that series. The earth is getting a spa day, and so should you!"
    },
    {
      id: 8,
      negative: "I burnt my dinner",
      positive: "🍳 You've just activated the 'Plan B' protocol! Time for takeout, which means no dishes to wash and food that actually tastes good. You've accidentally given yourself a night off from cooking. Sometimes the best meals are the ones we don't make!"
    },
    {
      id: 9,
      negative: "I lost my keys",
      positive: "🔑 Your keys have gone on an adventure without you! They're probably making friends with other lost items in the mysterious 'Lost Things Dimension.' This is the perfect excuse to clean your house/bag/car - you might find treasures you forgot you had!"
    },
    {
      id: 10,
      negative: "I have to work overtime",
      positive: "💰 Overtime means overtime pay! You're essentially getting paid to level up your skills. Think of it as being so awesome at your job that they literally can't function without you. You're the office superhero - cape not included, but definitely earned!"
    }
  ];

  let selectedMood = null;
  let showPositive = false;
  let currentPositive = '';

  function selectMood(mood) {
    selectedMood = mood;
    showPositive = false;
  }

  function flipMood() {
    if (selectedMood) {
      currentPositive = selectedMood.positive;
      showPositive = true;
    }
  }

  function resetMood() {
    selectedMood = null;
    showPositive = false;
    currentPositive = '';
  }
</script>

<main class="min-vh-100">
  <!-- Header -->
  <header class="app-header py-4 mb-4">
    <div class="container">
      <div class="text-center">
        <h1 class="display-4 fw-bold text-primary mb-2">
          🌟 MoodFlip 🌟
        </h1>
        <p class="lead text-muted">
          Turn your worst moments into your best laughs!
        </p>
      </div>
    </div>
  </header>

  <div class="container">
    <div class="row">
      <!-- Left Column - Mood Selection -->
      <div class="col-lg-6 mb-4">
        <div class="card shadow-sm h-100">
          <div class="card-header bg-primary text-white">
            <h3 class="card-title mb-0">
              <i class="bi bi-emoji-frown"></i>
              What's bringing you down?
            </h3>
          </div>
          <div class="card-body mood-grid">
            <div class="row g-3">
              {#each moodData as mood}
                <div class="col-12">
                  <div 
                    class="card mood-card {selectedMood?.id === mood.id ? 'selected' : ''}"
                    on:click={() => selectMood(mood)}
                    role="button"
                    tabindex="0"
                  >
                    <div class="card-body py-3">
                      <p class="mb-0 fw-medium">
                        {mood.negative}
                      </p>
                    </div>
                  </div>
                </div>
              {/each}
            </div>
          </div>
          <div class="card-footer text-center">
            <button 
              class="btn btn-warning btn-lg flip-button"
              disabled={!selectedMood}
              on:click={flipMood}
            >
              <span class="fw-bold">✨ Flip It! ✨</span>
            </button>
          </div>
        </div>
      </div>

      <!-- Right Column - Positive Response -->
      <div class="col-lg-6">
        <div class="card shadow-sm h-100">
          <div class="card-header bg-success text-white">
            <h3 class="card-title mb-0">
              <i class="bi bi-emoji-smile"></i>
              Your mood makeover!
            </h3>
          </div>
          <div class="card-body d-flex align-items-center justify-content-center">
            {#if !showPositive}
              <div class="text-center text-muted">
                <div class="mb-4">
                  <i class="bi bi-arrow-left display-1"></i>
                </div>
                <h4>Select a situation and flip it!</h4>
                <p>Choose what's bothering you and watch the magic happen ✨</p>
              </div>
            {:else}
              <div class="positive-response p-4 rounded-3 w-100">
                <div class="text-center mb-3">
                  <h4 class="text-success fw-bold">
                    🎉 Mood Flipped! 🎉
                  </h4>
                </div>
                <p class="lead mb-4">
                  {currentPositive}
                </p>
                <div class="text-center">
                  <button 
                    class="btn btn-outline-primary"
                    on:click={resetMood}
                  >
                    Try Another One!
                  </button>
                </div>
              </div>
            {/if}
          </div>
        </div>
      </div>
    </div>

    <!-- Fun Facts Footer -->
    <div class="row mt-5">
      <div class="col-12">
        <div class="card bg-light">
          <div class="card-body text-center">
            <h5 class="card-title text-primary">💡 Fun Fact</h5>
            <p class="card-text">
              Studies show that reframing negative thoughts can actually rewire your brain to be more optimistic. 
              You're literally training your brain to be happier! 🧠✨
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</main>

<style>
  .min-vh-100 {
    min-height: 100vh;
  }
</style>