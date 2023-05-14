<template>
    <div class="content">
        <h3>Type the given word within <span class="seconds">{{seconds}}</span> seconds</h3>
        <h1 class="guess">{{ word }}</h1>
            <form ref="form" >
                <input type="text" placeholder="Start typing"/>
            </form>
        <h4 class="message">{{message}}</h4>
      <div class="score">
        <h4>Time Left: {{ time }}</h4>
        <h4>Score: {{score}}</h4>
      </div>
      <button class="button">New Game</button>
    </div>
</template>

<script>
   export default{
    data(){
        return{
            time: 0,
            score: 0,
            seconds:0,
            message: '',
            word: '',
            words:['hello','appointment','crossover','hat','river','statue','generate','stubborn','cocktail','sugar','nonsense','jealous',
             'impatient','joke','appropriate','mountaintop','javascript','algorithm',"own","other","old","right","big","high","different","small",
             "large","next","early","young","important","few","public","bad","same","able","disability","arrangement","impostor","credibility"],
        }
    },
    methods:{
        randomWord(){
            let randomWord = Math.floor(Math.random() * this.words.length)
            return this.words[randomWord];
        }
    },
    mounted(){
        this.word = this.randomWord();
    }
   }
</script>

<style lang="scss" scoped>
  @import './__GameContent.scss';
</style>