<template>
  <div class="container">
    <div class="swipe-box" >
      <mt-swipe :auto="3000">
        <mt-swipe-item v-for="item in imgList" :key="item.id">
          <a :href="item.linkUrl">
          <img class="swipe-img" :src="item.picUrl" alt="">
          </a>
        </mt-swipe-item>
      </mt-swipe>
    </div>
    <div class="wrapper" ref="wrapper" style="overflow: hidden;margin-top: 0.2rem">
      <div class="content song-box">
        <h2>热门歌单</h2>
        <div class="song-list">
          <div class="song-item" v-for="item in songList">
            <div class="icon">
              <img :src="item.picUrl" alt="" style="height: 0.8rem;width: 0.8rem " >
            </div>
            <div class="text">
              <p>{{item.songListDesc}}</p>
              <p>
              <span>
                收藏人数：<i>{{item.accessnum}}</i>
              </span>

              </p>
              <p>
               <span>
                专辑创建：{{item.songListAuthor}}
              </span>
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div>
      111
    </div>
  </div>
</template>

<script>
  import Bscroll from 'better-scroll'
  const api ='https://c.y.qq.com/musichall/fcgi-bin/fcg_yqqhomepagerecommend.fcg?g_tk=5381&uin=0&format=json&inCharset=utf-8&outCharset=utf-8&notice=0&platform=h5&needNewCode=1&_=1528894745999'
  export default {
    name: "recommend",
    data(){
      return{
        imgList:[],
        songList:[],
        scroll:null
      }
    },
    created(){
      this.$axios(api).then((res)=>{
        let img_Swpier=res.data.data.slider
        this.imgList=img_Swpier
        this.songList=res.data.data.songList
        console.log(this.songList)


      })
        .catch((err)=>{
          console.log(err)
        })
    },
    mounted(){
      console.log(11)
      console.log(this.$refs.wrapper)
      this.$nextTick(()=>{
        this.scroll = new Bscroll(this.$refs.wrapper)
      })

    },
    methods:{

    }
  }
</script>

<style scoped lang="less">
.container{
  .swipe-box{
    width: 100%;
    height: 1.5rem;
    .mint-swipe{

    }
    .swipe-img{
      width: 100%;
    }
  }
  .song-box{
    h2{
      text-align: center;
      font-weight: bold;
      margin: 0.1rem 0;
      font-size: 0.18rem;
    }
    .song-list{

      .song-item{
        display: flex;
        flex-direction: row;
        margin: 0.05rem 0;
        .icon{
          padding: 0 0.1rem;
        }
        .text{
          margin-left: 0.15rem;
          display: flex;
          flex-direction: column;
          justify-content:space-between ;
          p{
            font-size: 0.16rem;
            margin: 0.05rem 0;
            span{
              font-size: 0.12rem;
              margin-right: 0.1rem;
              i{
                color: #ff0033;
              }
            }
          }
        }
      }
    }
  }
}
</style>
