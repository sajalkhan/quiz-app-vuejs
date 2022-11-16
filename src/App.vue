<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <questions v-if="questionsAnswered < questions.length" :questions="questions"
        :questionsAnswered="questionsAnswered" @question-answered="questionAnswered" />
        
      <result v-else :results="results" :totalCorrect="totalCorrect" />
    </transition>

    <button type="button" class="reset-btn" @click.prevent="reset" v-if="questionsAnswered === questions.length">
      Reset
    </button>
  </div>
</template>

<script>
import Questions from "./components/Questions.vue";
import Result from "./components/Result.vue";
import { questions, results } from './constants';

export default {
  name: "App",
  components: {
    Questions,
    Result,
  },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions,
      results
    };
  },
  methods: {
    questionAnswered(is_correct) {
      if (is_correct) {
        this.totalCorrect++;
      }

      this.questionsAnswered++;
    },
    reset() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
    },
  },
};
</script>

<style>
.ctr {
  margin: 0 auto;
  max-width: 600px;
  width: 100%;
  box-sizing: border-box;
  position: relative;
}

.reset-btn {
  background-color: #ff6372;
  border: 0;
  font-size: 22px;
  color: #fff;
  padding: 10px 25px;
  margin: 10px auto;
  display: block;
}


.reset-btn:active,
.reset-btn:focus,
.reset-btn:hover {
  border: 0;
  outline: 0;
}

.fade-enter-from {
  opacity: 0;
}

.fade-enter-active {
  transition: all 0.3s linear;
}

.fade-leave-active {
  transition: all 0.3s linear;
  opacity: 0;
  position: absolute;
}

.fade-leave-to {
  opacity: 0;
}
</style>