<template>
  <section class="columns" v-if="!status">
    <div class="column">
      <div class="box has-text-centered mt-3">
        <button class="button is-success" @click="startGame">START</button>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  name: "Start",
  props: {
    status: Boolean
  },
  data() {
    return {
      data: {
        gameIsRunning: true,
        playerHealth: 100,
        monsterHealth: 100,
        turns: []
      }
    };
  },
  methods: {
    startGame() {
      if(!this.data.gameIsRunning){
        this.data.gameIsRunning = true;
      }
      console.log(this.data.gameIsRunning);
      this.$emit("startGame", this.data);
    },
  }
};
</script>