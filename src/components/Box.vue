<template>
<div class="color-card">
  <div class="color-swatch">
    <div class="js-color" :style="{backgroundColor:color}"></div>
  </div>
  <div class="color-data">
    <h4 class="selectable">{{color}}</h4>
  </div>
</div>
</template>

<script>
export default {
  props: {
    color: {
      type: String
    }
  }
};
</script>

<style>
.color-card {
  position: relative;
  width: 25%;
  margin: 0 0 1.5em;
  padding: 0 0.75em;
  overflow: hidden;
  float: left;
}
.color-card .color-swatch {
  position: relative;
  width: 100%;
  padding-bottom: 54%;
  cursor: pointer;
}

.color-card .color-swatch div {
  position: absolute;
  width: 100%;
  height: 100%;
  border-top-right-radius: 3px;
  border-top-left-radius: 3px;
}
.color-card .color-data {
  padding: 0.75em 1em 0.375em;
  border-right: 1px solid #eaeaea;
  border-left: 1px solid #eaeaea;
  border-bottom: 1px solid #eaeaea;
  border-bottom-right-radius: 3px;
  border-bottom-left-radius: 3px;
}
.color-card .color-data h4 {
  height: 22px;
  margin-bottom: 0.375em;
  margin: 0;
  font-style: normal;
  font-weight: 700;
  letter-spacing: 0.1em;
  font-size: 14px;
}
</style>
