<template>
  <q-page class="column justify-center items-center">
    <img class="logo" alt="Telos logo" src="~assets/telos-logo-full.png" />
    <!--<h6 class="description">
      Use this template as a starting point for your app and save the time of writing all the boilerplate code.
      It has an implementation of UAL (Universal
      Authenticator Library) which you can test with the Login button.  There are other examples and essential quasar links in the side menu.
    </h6>-->
    <div align="center">
      <InteractiveCanvas/>
        <!--<canvas id="myCanvas" width="500" height="200" style="border:2px solid black"></canvas>
        <br /><br />
        <button onclick="javascript:clearArea();return false;">Clear Area</button>
        Line width : <select id="selWidth">
            <option value="1">1</option>
            <option value="3">3</option>
            <option value="5">5</option>
            <option value="7">7</option>
            <option value="9" selected="selected">9</option>
            <option value="11">11</option>
        </select>
        Color : <select id="selColor">
            <option value="black">black</option>
            <option value="blue" selected="selected">blue</option>
            <option value="red">red</option>
            <option value="green">green</option>
            <option value="yellow">yellow</option>
            <option value="gray">gray</option>
        </select>-->
    </div>
  </q-page>
</template>

<script>
import InteractiveCanvas from "../components/InteractiveCanvas"
export default {
  name: "Index",
  components: {
    InteractiveCanvas
  }
};

</script>

<style lang="sass" scoped>
.logo
  max-width: 400px

.description
  max-width: 800px
</style>
