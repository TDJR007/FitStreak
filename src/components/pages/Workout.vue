// File: src/components/pages/Workout.vue

<script setup>
import { ref, computed } from "vue";
import Portal from "@/components/Portal.vue";
import { workoutProgram, exerciseDescriptions } from "@/utils";
import dumbbell from "@/assets/dumbbell-solid-full.svg";
import questionIcon from "@/assets/circle-question-regular-full.svg";
import saveIcon from "@/assets/floppy-disk-solid-full.svg";
import checkIcon from "@/assets/check-solid-full.svg";
import crossIcon from "@/assets/xmark-solid-full.svg";

const workoutType = ["Push", "Pull", "Legs"];

const { data, selectedWorkout } = defineProps({
    data: Object,
    selectedWorkout: Number,
    handleSaveWorkout: Function,
    isWorkoutComplete: Boolean,
});

// console.log(workoutProgram);
const { workout, warmup } = workoutProgram[selectedWorkout];

let selectedExercise = ref(null);  // This would be set when a user clicks on a question button
// console.log(selectedExercise);
const exerciseDescription = computed(() => exerciseDescriptions[selectedExercise.value])

function handleCloseModal() {
    selectedExercise.value = null;
}

</script>

<template>
    <Portal hello="world" :handleCloseModal="handleCloseModal" v-if="selectedExercise">
        <div class="exercise-description">
            <h3> {{ selectedExercise }}</h3>
            <div>
                <small>Description</small>
                <p>{{ exerciseDescription }}</p>
            </div>
            <button @click="handleCloseModal">Close<img :src="crossIcon" alt="close icon" width="24"
                    height="24"></button>
        </div>
    </Portal>

    <section id="workout-card">
        <div class="plan-card card">
            <div class="plan-card-header">
                <p>Day {{ selectedWorkout < 9 ? '0' + (selectedWorkout + 1) : (selectedWorkout + 1) }}</p>
                        <img :src="dumbbell" alt="dumbbell icon" width="24" height="24">
            </div>
            <h2>{{ workoutType[selectedWorkout % 3] }} Workout</h2>
        </div>

        <div class="workout-grid">
            <h4 class="grid-name">Warmup</h4>
            <h6>Sets</h6>
            <h6>Reps</h6>
            <h6 class="grid-weights">Weights</h6>

            <div class="workout-grid-row" v-for="(w, wIdx) in warmup" :key="wIdx">
                <div class="grid-name">
                    <p>{{ w.name }}</p>
                    <button class="question-btn" @click="selectedExercise = w.name">
                        <img :src="questionIcon" alt="question icon" width="24" height="24">
                    </button>
                </div>
                <p>{{ w.sets }}</p>
                <p>{{ w.reps }}</p>
                <input class="grid-weights" placeholder="14kg" type="text" disabled />
            </div>

            <div class="workout-grid-line"></div>

            <h4 class="grid-name">Workout</h4>
            <h6>Sets</h6>
            <h6>Reps</h6>
            <h6 class="grid-weights">Weights</h6>

            <div class="workout-grid-row" v-for="(w, wIdx) in workout" :key="wIdx">
                <div class="grid-name">
                    <p>{{ w.name }}</p>
                    <button class="question-btn" @click="selectedExercise = w.name">
                        <img :src="questionIcon" alt="question icon" width="24" height="24">
                    </button>
                </div>
                <p>{{ w.sets }}</p>
                <p>{{ w.reps }}</p>
                <input v-model="data[selectedWorkout][w.name]" class="grid-weights" placeholder="14kg" type="text" />
            </div>
        </div>

        <div class="card workout-btns">
            <button @click="handleSaveWorkout">Save & Exit <img :src="saveIcon" alt="save icon" width="32" height="32"></button>
            <button :disabled="!isWorkoutComplete" @click="handleSaveWorkout">Complete <img :src="checkIcon" alt="check icon" width="32" height="32"></button>
        </div>

    </section>

</template>

<style scoped>
#workout-card,
.plan-card {
    display: flex;
    flex-direction: column;
}

#workout-card {
    gap: 1.5rem;
}

.plan-card-header,
.workout-btns {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 1rem;
}

.workout-grid,
.workout-grid-row {
    display: grid;
    grid-template-columns: repeat(7, minmax(0, 1fr));
    gap: 1rem;
}

.workout-grid-row,
.workout-grid-line {
    grid-column: span 7 / span 7;
}

.workout-grid-line {
    margin: 0.5rem 0;
    height: 3px;
    border-radius: 2px;
    background: var(--background-muted);
}

.grid-name {
    grid-column: span 3 / span 3;
    display: flex;
    align-items: center;
    gap: 1rem;
}

.question-btn {
    padding: 0;
    border: none;
    box-shadow: none;
    position: relative;
    width: 24px;
    height: 24px;
}

.question-btn img {
    opacity: 0;
    position: absolute;
    top: 0;
    left: 0;
}

.question-btn::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 24px;
    height: 24px;
    background-color: currentColor;
    mask: url('@/assets/circle-question-regular-full.svg') no-repeat center;
    mask-size: contain;
    -webkit-mask: url('@/assets/circle-question-regular-full.svg') no-repeat center;
    -webkit-mask-size: contain;
    transition: background-color 0.2s ease;
}

.question-btn:hover::after {
    background-color: var(--color-link);
}

.question-btn:hover {
    transform: none;
    box-shadow: none;
}

.workout-grid-row .question-btn {
    opacity: 0;
    pointer-events: none;
}

.workout-grid-row:hover .question-btn {
    opacity: 1;
    pointer-events: all;
}

.grid-name p {
    text-transform: capitalize;
}

.grid-weights {
    grid-column: span 2 / span 2;
}

.workout-btns button {
    flex: 1;
}

.workout-btns button img {
    padding-left: 0.5rem;
}

.exercise-description {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    width: 100%;
}

.exercise-description h3 {
    text-transform: capitalize;
}

.exercise-description button img {
    padding-left: 0.5rem;
}
</style>