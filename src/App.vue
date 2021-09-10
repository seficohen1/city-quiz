<template>
  <div class="ctr">
      <transition name="fade" mode="out-in">
        <questions v-if="questionsAnswered < questions.length" :questions="questions" :questionsAnswered="questionsAnswered" @question-answered="questionAnswered"></questions>
        <results v-else :results="results" :totalCorrect="totalCorrect"></results>
      </transition>
    <button type="button" class="reset-btn" @click.prevent="reset" v-show="questionsAnswered === questions.length">Reset</button>
</div>
</template>

<script>
import Questions from './components/Question.vue'
import Results from './components/Result.vue'
export default {
  name: 'App',
  components: {
      Questions,
      Results,
  },
  data() {
    return {
      totalCorrect: 0,
      questionsAnswered: 0,
      questions: [
        {
            q: 'What is the capital of Norway?', 
            answers: [
                {
                    text: 'Stavanger',
                    is_correct: false
                },
                {
                    text: 'Malmö',
                    is_correct: false 
                },
                {
                    text: 'Bergen',
                    is_correct: false 
                },
                {
                    text: 'Oslo',
                    is_correct: true 
                }
            ] 
        },
        { 
            q: 'What is the capital of Spain?', 
            answers: [
                {
                    text: 'Valencia',
                    is_correct: false
                },
                {
                    text: 'Barcelona',
                    is_correct: false 
                },
                {
                    text: 'Madrid',
                    is_correct: true 
                },
                {
                    text: 'Sevilla',
                    is_correct: false 
                }
            ] 
        },
        { 
            q: 'What is the capital of New York?', 
            answers: [
                {
                    text: 'New York City',
                    is_correct: false
                },
                {
                    text: 'Albany',
                    is_correct: true 
                },
                {
                    text: 'Buffalo',
                    is_correct: false 
                },
                {
                    text: 'None of the above',
                    is_correct: false 
                }
            ] 
        },
    ],
      results: [
          {
              min: 0,
              max: 2,
              title: "Try again!",
              desc: "Do a little more studying and you may succeed!"
          },
          {
              min: 3,
              max: 3,
              title: "Wow, you're a genius!",
              desc: "Studying has definitely paid off for you!"
          }
      ]
    }
  },
  methods: {
      reset() {
          this.totalCorrect = 0
          this.questionsAnswered = 0
      },
      questionAnswered(correctAnswer) {
          if (correctAnswer) {
              this.totalCorrect++
          }
          this.questionsAnswered++
      }
  }
}
</script>

<style>

</style>
