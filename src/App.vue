<template>
  <div id="overall">
      <section class="container text-center">
          <div class="row" v-if="show">

              <div class="col-md-4">
                  <h6>Tap into the power of ...</h6>
              </div>
              <div class="col-md-4">
                  <div class="d-flex">
                        <img src="../logo.png" alt="">
                        <h3 class="pad-down">ue Technology!</h3>
                  </div>
              </div>
              <div class="col-md-4">
                  <button class="btn btn-success btn-block" @click="timer">
                      Start Quiz
                  </button>
                </div>
          </div>
      </section>

      <section class="container" v-if="!show">
              <div class="col-md-2"></div>
              <div class="col-md-8 text-center question-container">
                    <app-header :secondSend="second"></app-header>
                    <app-question :secondSend="second" @timeDonReach="second = $event"></app-question>
              </div>
              <div class="col-md-2"></div>
      </section>
      
  </div>
</template>

<script>
import Question from './components/Questions.vue';
import Header from "./components/Header.vue"

export default {
    data () {
        return {
            show: true,
            second: 0
        }
    },
    methods: {
        timer () {
            this.show = !this.show
            setInterval(() => {
                if(this.second < 100)
                this.second = this.second + 1
                else return
                console.log(this.second)

            }, 300);
}
    },
    components: {
        appQuestion: Question,
        appHeader: Header
    }

}
</script>

<style >
.pad-down {
    padding-top: 19%;
    color: #41B883;
    margin-left: -9%;
}
#overall {
    background-color: rgb(1, 5, 27);
    height: 100vh;
    color: #41B883;
    padding-top: 10vh;
    background-image: linear-gradient(to right, rgb(1, 5, 27), rgb(1, 5, 27), rgb(1, 5, 27),rgb(1, 5, 27), rgb(3, 11, 54));
}
.btn:hover {
    background-color: #41B883;
    color: rgb(1, 5, 27);
}

.btn {
    background-color: rgb(1, 5, 27);
    color: #41B883;
    border: 1px solid #41B883;
    outline: none;
}
.question-container{
    background: rgb(1, 5, 27);
    padding: 30px 20px;
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
.d-flex {
    padding-left: 10%;
}
</style>
