<template>
  <div class="content" ref="content"> 
    <div class="nowplay-wrapper">
      <ul class="nowplay-list">
        <li class="nowplay-item" v-for="item in movieList" :key="item.id" @click="toDetail(item.id)"> 
          <img width="64" height="90" src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1568683619&di=e45a430c366354f7be2df18dba008768&imgtype=jpg&er=1&src=http%3A%2F%2Fpic32.nipic.com%2F20130816%2F13287978_102304113000_2.jpg"/>
          <div class="desc">
            <h1 class="title">{{ item.nm }}</h1>
            <div class="comments">
              <span class="text">影评:</span>
              <span  class="score">{{ item.sc }}</span>
            </div>
            <div class="star">
              <span class="text">主演:{{ item.star }}</span>
            </div>
            <p class="text">{{ item.showInfo }}</p>
            <img v-show="item.version.substring(0,3) === 'v3d' " class="max" width="50" height="17" src="data:image/png;base64,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"/>
          </div>
          <div class="buy">
            <button class="btn">购票</button>
          </div>
        </li>
      </ul>
    </div>
  </div> 
</template>
<script>
import BScroll from 'better-scroll'
export default {
  name : 'nowplay',
  data () {
    return {
      movieList:[]
    };
  },
  created(){
    const movie = require('../../data/nowplay.json')
    let movieList = movie.data.movieList
    this.movieList = movieList
    this.$nextTick(()=>{
      this.scroll = new BScroll(this.$refs.content,{
        click:true
      })
    })
  },
  methods:{
    toDetail(id){
      this.$router.push(`/movie/detail/${id}`)
    }
  }

}
</script>
<style  scoped>
.content{
  position: absolute;
  top: 94px;
  left: 0;
  bottom: 52px;
  width: 100%;
  overflow: hidden;
}
.nowplay-list{
  padding: 15px 20px 0 15px;
}
.nowplay-item{
  display: flex;
  border-bottom: 1px solid #e6e6e6 ;
  padding: 10px 0;
}
.desc{
  flex: 1;
  padding-left: 5px;
  position: relative;
}
.title{
  font-size: 17px;
  font-weight: 700;
  margin-bottom: 10px;
}
.text{
  font-size: 13px;
  color: #666666;
}
.score{
  font-size: 15px ;
  color: #faaf00;
}
.comments{
  margin: 5px 0;
}
.star{
  margin-bottom: 10px;
  max-width: 210px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.buy{
  height: 96px;
  display: flex;
  align-items: center;
}
.max{
  position: absolute;
  top: 0;
  right: 0;
}
.btn{
  width: 47px;
  height: 27px;
  border: 0;
  background-color: #ef4238;
  border-radius: 4px;
  cursor: pointer;
  color: white;
}
</style>