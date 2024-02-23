<template>
  <img src="./assets/logo.png">
  <Points :zastepy="zastepy"/>
  <button class="app-btn" @click="nextZastep">Następny zastęp</button>
  <button class="app-btn" @click="nextQuestion">Następne pytanie</button>
  <Question @addPoints="addPoints" :questions="questionsJson.questions"/>
</template>

<script>
import questionsJson from './assets/questions.json'
import Points from './components/Points.vue'
import Question from './components/Question.vue'

export default {
  name: 'App',
  components: { Points, Question },
  data(){
    return{
      questionsJson: questionsJson,
      zastepy:[
        {name: "Cool Kiwi", points: 0, answering: true},
        {name: "Dzienne Sówki", points: 0, answering: false},
        {name: "Gryzące Komary", points: 0, answering: false},
        {name: "Nocne Sówki", points: 0, answering: false}
      ],
      answeringIndex: 0,
      playedIndex: null
    }
  },
  methods:{
    nextZastep(){
      this.answeringIndex === 3 ? this.answeringIndex = 0 : this.answeringIndex++
      this.zastepy.forEach((zastep) => {
        zastep.answering = false
      })
      this.zastepy[this.answeringIndex].answering = true
    },
    nextQuestion(){
      if(this.playedIndex === null){
        this.playedIndex = 0
      } else {
        this.playedIndex++
      }
      this.questionsJson.questions.forEach((question) => {
        question.played = false
      })
      this.questionsJson.questions[this.playedIndex].played = true
      console.log(this.questionsJson)
    },
    addPoints(index){
      this.zastepy.forEach((zastep) => {
        if(zastep.answering){
          zastep.points += this.questionsJson.questions[this.playedIndex].answers[index].points
        }
      })
    }
  }
}
</script>

<style lang="scss">
$fontsize: 1.3rem;
$mainorange: #e9a425;
$transition: all .2s ease-in-out;

#app{
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}
.app-btn{
  border: $mainorange 3px solid;
  width: 10%;
  height: 60px;
  font-size: $fontsize;
  cursor: pointer;
  background: none;
  transition: $transition;
  &:hover{
    transform: translateY(-5px);
  }
}
</style>
