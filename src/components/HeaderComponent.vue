<template>
    <header class="header">
        <div class="logo" 
            title="[ESAB logo — site provides]">
        </div>
        <nav class="nav-header">
            <ul>
                <li v-for="item in menuItems" :key="item.id">
                    <button @click="handleClick(item.id)">
                        {{ item.label }}
                    </button>
                </li>
            </ul>
        </nav>        
        <div class="demoAction">
            <a href="#demo" class="btn btn-primary">REQUEST DEMO</a>
        </div>
    </header>
</template>

<script setup>
import { defineEmits } from 'vue';

    const emit = defineEmits(['navigate'])
    const menuItems = [
        { id: 'productAndSolutions', label: 'Products & Solutions' },
        { id: 'weldingEquipment', label: 'Welding Equipment' },
        { id: 'support', label: 'Support' },
        { id: 'about', label: 'About' }
    ];
    const handleClick = (id) => {
        emit('navigate', id)
    };

</script>

<style scoped lang="scss">
@use '../styles/variables' as *;
.header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: sticky;
    top: 0;
    z-index: 100;
    background: $esab-black;
    border-bottom: 3px solid $esab-yellow;
    padding: 0 $gutter;
}
.logo {
    width: 110px;
    height: 34px;
    background: rgba($primary-color, 0.15);
    border: 2px dashed $wf-border;
    border-radius: $radius;
    border-color: rgba($primary-color, 0.3);
}
.nav-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 64px;
    gap: $sp-4;
}
ul {
    display: flex;
    gap: $sp-4;
    font-weight: $fw-medium;
    font-size: $ft-14;
    list-style-type: none;
    padding: 0;
    margin: 0;

    li button {
        color: $esab-white;
        opacity: 0.7;
        font-weight: 600;
        font-size: $ft-14;
        border: none;
        cursor: pointer;
        background: none;
    }

    li button:hover {
        color: $esab-yellow;
        opacity: 1;
    }
}
a {
    text-decoration: none;
}
.btn-primary {    
    padding: 10px 20px;
    font-weight: $fw-bold;
    font-size: 13px;
}
</style>