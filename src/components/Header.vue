<script setup>
import { ref } from 'vue';
import { defineProps } from 'vue';

//array with the three states for the 'active buttons'
const { activeStates } = defineProps(['activeStates']);

//set the active state to true and set the other ones to false
const handleStates = (item) => {
    item.state = !item.state

    const setInactive = activeStates.filter(inactive => inactive.name !== item.name)

    for (const inactive of setInactive) {
        inactive.state = false
    }
}
</script>
<template>
    <div class="card-header row-span-2">
        <div class="data-user">
            <div class="container-user-profile">
                <div class="user-profile">
                    <img src="../images/image-jeremy.png" alt="profile picture">
                </div>
            </div>
            <div class="container-user-data">
                <p class="user-tittle text-small">Report for</p>
                <span class="user-name text-big">Jeremy Robson</span>
            </div>
        </div>
        <div class="options">
            <button v-for="item in activeStates" :key="item.name" class="btn-option" role="button" aria-label="timeframe"
                @click="handleStates(item)">
                <span class="text-small" :class="[item.state ? 'active' : 'inactive']">{{ item.name }}</span>
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

.user-profile {
    width: 80px;
    height: 80px;
    overflow: hidden;
    border: 2.5px solid #ffff;
    border-radius: 50%;
}

.user-profile img {
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
    line-height: 8px;
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


@media(min-width: 768px) {
    .row-span-2 {
        grid-row: span 2;
    }

    .data-user {
        padding: 1.5rem 1.5rem 2rem 1.5rem;
        display: grid;
        grid-auto-flow: row;
        grid-template-columns: none;
    }

    .container-user-profile {
        padding-bottom: 18px;
    }

    .user-profile {
        width: 70px;
        height: 70px;
        border: 2.5px solid #ffff;
        border-radius: 50%;
    }

    .user-tittle {
        padding-bottom: 4px;
    }

    .options {
        padding: 15px 0px 15px 16px;
        display: grid;
        grid-auto-flow: row;
        justify-content: start;

    }

    .options .btn-option {
        background: none;
        padding: 3px 10px 3px 10px;
        text-align: left;
    }

}
</style>