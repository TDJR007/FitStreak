// File: src/components/pages/Welcome.vue

<script setup>
    defineProps({
        handleChangeDisplay: Function,
    });

</script>

<template>
    <Section id="welcome">
        <div class="benifits">
            <h2>Complete this program<br />if you want...</h2>
            <div>
                <p>✅ Follow a simple program with proven results.</p>
                <p>✅ Get fit, healthy, strong and absolutely shredded.</p>
                <p>✅ Learn more about gym, training and technique.</p>
            </div>

            <div>
                <h3>The Training Plan</h3>
                <p>This training plan follows a structure known as the
                    <strong>Bro Split</strong>.
                </p>
                <h5><i>Push &rarr; Pull &rarr; Legs &rarr; Repeat</i></h5>
            </div>
            <div class="card challenge">
                <h3>🔥 Your Challenge</h3>
                <p>Complete all the workouts and track your progress along the way!</p>
                <p>Do you accept?</p>
                <button @click="() => handleChangeDisplay(2)">Begin &rarr;</button>
            </div>
        </div>
    </Section>
</template>

<style scoped>
#welcome,
.challenge,
.benifits {
    display: flex;
    flex-direction: column;
}

#welcome {
    gap: 1.5rem;
}

.benifits {
    gap: 0.5rem;
}

.challenge {
    gap: 0.25rem;
}

@media (min-width: 640px) {
    #welcome {
        gap: 2rem;
        padding: 2rem 0;
    }

    .benifits {
        gap: 1rem;
    }
}
</style>
