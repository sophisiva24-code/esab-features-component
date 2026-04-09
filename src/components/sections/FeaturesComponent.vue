<template>
  <section id="features" class="section-features">
    <div class="container">
      <div class="section-header">
          <div class="section-tag">Features & Benefits</div>
          <h2 class="section-title">Engineered for Superior Welding Performance</h2>
          <p class="section-desc">
              More than 100 customer-requested features packed into the most capable engine-driven welder in its class.
          </p>
      </div>
      <div class="filter-tabs-wrapper">
        <FilterComponent :categories="categories" :activeCategory="activeCategory" @change="handleFilterChange"/>
      </div>
      <div class="toggle">
        <p @click="isGridView = !isGridView">
          {{ isGridView ? 'View Less' : 'View All' }}
        </p>
      </div>
      
        <!-- Slider -->
      <div v-if="!isGridView">
        <SliderComponent :cards="filteredCards" />
      </div>

      <!-- Grid -->
      <div v-else class="grid">
        <FeatureCardComponent
          v-for="card in filteredCards"
          :key="card.id"
          :card="card"
        />
      </div>
    </div>
  </section>
</template>
<script setup>
import FilterComponent from '../shared/FilterComponent.vue';
import { ref, computed } from 'vue';
import ruffianFeatures from '../../data/ruffian-features.json'; 
import SliderComponent from '../shared/SliderComponent.vue';
import FeatureCardComponent from '../shared/FeatureCardComponent.vue'


const cards = ref(ruffianFeatures.features)
const activeCategory = ref('all')
const isGridView = ref(false)

const filteredCards = computed(() => {
  if (activeCategory.value === 'all') return cards.value

  return cards.value.filter(
    card => card.category.toLowerCase() === activeCategory.value
  )
})

const handleFilterChange = (categoryId) => {
  activeCategory.value = cards.value.find(card => card.category.toLowerCase() === categoryId)?.category.toLowerCase() || 'all'
}

const categories = ruffianFeatures.categories.map((category) => ({
  id: category.toLowerCase(),
  name: category
}))
</script>
<style scoped lang="scss">
@use '../../styles/_variables' as *;

.filter-tabs-wrapper {
  display: flex;
  justify-content: center;
  margin-bottom: $sp-5;
}
.grid {
  position: relative;
  top: $sp-2;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: $sp-4;
  padding: 0px $sp-2;
}
@media (max-width: 1024px) {
  .grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .grid {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
  }
}
.toggle {
  display: flex; 
  justify-content: flex-end; 
  padding: 0px $sp-3;
  p {
    color: $cta-text;
    font-weight: $fw-medium;
    cursor: pointer;
    font-size: $ft-14;
  }
  & p:hover {
    text-decoration: underline;
  }
}
</style>