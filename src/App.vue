<script setup>
import Header from './components/Header.vue'
import data from './data/data.json'
import { reactive, computed } from 'vue';


//data.json
const reactiveData = reactive(data)

//array to switch the states, this help to create the "active button" in the header component
const activeStates = reactive([
    { name: "Daily", state: false },
    { name: "Weekly", state: true },
    { name: "Monthly", state: false }
])

//return the current state
const active = computed(() => {
    const currentActive = activeStates.find(element => element.state === true)

    return currentActive
})

</script>

<template>
    <main>
        <div class="grid-container">
            <!--User Data component -->
            <Header :activeStates="activeStates" />
            <!--activities -->
            <div v-for="data in reactiveData" :key="data.title"
                :style="{ backgroundImage: 'url(' + data.image + ')', backgroundColor: data.bgcolor }"
                class="activity-card">
                <div class="data-activity">
                    <div class="data-activity-header">
                        <span class="data-title">{{ data.title }}</span>
                        <button class="data-option" role="button" aria-label="Options Button">
                            <img src="./images/icon-ellipsis.svg" alt="" srcset="">
                        </button>
                    </div>
                    <div class="stats-data">
                        <!-- CURRENT HOURS -->
                        <span class="text-big current-hours" v-if="active.name === 'Weekly'">
                        {{ data.timeframes.weekly.current }}hrs</span>
                        <span class="text-big current-hours" v-else-if="active.name === 'Daily'">
                        {{ data.timeframes.daily.current }}hrs</span>
                        <span class="text-big current-hours" v-else-if="active.name === 'Monthly'">
                        {{ data.timeframes.monthly.current }}hrs</span>
                        <!-- PREVIOUS HOURS -->
                        <span class="text-small previous-hours" v-if="active.name === 'Weekly'">Last Week - 
                        {{ data.timeframes.weekly.previous }}hrs</span>
                        <span class="text-small previous-hours" v-if="active.name === 'Daily'">Last Week - 
                        {{ data.timeframes.daily.previous }}hrs</span>
                        <span class="text-small previous-hours" v-if="active.name === 'Monthly'">Last Week - 
                        {{ data.timeframes.monthly.previous }}hrs</span>
                    </div>
                </div>
            </div>
        </div>
    </main>
</template>

<style scoped>
.grid-container {
    max-width: 820px;
    margin: 0 auto;
    display: grid;
    gap: 23px;
}

.activity-card {
    background-repeat: no-repeat;
    background-position: top -8px right 15px;
    background-size: 3.2rem;
    border-radius: 20px;
    overflow: hidden;
    padding-top: 30px;
}

.data-activity {
    background: var(--darkBlue);
    border-radius: 15px;
    display: grid;
    padding: 18px 16px 22px 16px;
}

.data-activity:hover{
    background: var(--desaturatedBlue);
}

.data-activity-header {
    display: flex;
    justify-content: space-between;
}

.data-title {
    color: #ffff;
    font-weight: 400;
}

.data-option {
    background: none;
    border: none;
    cursor: pointer;
    color: var(--paleBlue);
}


.stats-data {
    display: flex;
    justify-content: space-between;
    padding-top: 2px;
}

.current-hours {
    color: #ffff;
    font-weight: 200;
}

.previous-hours {
    color: var(--paleBlue);
    margin-top: 4px;
}

@media (min-width: 768px) {
    .grid-container {
        grid-template-columns: 1fr 1fr 1fr 1fr;
        padding-top: 50px;
    }

    .activity-card {
        position: relative;
    }

    .data-activity {
        display: grid;
        padding: 14px 16px 14px 16px;
        position: absolute;
        bottom: 0;
        width: 100%;
    }

    .stats-data {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        padding-top: 2px;
    }

    .current-hours {
        display: block;
        width: 100%;
    }

    .previous-hours {
        margin-top: 0px;
    }

}
</style>
