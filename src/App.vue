<template>
  <div class="header">
    <ul class="header-button-left">
      <li>Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li @click="nextMenu">Next</li>
    </ul>
    <img src="./assets/logo.png" class="logo"/>
  </div>

  <MainContainer :data="data" :step="step" :image="image"/>
  <button @click="plusButton">더보기 리그</button>

  <div class="footer">
    <ul class="footer-button-plus">
      <input @change="upload" type="file" id="file" class="inputfile"/>
      <label for="file" class="input-plus">+</label>
    </ul>
  </div>

</template>

<script>

import MainContainer from "@/components/Container.vue";
import data from "@/assets/data";
import axios from "axios";

export default {
  name: 'App',
  components: {MainContainer},
  data() {
    return {
      data,
      clickTimes: 0,
      step: 0,
      image : '',
    }
  },
  methods: {
    plusButton() {
      axios.get(`https://codingapple1.github.io/vue/more${this.clickTimes}.json`).then((result) => {
        this.data.push(result.data);
        this.clickTimes++;
      }).catch((error) => {
        alert(error);
      })
    },
    nextMenu() {
      if (this.step == 2) {
        this.step = 0;
      } else {
        this.step++;
      }
    },
    upload(e){
      let file = e.target.files;
      this.image = URL.createObjectURL(file[0]);

      this.step=1;

    },
  }
}
</script>

<style>

body {
  margin: 0;
}

ul {
  padding: 5px;
  list-style-type: none;
}

.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}

.header {
  width: 100%;
  height: 40px;
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}

.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}

.header-button-right {
  color: skyblue;
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}

.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: white;
}

.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}

.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}

.inputfile {
  display: none;
}

.input-plus {
  cursor: pointer;
}

#app {
  box-sizing: border-box;
  font-family: "consolas";
  margin-top: 60px;
  width: 100%;
  max-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}


</style>
