<script setup>
import { ref } from 'vue';
import { defineProps } from 'vue';


const { activeStates } = defineProps(['activeStates']);

const handleStates = (item) => {
    item.state = !item.state //este podria causar problemas

    const setInactive = activeStates.filter(inactive => inactive.name !== item.name)

    for (const inactive of setInactive) {
        inactive.state = false
    }
}
</script>
<template>
    <div class="card-header">
        <div class="data-user">
            <div class="container-user-profile">
                <img src="../images/image-jeremy.png" alt="profile picture">
            </div>
            <div class="container-user-data">
                <p class="user-tittle text-small">Report for</p>
                <span class="user-name text-big">Jeremy Robson</span>
            </div>
        </div>
        <div class="options">
            <button v-for="item in activeStates" :key="item.name" class="btn-option text-small "
                @click="handleStates(item)">
                <!-- :class="[activeStates.daily ? 'active' : 'inactive']" -->
                <span :class="[item.state ? 'active' : 'inactive']">{{ item.name }}</span>
            </button>
        </div>
    </div>
</template>

<style scoped>
.card-header {
    background: var(--darkBlue);
    border-radius: 20px;
    overflow: hidden;
}

.data-user {
    background: var(--blue);
    padding: 1.5rem;
    border-radius: 15px;
    display: grid;
    grid-auto-flow: column;
    grid-template-columns: 1fr 2fr;
}

.container-user-profile {
    width: 80px;
    height: 80px;
    overflow: hidden;
    border: 2.5px solid #ffff;
    border-radius: 50%;
}

.container-user-profile img {
    width: 100%;
}

.container-user-data {
    padding-top: 8px;
}

.user-tittle {
    color: var(--paleBlue);
}

.user-name {
    color: #ffff;
    font-weight: 300;
}

.active {
    color: #ffff;
}

.inactive {
    color: var(--desaturatedBlue);
}

.options {
    padding: 15px 0px 15px 0px;
    display: grid;
    grid-auto-flow: column;
    justify-content: space-evenly;
}

.options .btn-option {
    background: none;
    padding: 5px 10px 5px 10px;
    border: none;

    cursor: pointer;
}
</style>