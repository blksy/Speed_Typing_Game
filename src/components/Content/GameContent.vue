<template>
    <div class="content">
        <h3>Type the given word within <span class="seconds">SECONDS</span> seconds</h3>
        <h1 class="guess">WORD </h1>
            <form ref="form" >
                <input type="text" placeholder="Start typing"/>
            </form>
        <h4 class="message">{{message}}</h4>
      <div class="score">
        <h4>Time Left: TIME</h4>
        <h4>Score: SCORE</h4>
      </div>
      <button class="button">New Game</button>
    </div>
</template>

<script>
   export default{
   }
</script>

<style lang="scss" scoped>
  @import './__GameContent.scss';
</style>