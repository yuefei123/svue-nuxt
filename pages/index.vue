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
          <div class="swiper-slide" v-for="(ele,index) in banner" :key="index" :style="'background-image:url(http://localhost:53000/'+ele.img+')'"></div>
        </div>
        <!-- Add Pagination -->
        <div class="swiper-pagination swiper-pagination-white"></div>
      </div>
    </div>
    <div class="list">
      <div class="swiper-container2">
        <div class="swiper-wrapper">
          <div class="swiper-slide" v-for="(ele,index) in banner" :key="index" :style="'background-image:url(http://localhost:53000/'+ele.img+')'"></div>
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
          <nuxt-link to='/search' class="xueba"><img src="/images/xueba.png" alt="xueba"></nuxt-link>
        <div>
          <nuxt-link to='/search' class="siliu"><img src="/images/siliu.png" alt="siliu"></nuxt-link>
          <nuxt-link to='/search' class="fayu"><img src="/images/fayu.png" alt="fayu"></nuxt-link>
        </div>
      </div>
      <div class="improveQuick">
        <nuxt-link to='/search'>
          <p>【中考物理】两字巧解电阻测量实验</p>
          <div>
            <img src="/images/person1.png" alt="person">
            <span>姜牧</span>
            <img src="/images/detail.png" alt="detail">
          </div>
        </nuxt-link>
        <nuxt-link to='/search'>
          <p>【中考物理】两字巧解电阻测量实验</p>
          <div>
            <img src="/images/person1.png" alt="person">
            <span>姜牧</span>
            <img src="/images/detail.png" alt="detail">
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
        <nuxt-link to='/search'>
          <div class="kemu">
            <span class="kemuName">逻辑英语</span>
            <span class="CLASSNAME">逻辑英语·系统3班</span>
          </div>
          <div class="time">
            <span>开课时间：2019-12-26 20:08:00</span>
            <span class="keshi">180课时</span>
          </div>
          <div class="info">
            <div class="teachers">
              <div class="teacher">
                <img src="/images/person1.png" alt="teacher">
                <span>钟平</span>
              </div>
              <div class="teacher">
                <img src="/images/person1.png" alt="teacher">
                <span>钟平</span>
              </div>
            </div>
            <div class="info1">
              <div class="money">
                <del>¥7560</del>
                <span>¥<span class="discount">3980</span></span>
              </div>
              <div class="time1">
                剩<span>{{Time[0]}}</span>恢复原价
              </div>
            </div>
          </div>
        </nuxt-link>
        <nuxt-link to='/search'>
          <div class="kemu">
            <span class="kemuName">逻辑英语</span>
            <span class="CLASSNAME">逻辑英语·系统3班</span>
          </div>
          <div class="time">
            <span>开课时间：2019-12-26 20:08:00</span>
            <span class="keshi">180课时</span>
          </div>
          <div class="info">
            <div class="teachers">
              <div class="teacher">
                <img src="/images/person1.png" alt="teacher">
                <span>钟平</span>
              </div>
              <div class="teacher">
                <img src="/images/person1.png" alt="teacher">
                <span>钟平</span>
              </div>
            </div>
            <div class="info1">
              <div class="money">
                <del>¥7560</del>
                <span>¥<span class="discount">3980</span></span>
              </div>
              <div class="time1">
                剩<span>{{Time[1]}}</span>恢复原价
              </div>
            </div>
          </div>
        </nuxt-link>
        <nuxt-link to='/search'>
          <div class="kemu">
            <span class="kemuName">逻辑英语</span>
            <span class="CLASSNAME">逻辑英语·系统3班</span>
          </div>
          <div class="time">
            <span>开课时间：2019-12-26 20:08:00</span>
            <span class="keshi">180课时</span>
          </div>
          <div class="info">
            <div class="teachers">
              <div class="teacher">
                <img src="/images/person1.png" alt="teacher">
                <span>钟平</span>
              </div>
              <div class="teacher">
                <img src="/images/person1.png" alt="teacher">
                <span>钟平</span>
              </div>
            </div>
            <div class="info1">
              <div class="money">
                <del>¥7560</del>
                <span>¥<span class="discount">3980</span></span>
              </div>
              <div class="time1">
                剩<span>{{Time[2]}}</span>恢复原价
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
      Endtime:["2019-12-15 16:00:00","2019-12-16 16:00:00","2019-12-17 15:00:00"],
      Time:[],
      banner:[]
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
    endTime(endtime){
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
          this.Time.push(time1);
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
    })
    setInterval(()=>{
      this.Time = [];
      this.Endtime.map((ele)=>{
        this.endTime(ele);
      })
    },1000)
    let { data } = await axios.get('http://localhost:53000/banner');
    // console.log(data);
    this.banner = data;
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
    background-position: center;
    background-size: cover;
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
    display: flex;
    a{
      display: block;
      width: 3.33rem;
    }
    .xueba{
      height: 4.34rem;
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
    a{
      display: block;
      width: 50%;
      height: 2.1rem;
      p{
        color: #36404a;
        font-size: .3rem;
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
            span{
              color: #ff773a;
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
