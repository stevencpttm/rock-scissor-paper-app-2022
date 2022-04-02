<template>
  <div id="container">
    <div id="bot-placeholder">
      <img :src="bot_image">
    </div>
    <div id="you-placeholder">
      <img :src="you_image">
    </div>
    <div id="buttons-container">
      <div id="btn-paper" @click="clickHandler(1)"></div>
      <div id="btn-scissor" @click="clickHandler(2)"></div>
      <div id="btn-rock" @click="clickHandler(3)"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      botChoice: 0,
      youChoice: 0,
    }
  },
  computed: {
    bot_image() {
      let botChoices = {};
      botChoices['-30'] = 'rock-lose.png';
      botChoices['-20'] = 'scissor-lose.png';
      botChoices['-10'] = 'paper-lose.png';
      botChoices['0'] = 'Placeholder-Bot.png';
      botChoices['10'] = 'paper-win.png';
      botChoices['20'] = 'scissor-win.png';
      botChoices['30'] = 'rock-win.png';
      botChoices['101'] = 'paper-draw.png';
      botChoices['102'] = 'scissor-draw.png';
      botChoices['103'] = 'rock-draw.png';
 
      return require(`@/assets/images/${botChoices[this.botChoice]}`)
    },
    you_image() {
      let userChoices = {};
      userChoices['-30'] = 'rock-lose.png';
      userChoices['-20'] = 'scissor-lose.png';
      userChoices['-10'] = 'paper-lose.png';
      userChoices['0'] = 'Placeholder-You.png';
      userChoices['10'] = 'paper-win.png';
      userChoices['20'] = 'scissor-win.png';
      userChoices['30'] = 'rock-win.png';
      userChoices['101'] = 'paper-draw.png';
      userChoices['102'] = 'scissor-draw.png';
      userChoices['103'] = 'rock-draw.png';
 
      return require(`@/assets/images/${userChoices[this.youChoice]}`)
    }
  },
  methods: {
    clickHandler(youPicked) {
      // Random number from 1..3
      let botPicked = Math.floor(Math.random() * 3) + 1;

      if (botPicked === youPicked) {
        // Draw
        this.botChoice = botPicked + 100;
        this.youChoice = youPicked + 100;
      } else if (
        youPicked === 1 && botPicked === 3 || 
        youPicked === 2 && botPicked === 1 ||
        youPicked === 3 && botPicked === 2
      ) {
        // You Win
        this.botChoice = botPicked * -10;
        this.youChoice = youPicked * 10;
      } else if (
        botPicked === 1 && youPicked === 3 || 
        botPicked === 2 && youPicked === 1 ||
        botPicked === 3 && youPicked === 2
      ) {
        // Computer Win
        this.botChoice = botPicked * 10;
        this.youChoice = youPicked * -10;
      }
    }
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
  background-color: #44D7B6;
}
#container {
  display: flex;
  flex-direction: column;
  width: 100%;
  min-height: 100vh;
  padding-top: 40px;
  box-sizing: border-box;
}
 
#bot-placeholder, #you-placeholder {
  flex: 0px 2 1;
}
 
#bot-placeholder img, #you-placeholder img {
  display: block;
  width: 60%;
  height: auto;
  margin: auto;
}
 
#buttons-container {
  flex: 0px 1 1;
  display: flex;
  flex-direction: row;
}
 
#buttons-container div {
  flex: 0px 1 1;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center bottom;
}
 
#buttons-container div#btn-paper {
  background-image: url('~assets/images/paper-btn.png');
}
 
#buttons-container div#btn-scissor {
  background-image: url('~assets/images/scissor-btn.png');
}
 
#buttons-container div#btn-rock {
  background-image: url('~assets/images/rock-btn.png');
}
</style>