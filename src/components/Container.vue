<template>
  <div>
    <div v-if="step==0">
    <Post v-for="(a,i) in data" :key="i" :data="data[i]">
      {{a.content}}
    </Post>
    </div>
  </div>
  <!-- 필터선택페이지 -->
  <div class="upload-image" :style="{backgroundImage : `url(${image})`}"></div>
  <div class="filters" v-if="step==1" >
    <div class="filter-1"></div>
    <div class="filter-1"></div>
    <div class="filter-1"></div>
    <div class="filter-1"></div>
    <div class="filter-1"></div>
  </div>

  <!-- 글작성페이지 -->
  <div class="upload-image" v-if="step==2" :style="{backgroundImage : `url(${image})`}"></div>
  <div class="write">
    <textarea class="write-box">write!</textarea>
  </div>
</template>

<script>

import Post from "@/components/Post.vue";

export default {
  name: 'MainContainer',
  components: {Post},
  props : {
    data : Array,
    step : Number,
    image : String,
  }
}
</script>

<style>
.upload-image{
  width: 100%;
  height: 450px;
  background: cornflowerblue;
  background-size : cover;
}
.filters{
  overflow-x:scroll;
  white-space: nowrap;
}
.filter-1 {
  width: 100px;
  height: 100px;
  background-color: cornflowerblue;
  margin: 10px 10px 10px auto;
  padding: 8px;
  display: inline-block;
  color : white;
  background-size: cover;
}
.filters::-webkit-scrollbar {
  height: 5px;
}
.filters::-webkit-scrollbar-track {
  background: #f1f1f1;
}
.filters::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
  background: #555;
}
.write-box {
  border: none;
  width: 90%;
  height: 100px;
  padding: 15px;
  margin: auto;
  display: block;
  outline: none;
}
</style>