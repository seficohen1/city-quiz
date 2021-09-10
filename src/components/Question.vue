<template>
      <div class="questions-ctr">
        <div class="progress">
            <div class="bar" :style="{width: `${(questionsAnswered / questions.length) * 100 }%`}" ></div>
            <div class="status">{{questionsAnswered}} out of {{questions.length}} questions answered</div>
        </div>
        <transition-group name="fade">
            <div class="single-question" v-for="(question, qi) in questions" :key="question.q" v-show="questionsAnswered === qi" >
                <div class="question">{{question.q}}</div>
                <div class="answers" v-for="answer in question.answers" :key="answer.t" @click.prevent="selectAnswer(answer.is_correct)">
                    <div class="answer" >{{answer.text}}</div>
                </div>
            </div>
        </transition-group>
    </div>
</template>

<script>
export default {
  props: ['questions', 'questionsAnswered'],
  data() {
      return {
          correctAnswers: 0
      }
  },
  emits: ['question-answered'],
  methods: {
      selectAnswer(correctAnswer) {
        this.$emit('question-answered', correctAnswer)
  }
}
}
</script>
