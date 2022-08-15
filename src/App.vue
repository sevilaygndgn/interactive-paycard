<template>
  <div id="app">
    <router-view />
  </div>
</template>
<script>
import HomeView from "./views/HomeView.vue";
export default {
  components: { HomeView },
};
</script>
<style lang="scss">
@import "./assets/reset.scss";
@import url('https://fonts.googleapis.com/css2?family=Farsan&family=Roboto&display=swap');
body {
  height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
