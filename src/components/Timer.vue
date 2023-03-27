<template>
  <div class="timer" :class="[state]">
    <div class="timer-text-wrapper">
      <div class="timer-text-h">{{timeH}}</div>
      <div class="timer-text-m">{{timeM}}</div>
      <div class="timer-text-s">{{timeS}}</div>
    </div>
    <div class="timer-buttons">
      <div class="timer-button-start" @click="toggle"></div>
      <div class="timer-button-pause" @click="toggle"></div>
      <div class="timer-button-stop" @click="clearTimer"></div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'TimerComponent',
    data() {
      return {
        state    : 'off',
        lastDate : null,
        timerId  : null,
        timer    : 0,
        timeH    : '',
        timeM    : '',
        timeS    : '00',
      }
    },

    methods: {

      clearTimer() {
        clearInterval(this.timerId);
        this.state = "off";
        this.timer = 0;
        this.lastDate = new Date();
        this.updateTimer();
      },

      updateTimer() {
        const diff = new Date() - this.lastDate;
        this.timer += diff;
        this.lastDate = new Date();

        const hours = this.timer > 0 ? Math.floor(this.timer / 1000 / 60 / 60) % 24 : 0;
        const minutes = this.timer > 0 ? Math.floor(this.timer / 1000 / 60) % 60 : 0;
        const seconds = this.timer > 0 ? Math.floor(this.timer / 1000 ) % 60 : 0;
        
        this.timeH = hours < 10 ? '0' + hours : hours;
        this.timeH = (this.timeH == "00") ? '' : this.timeH;

        this.timeM = minutes < 10 ? '0' + minutes : minutes;
        this.timeM = (this.timeH == '' && this.timeM == "00") ? '' : this.timeM;

        this.timeS = seconds < 10 ? '0' + seconds : seconds;

      },

      toggle() {
        this.state = (this.state == "on") ? "off" : "on"
        
        if (this.state == "on") {
          this.lastDate = new Date();
          this.updateTimer();

          this.timerId = setInterval(() => {
            this.updateTimer();
          }, 200);
        }
        else {
          clearInterval(this.timerId);
        }
      },
    },

    mounted() {
      //console.debug(this);
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  @font-face {
      font-family: 'Gotham Pro';
      src: url('/fonts/Gotham Pro/gothampro.ttf');
  }
  .timer {
    width: 225px;
    height: 120px;
    left: 212px;
    top: 72px;
    background: #696969;
    /* margin-bottom: 45px; */
  }

  .timer.on {
    color: #FFFFFF;
  }

  .timer.off {
    color: #9E9E9E;
  }
  
  .timer-text-wrapper,
  .timer-buttons {
    display: flex;
    height: 59.5px;
    justify-content: center;
    align-items: center;
  }
  
  .timer.on .timer-buttons {
    border-top: 1px solid #FFFFFF;
  }
  .timer.off .timer-buttons {
    border-top: 1px solid #9E9E9E;
  }


  .timer-buttons {
    border-bottom: none;
  }

  .timer-text-wrapper {
    font-family: 'Gotham Pro';
    font-style: normal;
    font-weight: 400;
    font-size: 22px;
    line-height: 21px;
    text-align: center;
  }

  .timer-text-h:not(:empty)::after,
  .timer-text-m:not(:empty)::after {
    content: ":";
  }

  .timer.on .timer-button-start {
    display: none;
  }

  .timer.off .timer-button-start {
    border-left: 17px solid #9E9E9E;
    width: 0;
    height: 0;
    margin-left: 70px;
    border-top: 10px solid transparent;
    border-bottom: 10px solid transparent;
  }

  .timer-button-stop {
    width: 20px;
    height: 20px;
    margin-left: auto;
    margin-right: 70px;
  }

  .timer.on .timer-button-stop {
    background-color: #FFFFFF;
  }

  .timer.off .timer-button-stop {
    background-color: #9E9E9E;
  }

  .timer.on .timer-button-pause {
    margin-left: 73px;
    width: 4px;
    height: 20px;
    border-left: 3px solid #FFFFFF;
    border-right: 3px solid #FFFFFF;
  }

  .timer.off .timer-button-pause {
    display: none;
  }
  
  .timer-button-start:hover,
  .timer-button-stop:hover,
  .timer-button-pause:hover {
    cursor: pointer;
  }

</style>
