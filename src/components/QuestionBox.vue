<template>
<div>
  <b-jumbotron>
    <template v-slot:header>Are you intelligent enough ?</template>

    <template v-slot:lead>
        {{currentQuestion.question}}
    </template>

    <hr class="my-4">

        <b-list-group>
            <b-list-group-item v-for="(answer, index) in answers"
             :key="index" 
             @click.prevent="selectAnswer(index)"
             :class="[selectedIndex === index ? 'selected' : '']"
             >
              {{answer}}"
            </b-list-group-item>
        </b-list-group>
    <div style="margin-top:20px" >
        <b-button variant="primary" href="#">Submit</b-button>
        <b-button @click="next" variant="success ml-10" href="#" style="margin-left:50px" >Next</b-button>
    </div>

  </b-jumbotron>
</div></template>

<script>
    import _ from 'lodash'
    export default {
        props:{
            currentQuestion: Object,
            next:Function
        },
        data(){
            return{
                selectedIndex: null,
                shuffledAnswers:[]
            }
        },
        computed:{
            answers(){
                let answers = [...this.currentQuestion.incorrect_answers]
                answers.push(this.currentQuestion.correct_answer)
                return answers
            }
        },
        watch:{
            currentQuestion:{
                immediate:true,
                handler(){
                    this.selectedIndex=null,
                    this.shuffleAnswer()
                }
            }
        },
        methods:{
            selectAnswer(index){
                this.selectedIndex = index
            },
            shuffleAnswer(){
                let answers = [...this.currentQuestion.incorrect_answers,this.currentQuestion.correct_answer]
                this.shuffledAnswers = _.shuffle(answers)
            },
        }
    }
</script>

<style scoped> 
    .list-group-item:hover{
        background: #eeeeee;
        cursor: pointer;
    }
    .selected{
        background-color:lightblue;
    }
    .correct{
        background-color:lightgreen;
    }.incorrect{
        background-color:red;
    }
</style>