<template>
    <section id="stats" class="stats-strip">
        <div class="container">
            <div class="stats-grid">
                <div class="stats-item" v-for="(stat, index) in stats" :key="index">
                    <div class="stat-value">{{ stat.value }}</div>
                    <div class="stat-label">{{ stat.label }}</div>
                    <div class="stat-sub">{{ stat.unit }}</div>
                </div>
            </div>
        </div>
    </section>
</template>
<script setup>
import ruffianFeatures from '../../data/ruffian-features.json'; 

const stats = ruffianFeatures.highlights;
</script>
<style scoped lang="scss">
@use '../../styles/_variables' as *;
.stats-grid{
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    text-align: center;
}
@media (max-width: 1024px) {
    .stats-grid {
        grid-template-columns: repeat(2, 1fr);
    }
}
.stats-item {
    padding: $sp-4 $sp-3;
    border-right: 1px solid $esab-gray-1;
}
.stats-item:last-child {
    border-right: none;
}
@media (max-width: 1024px) {
    .stats-item:last-child {
        border-right: 1px solid $esab-gray-1;
    }
}

.stat-value {
    font-size: 28px;
    font-weight: $fw-bolder;
    line-height: 1.1;
    color: $esab-yellow;
}
.stat-label {
    font-size: $ft-14;
    color: rgba($esab-white, 0.65);
    font-weight: $fw-medium;
    margin-top: $sp-1;
}
.stat-sub {
    font-size: $ft-12;
    color: rgba($esab-white, 0.35);
    margin-top: 2px;
}
</style>