<template>
  <div class="hero-section">
    <div class="hero-overlay"></div>
    <v-container class="hero-content fill-height">
      <v-row align="start" justify="start">
        <v-col cols="12" md="8" lg="6">
          <h1 class="hero-title font-weight-bold mb-4">
            One Stop Shop for Construction Permits
          </h1>
          <p class="hero-subtitle mb-8">
            Fast, Efficient, and Convenient Permit Processing for Naga City
          </p>
          <div class="d-flex">
            <v-btn color="#2962FF" dark large depressed class="hero-btn" to="/login">
              Apply Now
            </v-btn>
          </div>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  name: "HeroSection",
};
</script>

<style scoped>
.hero-section {
  /* Assumes the image 'bg.png' is in the 'src/assets' directory */
  background-image: url("@/assets/bg.png");
  background-size: cover;
  background-position: center center;
  position: relative;
  width: 100vw;
  height: 100vh;
  color: white;
}

.hero-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5); /* Dark overlay */
  z-index: 1;
}

.hero-content {
  position: relative;
  z-index: 2;
  text-align: left;
  padding-top: 100px; /* Pushes content down from the top */
}

.hero-title {
  font-size: 3.5rem;
  line-height: 1.2;
  text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.7);
}

.hero-subtitle {
  font-size: 1.25rem;
  font-weight: 300;
  max-width: 500px;
  text-shadow: 1px 1px 4px rgba(0, 0, 0, 0.7);
}

.hero-btn {
  text-transform: none;
  font-weight: 600;
  font-size: 1rem;
  border-radius: 4px;
  height: 50px !important;
  padding: 0 32px !important;
}

/* Responsive adjustments for smaller screens */
@media (max-width: 960px) {
  .hero-title {
    font-size: 2.5rem;
  }
  .hero-subtitle {
    font-size: 1.1rem;
  }
}
</style>
