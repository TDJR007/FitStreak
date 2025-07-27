// File: FitStreak/src/components/Grid.vue

<script setup>
import dumbbell from "@/assets/dumbbell-solid-full.svg";
import weightHanging from "@/assets/weight-hanging-solid-full.svg";
import bolt from "@/assets/bolt-solid-full.svg";
import refresh from "@/assets/rotate-left-solid-full.svg";

import { workoutProgram } from "@/utils";
// console.log(workoutProgram);

const props = defineProps({
    handleSelectWorkout: Function,
    firstIncompleteWorkoutIndex: Number,
    handleResetPlan: Function,
});

const workoutTypes = ['Push', 'Pull', 'Legs'];

</script>

<template>
    <section id="grid">
        <button :disabled="workoutIdx > 0 && workoutIdx > firstIncompleteWorkoutIndex"
            @click="handleSelectWorkout(workoutIdx)" :key="workoutIdx"
            v-for="(workout, workoutIdx) in Object.keys(workoutProgram)" class="card-button plan-card">
            <div>
                <p>Day {{ workoutIdx < 9 ? '0' + (workoutIdx + 1) : workoutIdx + 1 }}</p>
                        <img :src="dumbbell" alt="dumbbell icon" width="24" height="24" v-if="workoutIdx % 3 === 0">
                        <img :src="weightHanging" alt="weight hanging icon" width="24" height="24"
                            v-if="workoutIdx % 3 === 1">
                        <img :src="bolt" alt="bolt icon" width="24" height="24" v-if="workoutIdx % 3 === 2">
            </div>
            <h3>{{ workoutTypes[workoutIdx % 3] }}</h3>
        </button>

        <button :disabled="firstIncompleteWorkoutIndex != -1" @click="handleResetPlan" class="card-button plan-card-reset">
            <p>Reset</p>
            <img :src="refresh" alt="refresh icon" width="24" height="24">
        </button>
    </section>
</template>

<style scoped>
#grid {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 1rem;
}

#grid button {
    width: 100%;
}

#grid button:disabled {
    box-shadow: none;
    cursor: not-allowed;
}

.plan-card {
    display: flex;
    flex-direction: column;
}

.plan-card-reset {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1rem;
}

.plan-card div {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
}

.plan-card div p {
    text-align: left;
}

@media (min-width: 640px) {
    #grid {
        grid-template-columns: repeat(4, minmax(0, 1fr));
    }
}
</style>
