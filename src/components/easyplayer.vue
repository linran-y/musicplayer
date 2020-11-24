<template>
  <!-- 主体区域 -->
  <section id="player">
    <!-- 输入框 -->
    <header class="header">
      <h1>
        快速原型播放器
      </h1>
      <input
        autofocus="autofocus"
        autocomplete="off"
        placeholder="请输入歌名"
        class="new-todo"
        v-model="inputstring"
        @keyup.enter="search"
      />
    </header>
    <!-- 列表区域 -->
    <section class="main">
      <ul class="music-list">
        <li class="music" v-for="(it,idx) in this.songs" :key="idx">
          <div class="view" >
            <span class="index">{{idx+1}}.</span>
            <label>{{it.name}}</label>
            <button class="play" @click="songgetsrc(it.id)">
            </button>
          </div>
        </li>
      </ul>
    </section>
    <!-- 统计和清空 -->
    <footer class="footer">
      <audio :src="songurl" autoplay controls></audio>
    </footer>
  </section>
</template>

<script>
  /*
    接口1:歌曲搜索
      地址:https://autumnfish.cn/search
      方法:get
      参数:keywords  搜索关键字

    接口2:获取歌曲播放地址
      地址:https://autumnfish.cn/song/url
      方法:get
      参数:id  歌曲id
  */
  import axios from 'axios'
  import '../assets/css/player.css'
  export default {
    data(){
      return {
        inputstring:"年少有为",
        songs:[],
        songurl:null,
      }
    },
    methods:
            {
              songgetsrc(id){
                axios(
                        {

                          method:"get",
                          url:"https://autumnfish.cn/song/url",
                          params:
                                  {
                                    id:id,
                                  }
                        }
                ).then(res=>
                {
                  //console.log(res);
                  this.songurl=res.data.data[0].url;

                })
  },
              search(){
                axios(
                        {
                          url:"https://autumnfish.cn/search",
                          method:"get",
                          params:
                                  {
                                    keywords:this.inputstring,
                                  }
                        }
                ).then(res=>{
                  //console.log(res);
                  this.songs=res.data.result.songs;
                })
              }
            }
  }
</script>

<style></style>
