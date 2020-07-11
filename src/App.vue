<template>
  <div class="container mt-6">
    <Players v-bind:pHealth="status.playerHealth" v-bind:mHealth="status.monsterHealth" />
    <Start v-bind:status="status.gameIsRunning" v-on:startGame="start" />
    <Actions 
    v-if="status.gameIsRunning" 
    :status="status" 
    v-on:attacked="updateStatus" 
    v-on:specialAttack="updateStatus"
    v-on:startAgain="updateStatus"
    v-on:heal="updateStatus"
    v-on:giveUp="updateStatus"/>
    <Messages :turns="status.turns" v-if="status.turns.length"/>
  </div>
</template>

<script>
import Players from "./components/Players";
import Start from "./components/Start";
import Actions from "./components/Actions";
import Messages from "./components/Messages";
export default {
  name: "App",
  components: {
    Players,
    Start,
    Actions,
    Messages
  },
  data() {
    return {
      status: {
        playerHealth: 100,
        monsterHealth: 100,
        gameIsRunning: false,
        turns: []
      }
    };
  },
  methods: {
    start(data) {      
      this.status = data;
      // console.log(data.gameIsRunning);
    },
    updateStatus(datas) {
      this.status = datas;
    }
  }
};
</script>
