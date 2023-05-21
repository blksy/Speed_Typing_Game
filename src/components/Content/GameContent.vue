<template>
    <div class="btns__contain">
       <button class="button__dif">Easy</button>
       <button class="button__dif">Medium</button>
       <button class="button__dif">Hard</button>
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
          }else{
            this.message = 'Wrong Answer!'
          }
        },

        randomWord(){
            let randomWord = Math.floor(Math.random() * this.words.length)
            return this.words[randomWord];
        },
        timeCountDown(){
            setInterval(() =>{
            let remainingTime = this.time
            if(remainingTime > 0){
                this.time--
            }else{
                this.isGameOn = false
                this.message = 'Gameover'
                this.inputValue = ''
            }}, 1200);
        }, 
        timeLeft(){
            this.time = this.seconds;
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