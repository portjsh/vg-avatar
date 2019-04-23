<template>
  <div id="app">
    <avatar-wizard></avatar-wizard>
  </div>
</template>

<script>
import AvatarWizard from "./components/Avatar.vue";

export default {
  name: "app",
  components: {
    AvatarWizard
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
