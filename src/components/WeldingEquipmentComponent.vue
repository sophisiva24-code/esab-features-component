<template>
  <div>
    <HeroComponent />
    <StatsComponent />
    <FeaturesComponent />
    <RequestDemoComponent />
  </div>
</template>

<script setup>
import HeroComponent from './sections/HeroComponent.vue';
import StatsComponent from './sections/StatsComponent.vue';
import FeaturesComponent from './sections/FeaturesComponent.vue';
import RequestDemoComponent from './sections/RequestDemoComponent.vue';
</script>

<style scoped lang="scss">
@use '../styles/_variables' as *;
.section-hero {
  background: $esab-black-2;
  color: $esab-white;
  padding: $sp-8 0 0;
  overflow: hidden;
}
.stats-strip {
  background: $esab-black;
  color: $esab-white;
  padding: 0;
}
.section-features {
  padding: $sp-8 0;
  color: $cta-text;
}
.section-demo {
  background: $esab-black-3;
  color: $esab-white;
  padding: $sp-8 0;
}
</style>