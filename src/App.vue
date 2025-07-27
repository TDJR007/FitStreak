// File: FitStreak/src/App.vue

<script setup>
import Welcome from '@/components/pages/Welcome.vue'
import Layout from '@/components/layout/Layout.vue';
import Dashboard from '@/components/pages/Dashboard.vue';
import Workout from '@/components/pages/Workout.vue';

import { computed, ref, onMounted } from 'vue';
import { workoutProgram } from '@/utils';

const defaultData = {}
for (let workoutIdx in workoutProgram) {
  const workoutData = workoutProgram[workoutIdx];
  // create a for loop where we iterate over every workout
  defaultData[workoutIdx] = {} // initialize the workout data object

  // nested loop to loop over every exercise in the workout and initialize it's input value to an empty string
  for (let e of workoutData.workout) {
    defaultData[workoutIdx][e.name] = ''
  }

  // console.log(defaultData);
}
const selectedDisplay = ref(1);
const data = ref(defaultData); // {1....30: {"exercise_name": "", .....}}
const selectedWorkout = ref(-1);

const isWorkoutComplete = computed(() => {
  const currWorkout = data.value?.[selectedWorkout.value];
  if (!currWorkout) { return false }; // guard clause to exit function

  const isCompleteCheck = Object.values(currWorkout).every(ex => !!ex);
  console.log("IS COMPLETE: ", isCompleteCheck);
  return isCompleteCheck;
})

const firstIncompleteWorkoutIndex = computed(() => {
  const allWorkouts = data.value;

  if (!allWorkouts) return -1;
  // loop over every key value pair and check if the workout is complete or not
  for (const [index, workout] of Object.entries(allWorkouts)) {
    const isComplete = Object.values(workout).every(ex => !!ex);
    if (!isComplete) {
      return parseInt(index); // return the first incomplete workout index
    }
  }
  return -1; // if all workouts are complete, return -1
})

function handleChangeDisplay(idx) {
  selectedDisplay.value = idx;
}

function handleSelectWorkout(Idx) {
  selectedDisplay.value = 3;
  selectedWorkout.value = Idx;
}

function handleSaveWorkout() {
  // save the current data snapshot to localStorage so that we can retrieve it next time
  localStorage.setItem('workouts', JSON.stringify(data.value));

  // show the dashboard
  selectedDisplay.value = 2;

  // deselect a workout
  selectedWorkout.value = -1;
}

function handleResetPlan() {
  selectedDisplay.value = 2;
  selectedWorkout.value = -1;
  data.value = defaultData;
  localStorage.removeItem('workouts');
}

onMounted(() => {
  if (!localStorage) { return; }
  // Load the workouts from localStorage if they exist
  const savedData = localStorage.getItem('workouts');
  if (savedData) {
    data.value = JSON.parse(savedData);
    selectedDisplay.value = 2; // if the user has data we don't want to show the welcome screen every time they load the app
  }
});

</script>

<template>
  <Layout>
    <!--PAGE 1-->
    <Welcome :handleChangeDisplay="handleChangeDisplay" v-if="selectedDisplay == 1" />
    <!--PAGE 2-->
    <Dashboard :handleResetPlan="handleResetPlan" :firstIncompleteWorkoutIndex="firstIncompleteWorkoutIndex"
      :handleSelectWorkout="handleSelectWorkout" v-if="selectedDisplay == 2" />
    <!--PAGE 3-->
    <Workout :isWorkoutComplete="isWorkoutComplete" :handleSaveWorkout="handleSaveWorkout" :data="data"
      :selectedWorkout="selectedWorkout" v-if="workoutProgram?.[selectedWorkout]" />
  </Layout>
</template>

<style scoped></style>
