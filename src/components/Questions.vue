<template>
<div>
    <div v-if="timeUp">
        <div><h4>Question {{num + 1 }} / <span style="font-weight: lighter; font-size: 16px">{{questions.length}}</span></h4></div>
        <p class="cursor1" >{{ questions[num].question}}</p>

        <button class="cursor" name="one"  @click="answerPicked" :disabled="isDisabled" :class="correct1">{{ questions[num].option1}}</button><br>

        <button class="cursor" name="two" @click="answerPicked" :disabled="isDisabled" :class="correct2">{{ questions[num].option2}}</button><br>

        <button class="cursor" name="three" @click="answerPicked" :disabled="isDisabled" :class='correct3'>{{ questions[num].option3}}</button><br>

        <button class="cursor" name="four" @click="answerPicked" :disabled="isDisabled" :class="correct4">{{ questions[num].option4}}</button> <br>

        <button class="btn btn-success ml-2 mt-3" @click="nextQuestion">Next</button>

        <h6 class="text-right">score: {{scores}}</h6>

    </div>
    <div v-if="!timeUp">
        <h1>You scored {{scores}}/{{questions.length}}</h1>
        <h6>{{closingMessage()}}</h6>
        <a href="#" @click="playAgain">Play Again</a>
    </div>
</div>
  

</template>

<script>
import { questionsA } from './questions'
export default {
    data () {
        return {
            show: true,
            num: 0,
            questions: questionsA,
            scores: 0,
            isDisabled: false,
            attachRed: false,
            correct1: {},
            correct2: {},
            correct3: {},
            correct4: {},

        }
    }, 
    props: ["secondSend"],
    methods: {
        answerPicked (event) {
            this.isDisabled = !this.isDisabled
            if(event.target.innerText.toUpperCase().trim() === this.questions[this.num].answer.toUpperCase().trim() && event.target.name === "one"){
            this.correct1 = {green: true}
            this.scores++
            }
            else if(event.target.innerText.toUpperCase().trim() !== this.questions[this.num].answer.toUpperCase().trim() && event.target.name === "one"){
            this.correct1 = {red: true}
            }

            if(event.target.innerText.toUpperCase().trim() === this.questions[this.num].answer.toUpperCase().trim() && event.target.name === "two"){
            this.correct2 = {green: true}
            this.scores++
            }
            else if(event.target.innerText.toUpperCase().trim() !== this.questions[this.num].answer.toUpperCase().trim() && event.target.name === "two"){
            this.correct2 = {red: true}
            }


            if(event.target.innerText.toUpperCase().trim() === this.questions[this.num].answer.toUpperCase().trim() && event.target.name === "three"){
            this.correct3 = {green: true}
            this.scores++
            }
            else if(event.target.innerText.toUpperCase().trim() !== this.questions[this.num].answer.toUpperCase().trim() && event.target.name === "three"){
            this.correct3 = {red: true}
            }


            if(event.target.innerText.toUpperCase().trim() === this.questions[this.num].answer.toUpperCase().trim() && event.target.name === "four"){
            this.correct4 = {green: true}
            this.scores++
            }
            else if(event.target.innerText.toUpperCase().trim() !== this.questions[this.num].answer.toUpperCase().trim() && event.target.name === "four"){
            this.correct4 = {red: true}
            }
        },
        nextQuestion () {
            this.isDisabled = true
            this.correct1 = {green: false}
            this.correct2 = {green: false}
            this.correct3 = {green: false}
            this.correct4 = {green: false}
            if(this.num <= this.questions.length)
            this.num++;
            this.isDisabled = !this.isDisabled
            if (this.num >= this.questions.length)
            this.show = !this.show
        },
        playAgain () {
            location.reload()
        },
        closingMessage () {
            if (this.scores < 5)
            return "Try harder"
            if (this.scores < 7)
            return "Above average"
            if (this.scores > 7)
            return "Excellent!"
        }
    },
    computed: {
        timeUp: function () {
            var qSend =  this.secondSend;
            if(qSend >= 100){
                this.$emit('timeDonReach', qSend)
                return false
            }
            else return true
        }
    }
   
}
</script>

<style scoped>
.cursor{
    background: rgb(1, 5, 27);
    padding: 10px 20px;
    border-radius: 20px;
    cursor: pointer;
    color: white;
    min-width: 200px;
    text-align: left;
    margin: 5px;
    font-weight:lighter;
    outline: none;
    border: 1px solid rgb(48, 6, 199);
}

.cursor1 {
    color: white;
    background:  rgba(0, 0, 0, 0.2);
    padding: 10px 120px;
}

.green {
    background-color: rgb(123, 226, 123);
    padding: 10px;
    border-radius: 20px;
    cursor: pointer;
    color: rgb(39, 39, 39);
    min-width: 200px;
    text-align: left;
    margin: 5px;
    font-weight: lighter;
    outline: none;
}
.red {
    background-color: rgb(243, 81, 81);
    padding: 10px;
    border-radius: 20px;
    cursor: pointer;
    color: white;
    min-width: 200px;
    text-align: left;
    margin: 5px;
    font-weight: lighter;
    outline: none;
}
.btn {
    background-color: #41B883;
    color: rgb(1, 5, 27);
    outline: none;
}
a {
    text-decoration: none;
}
</style>


