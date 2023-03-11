<script setup>
import { defineProps, ref } from 'vue';

const { data, activeStates }
    = defineProps(
        [
            'data',
            'activeStates'
        ]);







</script>
<template>
    <div class="activity-card">
        <div class="data-activity">
            <div class="current-activity">
                <p class="activity"></p>
                <span class="time text-bigger"  />
            </div>
            <div class="last-week-activity">
                <button class="btn-option">
                    <img src="../images/icon-ellipsis.svg" alt="" srcset="">
                </button>
                <p class="last-week-data text-small"></p>
            </div>
        </div>
    </div>
</template>
<style scoped>
.activity-card {
    background-color: var(--lightRedWork);
    background-image: url(../images/icon-work.svg);
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