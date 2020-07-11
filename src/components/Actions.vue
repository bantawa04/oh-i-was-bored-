<template>
  <section class="columns" v-if="status.gameIsRunning">
    <div class="column">
      <div class="box has-text-centered mt-3">
        <button class="button is-danger" @click="attack">ATTACK</button>
        <button class="button is-warning" @click="specialAttack">SPECIAL ATTACK</button>
        <button class="button is-success" @click="heal">HEAL</button>
        <button class="button is-info" @click="giveUp">GIVE UP</button>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  name: "Actions",
  props: {
    status: Object
  },
  data() {
    return {
      datas: {}
    };
  },
  methods: {
    startGame() {
      this.datas.gameIsRunning = true;
      this.datas.playerHealth = 100;
      this.datas.monsterHealth = 100;
      this.datas.turns = [];
      this.$emit('startAgain', this.datas);
    },
    attack() {
      let damage = this.calculateDamage(3, 10);
      this.datas.monsterHealth -= damage;
      this.datas.turns.unshift({
        isPlayer: true,
        text: "PLAYERS HITS MONSTER FOR " + damage
      });
      if (this.checkWin()) {
        return;
      }
      this.monsterAttack();
      console.log(this.datas);
      this.$emit("attacked", this.datas);
    },
    specialAttack() {
      let damage = this.calculateDamage(10, 20);
      this.datas.monsterHealth -= damage;
      this.datas.turns.unshift({
        isPlayer: true,
        text: "PLAYERS HITS HARD MONSTER FOR " + damage
      });
      if (this.checkWin()) {
        return;
      }
      this.monsterAttack();
      this.$emit("specialAttack", this.datas);
    },
    heal() {
      if (this.datas.playerHealth <= 90) {
        this.datas.playerHealth += 10;
        this.datas.turns.unshift({
          isPlayer: true,
          text: "PLAYERS HEALS FOR 10 "
        });
      } else {
        this.datas.playerHealth = 100;
      }
      this.monsterAttack();
      this.$emit("heal", this.datas);
    },
    giveUp() {
        this.datas.gameIsRunning = false;
        this.datas.playerHealth = 100;
        this.datas.monsterHealth = 100;
        this.datas.turns = [];
        this.$emit("giveUp", this.datas);
    },
    calculateDamage(min, max) {
      return Math.max(Math.floor(Math.random() * max) + 1, min);
    },
    checkWin() {
      if (this.datas.monsterHealth <= 0) {
        if (confirm("You won ! New Game ?")) {
          this.startGame();
        } else {
          this.datas.gameIsRunning = false;
        }
        return true;
      } else if (this.datas.playerHealth <= 0) {
        if (confirm("You Lost ! New Game ?")) {
          this.startGame();
        } else {
          this.datas.gameIsRunning = false;
        }
        return true;
      }

      return false;
    },
    monsterAttack() {
      let damage = this.calculateDamage(5, 12);
      this.datas.playerHealth -= damage;
      this.datas.turns.unshift({
        isPlayer: false,
        text: "MONSTER HITS PLAYER FOR " + damage
      });
      this.checkWin();
    }
  },
  mounted() {
    this.datas = this.status;
  }
};
</script>
<style scoped>
.button:not(:last-child) {
  margin-right: 1rem;
}
</style>