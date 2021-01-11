<template>
  <div id="app">
    <div style="margin-bottom: 5%">
      <h2 style="margin-bottom: none !important">Vue JS avatar uploader</h2>
      <p>Really simple image uploader with zero dependencies.</p>
    </div>
    <Uploader></Uploader>
  </div>
</template>

<script>
import Uploader from "./components/Uploader";

export default {
  name: "App",
  components: {
    Uploader,
  },
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
  display: flex;
  flex-direction: column;
}
</style>
