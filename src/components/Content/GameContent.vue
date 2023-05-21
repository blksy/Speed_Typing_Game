<template>
    <div class="btns__contain">
       <button class="button__dif" @click="easyDiff">Easy</button>
       <button class="button__dif" @click="mediumDiff">Medium</button>
       <button class="button__dif" @click="hardDiff">Hard</button>
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
      <button class="button" @click="reset">New Game</button>
    </div>
</template>

<script>
   export default{
    data(){
        return{
            time: 8,
            score: 0,
            seconds:0,
            easy: 9,
            medium: 6,
            hard: 3,
            isGameOn: true,
            inputValue: '',
            message: '',
            word: '',
            words:[ 'calendar','appointment','crossover','comparison','tomorrow','comfortable','generate','stubborn','cocktail','accidentally','nonsense','jealous',
             'impatient','maelstrom','appropriate','mountaintop','grateful','algorithm',"maintain","other","phenomenon","excellent","aberration","complement","different","exaggerate",
             "recommend","development","direction","immediate","important","subjugate","public","accomplish","knowledge","conflagration","disability","arrangement","impostor","credibility"],
        }
    },
    methods:{
        getUserInput(){
          const userWord = this.$refs.form.userInput.value;
          if(userWord === this.word){
            this.message = 'Correct!'
            this.word = this.randomWord()
            this.inputValue = '';
            this.score ++;
            this.timeReset();
          }else{
            this.message = 'Wrong Answer!'
          }
        },

        randomWord(){
            let randomWord = Math.floor(Math.random() * this.words.length)
            return this.words[randomWord];
        },
        
        easyDiff(){
          this.seconds = this.easy;
          this.timeLeft();
          this.timeCountDown();
          this.level = 'easy';
        },

        mediumDiff(){
          this.seconds = this.medium;
          this.timeLeft();
          this.timeCountDown();
          this.level = 'medium';
        },

        hardDiff(){
          this.seconds = this.hard;
          this.timeLeft();
          this.timeCountDown();
          this.level = 'hard';
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
            this.time = this.easy
         }else if(this.level === 'medium'){
            this.time = this.medium
         }else if(this.level === 'hard'){
            this.time = this.hard
         }
        },

        reset(){
        window.location.reload();
        },
    },

    mounted(){
        this.word = this.randomWord();
    }
   }
</script>

<style lang="scss" scoped>
  @import './__GameContent.scss';
</style>