<script setup>
import Header from './components/Header.vue'
import data from './data/data.json'
import {  reactive, computed } from 'vue';


//data.json
const reactiveData = reactive(data)



//array to switch the states, this help to create the "active button" in the heather component
//based on this array i wanna render the data
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

//i need to create a new object depending on the active data?

//how do i render only de daily, weekly or monthly if i cannot do this: {{data.timeframes.active.name.current}}

</script>

<template>
    <main>
        <div class="grid-container">
            <!--User Data component -->
            <Header :activeStates="activeStates" />
            <!--activities -->
            <div class="activity-card" v-for="data in reactiveData" :key="data.title">
                <div class="data-activity">
                    <div class="current-activity">
                        <p class="activity">{{ data.title }}</p>
                        <span class="time text-bigger">{{ data.timeframes.daily.current}}hrs </span>
                    </div>
                    <div class="last-week-activity">
                        <button class="btn-option">
                            <img src="./images/icon-ellipsis.svg" alt="" srcset="">
                        </button>
                        <p class="last-week-data text-small">Last week - 36hrs</p>
                    </div>
                </div>

            </div>
        </div>
    </main>
</template>

<style scoped>
.grid-container {
    display: grid;
    gap: 23px;
}

.activity-card {
    background-color: var(--lightRedWork);
    background-image: url(./images/icon-work.svg);
    background-repeat: no-repeat;
    background-position: top -8px right 15px;
    background-size: 3.2rem;
    border-radius: 20px;
    overflow: hidden;

    /*por el momento */
    padding-top: 30px;
}

.data-activity {
    background: var(--darkBlue);
    border-radius: 15px;
    display: grid;
    padding: 18px 16px 22px 16px;
    grid-auto-flow: column;
    grid-template-columns: 1fr 1fr;
}

.current-activity .activity {
    color: #ffff;
    font-weight: 500;
}

.current-activity .time {
    color: #ffff;
    font-weight: 300;
}

.last-week-activity {
    text-align: right;
}

.last-week-activity .btn-option {
    padding-bottom: 3px;
    background: none;
    border: none;
    cursor: pointer;
}

.last-week-activity .last-week-data {
    padding-top: 10px;
    color: var(--paleBlue);
}
</style>
