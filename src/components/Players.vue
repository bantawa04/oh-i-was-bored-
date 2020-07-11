<template>
  <div class="columns">
    <div class="column p-4">
      <h1 class="is-size-2 has-text-centered">You</h1>
      <figure class="image is-128x128 container">
        <img src="../assets/img/witcher.jpeg" />
      </figure>
      <div
        class="column has-background-success has-text-white healthBar"
        :style="{width: pHealth +'%'}"
      >{{pHealth}}</div>
    </div>
    <div class="column p-4">
      <h1 class="is-size-2 has-text-centered">Monster</h1>
      <figure class="image is-128x128 container">
        <img src="../assets/img/monster.jpg" />
      </figure>
      <div
        class="column has-background-success has-text-white healthBar"
        :style="{width: mHealth +'%'}"
      >{{mHealth}}</div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Players",
  props: {
    pHealth: Number,
    mHealth: Number
  }
};
</script>
<style scoped>
.healthBar{
    transition: all 500ms ease-out;
}
</style>