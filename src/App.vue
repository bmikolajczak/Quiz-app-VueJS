<template>
  <div class="ctr">
      
    <transition-group name="fade">
        <home v-if="startFlag==true" @started="started"></home>
        <questions v-if="questionsAnswered<questions.length && startFlag==false" 
        :questions="questions"
        :questionsAnswered="questionsAnswered"
        @question-answered="questionAnswered"></questions>
        
        <result v-else-if="questionsAnswered>=questions.length && startFlag==false" :results="results" :totalCorrect="totalCorrect"></result>
    </transition-group>
    <button type="button" class="reset-btn" @click.prevent="reset" v-if="questionsAnswered===questions.length">Reset Quiz</button>
</div>
</template>

<script>
import Questions from './components/Questions.vue'
import Result from './components/Result.vue'
import Home from './components/Home.vue'
export default {
  name: 'App',
  components:{Questions,Result,Home},
  data(){
    return{
      questionsAnswered:0,
      totalCorrect:0,
      startFlag:true,
      questions: [
          {
              q: 'What is 2 + 2?', 
              answers: [
                  {
                      text: '4',
                      is_correct: true
                  },
                  {
                      text: '3',
                      is_correct: false 
                  },
                  {
                      text: '1',
                      is_correct: false 
                  },
                  {
                      text: '5',
                      is_correct: false 
                  }
              ] 
          },
          { 
              q: 'What is √9?', 
              answers: [
                  {
                      text: '6',
                      is_correct: false
                  },
                  {
                      text: '2.333',
                      is_correct: false 
                  },
                  {
                      text: '3',
                      is_correct: true 
                  },
                  {
                      text: '3.3',
                      is_correct: false 
                  }
              ] 
          },
          { 
              q: 'what is 2+(3+5)*6', 
              answers: [
                  {
                      text: '49',
                      is_correct: false
                  },
                  {
                      text: '50',
                      is_correct: true 
                  },
                  {
                      text: '51',
                      is_correct: false 
                  },
                  {
                      text: '48',
                      is_correct: false
                  }
              ] 
          },
          { 
              q: 'what is √9+√4', 
              answers: [
                  {
                      text: '5',
                      is_correct: true
                  },
                  {
                      text: '6',
                      is_correct: false 
                  },
                  {
                      text: '4',
                      is_correct: false 
                  },
                  {
                      text: '9',
                      is_correct: false
                  }
              ] 
          },
          { 
              q: 'what is 100*12+√9', 
              answers: [
                  {
                      text: '1200',
                      is_correct: false
                  },
                  {
                      text: '1202',
                      is_correct: false 
                  },
                  {
                      text: '1203',
                      is_correct: true 
                  },
                  {
                      text: '1204',
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
              max: 5,
              title: "Great job!",
              desc: "You did well but there's still room for improvement, is it?"
          },
          {
              min: 5,
              max: 5,
              title: "You're a genius!!!",
              desc: "Someone has been studying really hard lately!"
          },

      ]
    }
  },
methods:{
    questionAnswered(is_correct){
      if(is_correct){
        this.totalCorrect++;
      }
      this.questionsAnswered++;
    },
    reset(){
        this.questionsAnswered=0;
        this.totalCorrect=0;
    },
    started(){
        this.startFlag=!this.startFlag;
    }
  }

}

</script>

