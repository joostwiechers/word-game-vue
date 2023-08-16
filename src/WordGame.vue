<script setup>
import WordGrid from './WordGrid.vue'
import words from './words'
import {ref} from 'vue'
import Notification from './Notification.vue'

// Constants.
const MAX_ATTEMPTS = 6
const WORD_LENGTH = 5

// Game values.
const word = ref(words[Math.floor(Math.random() * words.length)])
const currentAttempt = ref('')
const attempts = ref([])

// Game-ending conditions.
const wordGuessed = ref(false)
const exhaustedAttempts = ref(false)

// Give cheater a hand.
console.log(word.value)

const setAttempt = e => {
  e.preventDefault()
  const attempt = currentAttempt.value

  if (attempt.length !== WORD_LENGTH) {
    return
  }

  attempts.value.push(attempt)
  currentAttempt.value = ''

  wordGuessed.value = attempts.value.includes(word.value)
  exhaustedAttempts.value = attempts.value.length === MAX_ATTEMPTS
}
</script>

<template>
  <Notification type="success" v-if="wordGuessed" message="Word has been guessed" />
  <Notification type="error" v-if="exhaustedAttempts && !wordGuessed" message="Word has not been guessed" />

  <WordGrid :attempts="attempts" :word="word" :max-attempts="MAX_ATTEMPTS" max-attempts="5" />

  <form v-on:submit="setAttempt">
    <input :disabled="wordGuessed || (exhaustedAttempts && !wordGuessed)" type="text" v-model="currentAttempt">
  </form>
</template>

<style lang="scss" scoped>
input {
  height: 4rem;
  font-size: 2rem;
  padding: 0 1rem;
  display: block;
  border-radius: 1rem;
  margin: 0 auto 1rem;
  border: 1px solid black;
}
</style>
