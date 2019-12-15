<template>
  <div class="container">
    <div class="header">
      <nuxt-link to="/search" class="search">
        <i class="fa fa-search"></i>输入搜索内容
      </nuxt-link>
      <nuxt-link to="/user" class="user">
        <i class="fa fa-user-o"></i>
      </nuxt-link>
    </div>
    <!-- banner图 -->
    <div class="banner">
      <div class="swiper-container">
        <div class="swiper-wrapper">
          <div class="swiper-slide" v-for="ele in banner" :key="ele.id" :style="'background-image:url(http://localhost:53000/'+ele.img+')'"></div>
        </div>
        <!-- Add Pagination -->
        <div class="swiper-pagination swiper-pagination-white"></div>
      </div>
    </div>
    <div class="list">
      <div class="swiper-container2">
        <div class="swiper-wrapper">
          <div class="swiper-slide" v-for="(ele,index) in List" :key="index">
            <nuxt-link to='/search' v-for="ele1 in ele" :key="ele1.id">
              <img :src="'http://localhost:53000/'+ele1.img" :alt="ele1.title">
              <span>{{ele1.title}}</span>
            </nuxt-link>
          </div>
        </div>
        <!-- Add Pagination -->
        <div class="swiper-pagination"></div>
      </div>
    </div>
    <div class="main">
      <div class="course">
        <div>
          <h3>今天公开课</h3>
          <h4>Today's public class</h4>
        </div>
        <nuxt-link to="/search"><span>查看更多</span><i class="fa fa-caret-right"></i></nuxt-link>
      </div>
      <div class="public">
          <nuxt-link to='/search' v-for="ele in Public" :key="ele.id" :class="ele.title"><img :src="'http://localhost:53000/'+ele.img" :alt="ele.title"></nuxt-link>
      </div>
      <div class="improveQuick">
        <nuxt-link to='/search' v-for="(ele,index) in Today" :key="index">
          <p>{{ele.title}}</p>
          <div>
            <img :src="'http://localhost:53000/'+ele.img" alt="person">
            <span>{{ele.name}}</span>
            <img src="https://shared-https.ydstatic.com/ke/wap/v2.4.5/9cf788d02d34169fbdf84bf744f7072a.png" alt="detail">
          </div>
        </nuxt-link>
      </div>
      <div class="course">
        <div>
          <h3>课程精选</h3>
          <h4>Course selection</h4>
        </div>
        <nuxt-link to="/search"><span>查看更多</span><i class="fa fa-caret-right"></i></nuxt-link>
      </div>
      <div class="selection">
        <nuxt-link to='/search' v-for="(ele,index) in Selection" :key="ele.id">
          <div class="kemu">
            <span class="kemuName">{{ele.kemuName}}</span>
            <span class="CLASSNAME">{{ele.CLASSNAME}}</span>
          </div>
          <div class="time">
            <span>开课时间：{{ele.startTime}}</span>
            <span class="keshi">{{ele.keshi}}</span>
          </div>
          <div class="info">
            <div class="teachers">
              <div class="teacher" v-for="ele1 in ele.teacher" :key="ele1._id">
                <img :src="'http://localhost:53000/'+ele1.img" alt="teacher">
                <span>{{ele1.name}}</span>
              </div>
            </div>
            <div class="info1">
              <div class="money" v-if="ele.newPrice">
                <del v-if="ele.oldPrice">¥{{ele.oldPrice}}</del>
                <span>¥<span class="discount">{{ele.newPrice}}</span></span>
              </div>
              <div class="money" v-else>
                <i class="over">售罄</i>
              </div>
              <div class="time1" v-if="ele.endTime">
                剩<span>{{Time[index]}}</span>恢复原价
              </div>
              <div class="time1" v-if="ele.number">
                已有{{ele.number}}人购买
              </div>
            </div>
          </div>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import Swiper from "swiper";
import "swiper/css/swiper.min.css";
import  axios from "axios"
export default {
  data(){
    return{
      Time:[],
      banner:[],
      list:[],
      List:[],
      Public:[],
      Today:[],
      Selection:[]
    }
  },
  methods:{
    double(obj){
      if(obj<10){
        return "0"+obj
      }else{
        return obj
      }
    },
    endTime(endtime,index){
        var time,day,hour,minute,second,time1;
        time = new Date(endtime).getTime()-new Date().getTime();
        if(time*1>0){
          day = parseInt(time / (1000 * 24 * 3600)); //剩余天数
          hour = parseInt((time / (1000 * 24 * 3600)-day)*24); //剩余小时
          minute = parseInt(((time / (1000 * 24 * 3600)-day)*24-hour)*60); //剩余分钟
          second = parseInt((((time / (1000 * 24 * 3600)-day)*24-hour)*60-minute)*60);  //剩余秒数
          if(day == "0"){
            time1 = this.double(hour)+":"+this.double(minute)+":"+this.double(second);
          }else{
            time1 = day+"天"+this.double(hour)+":"+this.double(minute)+":"+this.double(second);
          }
          this.Time[index]=time1;
        }else{
          time1="活动已结束"
        }
      return time1;
    }
  },
  async mounted() {
    setTimeout(()=>{
      new Swiper(".swiper-container", {
        loop: true,
        autoplay: { delay: 1500, disableOnInteraction: false },
        pagination: {
          el: ".swiper-pagination",
          clickable: true
        }
      });
      new Swiper(".swiper-container2", {
        pagination: {
          el: ".swiper-pagination",
          clickable: true
        }
      });
    },1000)
    let { data } = await axios.get('http://localhost:53000/goods');
    this.banner = data.banner;
    this.list = data.list;
    this.Public = data.public;
    this.Today = data.today;
    this.Selection = data.selection;
    if(this.list.length>8){
      var num = parseInt(this.list.length/8);
      for(var i=0;i<num;i++){
        this.List[i]=this.list.splice(0,8)
      }
      this.List.push(this.list);
    }else{
      this.List.push(this.list);
    }
    setInterval(()=>{
      this.Time = [];
      this.Selection.map((ele,index)=>{
        // console.log(!!ele.endTime);
        if(!!ele.endTime){
          this.endTime(ele.endTime,index)
        }
      })
    },1000)
  }
};
</script>

<style lang="scss" scoped>
.header {
  position: absolute;
  top: 0;
  left: 0;
  height: 1rem;
  width: 100%;
  background: transparent;
  display: flex;
  justify-content: space-around;
  align-items: center;
  z-index: 100;
  .search {
    display: block;
    height: 0.6rem;
    line-height: 0.6rem;
    width: 5.76rem;
    text-indent: 0.2rem;
    color: gray;
    background: whitesmoke;
    border-radius: 0.1rem;
    i {
      margin-right: 0.2rem;
    }
  }
  .user {
    i {
      font-size: 0.4rem;
    }
  }
}
.banner {
  height: 5.47rem;
  .swiper-container {
    width: 100%;
    height: 100%;
  }
  .swiper-slide {
    background-position: center;
    background-size: cover;
  }
  .swiper-pagination {
    text-align: right;
    position: absolute;
    top: 3rem;
  }
}
.list{
  height: 3.5rem;
  width: 6.66rem;
  background: white;
  margin: 0 auto;
  position: relative;
  top: -2rem;
  z-index: 100;
  overflow: hidden;
  .swiper-container2 {
    width: 100%;
    height: 2.9rem;
  }
  .swiper-slide {
    display: flex;
    flex-wrap: wrap;
    a{
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 50%;
      width: 25%;
      img{
        width: .61rem;
        height: .61rem;
        margin-bottom: .1rem;
      }
    }
  }
}
.main{
  position: relative;
  top: -1.7rem;
  width: 6.66rem;
  margin:0 auto;
  .course{
    display: flex;
    height: .8rem;
    border-left: .1rem solid red;
    justify-content: space-between;
    align-items: center;
    margin-bottom: .4rem;
    div{
      margin-left: .2rem;
      h4{
        color: #afafaf;
        font-size: .24rem;
      }
    }
    a{
      color: #afafaf;
      font-size: .28rem;
    }
  }
  .public{
    overflow: hidden;
    a{
      display: inline-block;
      width: 3.33rem;
    }
    .xueba{
      height: 4.34rem;
      float: left;
      img{
        width: 100%;
        height: 100%;
      }
    }
    .fayu,.siliu{
      height: 2.17rem;
      img{
        width: 100%;
        height: 100%;
      }
    }
  }
  .improveQuick{
    display: flex;
    flex-wrap: wrap;
    margin-bottom: .4rem;
    a{
      display: block;
      width: 50%;
      height: 2.1rem;
      p{
        color: #36404a;
        font-size: .32rem;
        padding: .2rem .2rem 0;
      }
      div{
        display: flex;
        height: .48rem;
        justify-content: space-around;
        align-items: center;
        padding: .3rem .2rem;
        img{
          height: 100%;
          border-radius: 50%;
        }
        span{
          color: #a6acb1;
        }
      }
    }
  }
  .selection{
    a{
      display: block;
      height: 2.06rem;
      padding: .4rem 0;
      .kemu{
        .kemuName{
          display: inline-block;
          background: #838d98;
          color: white;
          width: 1.04rem;
          height: .36rem;
          text-align: center;
          border-radius: .1rem;
          margin-right: .2rem;
        }
        .CLASSNAME{
          color: #36404a;
          font-size: .32rem;
        }
      }
      .time{
        padding: .2rem 0;
        .keshi{
          margin-left: .2rem;
        }
      }
      .info{
        height: .93rem;
        display: flex;
        justify-content: space-between;
        align-items: center;
        .teachers{
          display: flex;
          .teacher{
            display: flex;
            flex-direction: column;
            margin-right: .2rem;
            align-items: center;
            img{
              width: .46rem;
              height: .46rem;
              border-radius: 50%;
            }
          }
        }
        .info1{
          text-align: right;
          .money{
            .over{font-size: .35rem;}
            span{
              color: #ff773a;
              font-weight: bold;
              margin-left: .2rem;
              .discount{
                margin-left: .02rem;
                font-size: .35rem;
              }
            }
          }
        }
      }
    }
  }
}
</style>
