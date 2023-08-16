<script setup>
defineProps({
  word: String,
  maxAttempts: Number,
  attempts: Array
})

const letterClass = (word, letter, letterPosition) => {
  if (typeof letter !== 'string') {
    return ''
  }

  if (word[letterPosition] === letter) {
    return 'word-grid__letter--correct'
  }

  if (word.includes(letter)) {
    return 'word-grid__letter--misplaced'
  }

  return 'word-grid__letter--incorrect'
}
</script>

<template>
  <div class="word-grid">
    <div v-for="attemptIteration in maxAttempts" class="word-grid__word">
      <span v-for="(letter, key) in word.length"
            :class="['word-grid__letter', letterClass(word, attempts?.[attemptIteration - 1]?.[letter-1], key)]">
        <template v-if="attempts[attemptIteration - 1]">
          {{ attempts[attemptIteration - 1][key] }}
        </template>
      </span>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.word-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
  width: min-content;
  margin: 1rem auto;
  font-weight: bold;

  &__word {
    display: flex;
    gap: inherit;
    width: 100%;
    justify-content: stretch;
  }

  &__letter {
    background: var(--default-color, white);
    color: var(--default-dark-color, black);
    width: 4rem;
    border: 1px solid black;
    height: 4rem;
    display: inline-block;
    text-align: center;
    line-height: 4rem;
    font-size: 2rem;
    text-transform: uppercase;
    border-radius: var(--default-border-radius);

    &--correct {
      background-color: var(--success-color, green);
      transition: var(--background-transition);
    }

    &--misplaced {
      background-color: var(--notice-color, yellow);
      transition: var(--background-transition);
    }

    &--incorrect {
      background-color: var(--incorrect-color, gray);
      transition: var(--background-transition);
    }
  }
}
</style>
