<template>
  <div id="app">
    <img width="25%" src="https://htmlcolorcodes.com/assets/images/html-color-codes-color-palette-generators-7a5b8241.jpg">
    <div style="margin-top:32px">
      <label name="" for="colorInput"> color </label>
      <input placeholder="type color" id="colorInput" type="text" v-model="color" @keyup.enter="transformColor" >
      
    </div>
    <div>
      <label style="font-size:13px"> 类别 </label>
       <select v-model="selected" @change="transformColor">
        <option value="" disabled>select a color harmony</option>
        <option>Complementary</option>
        <option>Triadic</option>
        <option>Tetradic</option>
        <option>Analogous</option>
        <option>Shades</option>
        <option>Tints</option>
        <option>Tones</option>
      </select>
    </div>
    <p>{{error}}</p>
    <div id="harmonies">
      <Box v-for="item in colors" :key="item.id" :color="item.color"/>
    </div>
    <HelloWorld msg="Simple Color Harmony Map"/>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld";
import Box from "./components/Box";
import tinycolor from "tinycolor2";
export default {
  name: "App",
  components: {
    HelloWorld,
    Box
  },
  data() {
    return {
      color: "red",
      colors: [],
      error: null,
      selected: ""
    };
  },
  methods: {
    getColors({ r, g, b, a }, num, n) {
      let index,
        c,
        s,
        u,
        res = [];
      for (
        (isFinite(num) && "number" == typeof num) || (num = 10),
          c = (n - r) / num,
          s = (n - g) / num,
          u = (n - b) / num,
          index = 0;
        num > index;
        index++
      ) {
        console.log(r, g, b, a);
        res.push({
          id: index,
          color: tinycolor({ r, g, b, a }).toString("hsl")
        });
        r += c;
        g += s;
        b += u;
      }
      return res;
    },
    transformColor() {
      const color = tinycolor(this.color);
      if (color.isValid()) {
        switch (this.selected.toLowerCase()) {
          case "tints":
            this.colors = this.getColors(color.toRgb(), 8, 255);
            break;
          case "shades":
            this.colors = this.getColors(color.toRgb(), 8, 0);
            break;
          case "tones":
            this.colors = this.getColors(color.toRgb(), 8, 128);
            break;
          case "triadic":
            this.colors = color
              .triad()
              .map((c, index) => ({ id: index, color: c.toString("hsl") }));
            break;
          case "tetradic":
            this.colors = color
              .tetrad()
              .map((c, index) => ({ id: index, color: c.toString("hsl") }));
            break;
          case "complementary":
            this.colors = [
              { id: 0, color: color.toString("hsl") },
              { id: 1, color: color.complement().toString("hsl") }
            ];
            break;
          default:
            this.colors = color
              .analogous()
              .map((c, index) => ({ id: index, color: c.toString("hsl") }));
            break;
        }
      } else {
        this.error = "your color is inValid";
      }
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  text-align: center;
}
div#harmonies {
  margin-right: -0.75em;
  margin-left: -0.75em;
  text-align: left;
  overflow: hidden;
}
</style>
