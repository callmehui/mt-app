<template>
  <div id="app">
    <!-- 头部 -->
    <app-header :poiInfo="poiInfo"></app-header>

    <!-- 导航 -->
    <app-nav></app-nav>

    <!-- 内容 -->
    <router-view></router-view>

  </div>
</template>

<script>
import Header from "./components/header/Header"
import Nav from "./components/nav/Nav"


export default {
  name: 'App',
  components: {
    "app-header": Header,
    "app-nav": Nav,
  },
  data(){
    return {
      poiInfo: {}
    }
  },
  // 在created生命周期通过created()钩子函数获取数据
  created(){
    fetch("/api/goods")
    .then( res => {
      // 通过自带的json()方法将获取的数据转换为json格式
      return res.json()
    })
    .then(
       response => {
         console.log(response)
        // 验证是否获取到数据
        if( response.code == 0 ){
          // 将获取的数据赋值为vue实例的data对象的属性
          this.poiInfo = response.data.poi_info;
        }
       }
    )
  }
}
</script>

<style>
</style>
