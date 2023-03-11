<script setup>
import Header from './components/Header.vue'
import Activity from './components/Activity.vue'
import data from './data/data.json'
import { ref } from 'vue';

const reactiveData = ref(data)

const activeStates = ref([
  { name: "daily", state: false },
  { name: "weekly", state: true },
  { name: "monthly", state: false }
])

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
                <span class="time text-bigger" v-text="`${data.timeframes.daily.current}hrs`"  />
            </div>
            <div class="last-week-activity">
                <button class="btn-option">
                    <img src="../images/icon-ellipsis.svg" alt="" srcset="">
                </button>
                <p class="last-week-data text-small"></p>
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
