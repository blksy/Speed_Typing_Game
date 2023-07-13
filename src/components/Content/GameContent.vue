<template>
    <div class="btns__contain">
       <button class="button__dif" @click="chooseDifficulty(0, 0)">Easy</button>
       <button class="button__dif" @click="chooseDifficulty(1, 1)">Medium</button>
       <button class="button__dif" @click="chooseDifficulty(2, 2)">Hard</button>
    </div>
    <div class="content">
        <h3>Type the given word within <span class="seconds">{{seconds}}</span> seconds</h3>
        <h1 class="guess">{{ word }}</h1>
            <form ref="form" @submit.prevent="getUserInput()">
                <input type="text" placeholder="Start typing" v-model="inputValue" name="userInput"/>
            </form>
        <h4 class="message">{{message}}</h4>
        <div class="score">
          <h4>Time Left: {{ time }}</h4>
          <h4>Score: {{score}}</h4>
        </div>
      <button class="button" @click="reset" :disabled="isGameOn">New Game</button>
    </div>  
</template>

<script>
import axios from 'axios';

   export default{
    data(){
        return{
            time: 0,
            score: 0,
            seconds:0,
            isGameOn: true,
            inputValue: '',
            message: '',
            word: '',
            difficulty:{
              diff:['easy', 'medium', 'hard'],
              count:[9, 6, 3]
            },
        }
    },
    methods:{        
    getUserInput(){
          const userWord = this.$refs.form.userInput.value;
          if(userWord === this.word){
            this.message = 'Correct!'
            this.word = this.getWord()
            this.inputValue = '';
            this.score ++;
            this.timeReset();
          }else{
            this.message = 'Wrong Answer!'
          }
        },

    getWord(){
        axios.get('https://random-word-api.herokuapp.com/word')
         .then(response =>{
         this.word = response.data[0];
        })
      },
            
    chooseDifficulty(name, time){
        this.seconds = this.difficulty.count[time];
        this.timeLeft();
        this.timeCountDown();
        this.level = this.difficulty.diff[name];
        this.$refs.form.userInput.focus();
      },

    timeCountDown(){
        setInterval(() =>{
        let remainingTime = this.time
        if(remainingTime > 0){
          this.time--
        }else{
          this.isGameOn = false
          this.message = 'Game Over'
          this.inputValue = ''
        }}, 1200);
        }, 

    timeLeft(){
        this.time = this.seconds;
      },

    timeReset(){
        if(this.level === 'easy'){
          this.time = 9
        }else if(this.level === 'medium'){
          this.time = 6
        }else if(this.level === 'hard'){
          this.time = 3
        }
      },

    reset(){
        this.isGameOn = true;
        this.time = 0;
        this.score = 0;
        this.seconds = 0;
        this.message = '';
      },
    },

    mounted(){
      
      this.word = this.getWord()
    }
  }

</script>

<style lang="scss" scoped>
  @import './__GameContent.scss';
</style>