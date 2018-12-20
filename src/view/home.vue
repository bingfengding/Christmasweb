<template>
  <div id="home">
    <div class="modal" v-show="modalShow" @click="hideModal"></div>
    <div class="header">
      <div class="headerModal" v-show="headerModalShow"  @click="headerModalShow = false">
        <div class="videoBox" @click.stop>
          <video width="960" height="540" controls>
            <source src="../assets/christmas.mp4" type="video/mp4">
            您的浏览器不支持 video 标签。
        </video>
        </div>
      </div>
      <div class="center">
        <div class="textBox">
          <p>你许下心愿，我负责实现！金蛋100％获奖</p>
          <!-- <p>抽奖次数无限上限，点击<span class="ff8">查看详情</span></p> -->
        </div>
        <div class="videoImgBox">
          <div class="videoImg" @click="headerModalShow = true"></div>
        </div>
      </div>
    </div>
    <div class="main">
      <div class="winningBox" v-if="showWinning">
        <div class="winningClose" @click="closeWinning"></div>
        <div class="winningBg">
          <p class="text1">恭喜您!获得了一等奖</p>
          <p class="text2">
            <span>iPhone XS Max</span>
          </p>
          <div class="winningImg">
            <img src="../image/winning_img.png" alt="">
          </div>
        </div>
        <div class="winningTitle">
          <div class="winningCenter">
            <p class="text3">|  请注意查看站内信通知哦！</p>
          </div>
        </div>
      </div>
      <div class="numBox">
        <div class="numCen">
           <div class="num num1">
            {{numList.gift}}
          </div>
          <div class="num num2">
            {{numList.giftB}}
          </div>
          <div class="num num3">
            {{numList.giftC}}
          </div>
          <div class="num num4">
            {{numList.giftD}}
          </div>
          <div class="num num5">
            {{numList.giftE}}
          </div>
          <div class="num num6">
            {{numList.giftE}}
          </div>
          <div class="num num7">
            {{numList.giftE}}
          </div>
        </div>
       
      </div>
      
      <div class="knockBox">
        <div class="eggList">
          <div class="eggBox">
            <div class="hammer"  ref="hammer" :style="hammerStyle" :class="delayKnock?'knock':''"></div>
            <div class="ItemBox">
              <div class="egg" @click="knockEgg(index)" 
              v-for="(item,index) in eggList" :key="index"
              :class="knockIndex == index ? 'knockMe' : ''"
              >
              <img src="../image/egg3.gif" alt="" v-if="item.status===2" style="zIndex:1">
              <img src="../image/egg2.png" alt="" v-else-if="item.status===1" style="zIndex:10">
              <img src="../image/egg.png" alt="" v-else-if="item.status===0" style="zIndex:10">
              </div>
            </div>
          </div>
        </div>
        
      </div>
      <div class="luckyBox">
          <div class="residue itemBtn">您还有 <span>{{residue}}</span> 次抽奖机会</div>
          <div class="moreLucky itemBtn">获取更多抽奖机会</div>
        </div>
    </div>
    <div class="gameBox">
      <div class="itemBox">
        <div class="gameItemBox vr">
          <div class="item " @mouseover="hover('vr')" @mouseleave="leave('vr')"  @click="openUrl('vr')">
            <div class="animated text" :class="vrShow?'fadeInUp':'fadeOutDown'">
              VR彩票
            </div>
          </div>
          <p class="itemText">一个专业度与娱乐性兼具的权威彩票平台</p>
        </div>
        <div class="gameItemBox sport">
        <div class="item "  @mouseover="hover('sport')" @mouseleave="leave('sport')"  @click="openUrl('sport')">
          <div class="animated text" :class="sportShow?'fadeInUp':'fadeOutDown'">
            万博体育
          </div>
        </div>
        <p class="itemText">最有信誉的体育投注平台 官方推荐 安全买球</p>
        </div>
        <div class="gameItemBox eSports">
        <div class=" item"  @mouseover="hover('eSports')" @mouseleave="leave('eSports')"  @click="openUrl('eSports')">
          <div class="animated text" :class="eSportsShow?'fadeInUp':'fadeOutDown'">
            万博电竞
          </div>
        </div>
        <p class="itemText">热门游戏全覆盖 完美电竞体验</p>
        </div>
        <div class="gameItemBox chess">
          <p class="itemText">全球顶级棋牌竞技平台</p>
        <div class=" item"  @mouseover="hover('chess')" @mouseleave="leave('chess')"  @click="openUrl('chess')">
          <div class="animated text" :class="chessShow?'fadeInUp':'fadeOutDown'">
            万博棋牌
          </div>
        </div>
        </div>
      </div>
    </div>
    <div class="ruleBox">
      <div class="center">
        <div class="ruleTextBox" >
          <div class="prompt" @click="showInfo">友情建议</div>
          <div class="ruleInfo" v-show="infoShow">
             请于2018年12月24日（00:00:00）准点后参与累计存款。基于网络环境的不稳定性，为保障您可以正常参与活动，您需在2019年1月1日（23:59:59）前完成存款结算，请合理安排，为第三方平台/银行到账预留充分时间，这意味着，2019年1月2日（00:00:00）后到账的存款将不予与累计。感谢您的支持，祝您游戏愉快！
           </div>
          <div class="ruleItem" v-for="(item,index) in ruleTextList" :key="index">
            <p class="ruleTitle"> {{item.title}}</p>
            <p class="ruleText">{{item.content}}</p>
            <div class="textBox" v-if="item.text">
              <p v-for="(value,key) in item.text" :key="key">
                {{value}}
              </p>
            </div>
          </div>
          
        </div>
      </div>
    </div>
    <div class="moreBox">
      <div class="center">
        <div class="infoBox">
          <p class="infoTitle bold textCen">【敬请期待】</p>
          <p class="infoBold bold">亲爱的ManBetX万博会员，</p>
          <p class="infoBold bold">您好！</p>
          <p class="infoText">
            圣诞袜里的心愿单都如期实现了吗？为感恩各位一直以来对ManBetX万博的信任与支持， ManBetX万博年末回馈盛典继续接力！特此献上“好礼不停，金蛋不止”回馈活动！双“蛋”来袭，圣诞过后更有元旦，精彩游戏、神秘大礼轮番登场，惊喜一整年！节日加冕好运不停，幸运锦鲤伴您每一次的满足感都得到升华，与ManBetX万博一起祈愿新年吧！
          </p>
          <p class="infoBold bold">敬祝颂乐</p>
          <p class="infoBold bold lastInfo">ManBetX万博</p>
          <!-- <div class="moreBtn">
            <div class="btn">了解更多</div>
          </div> -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import posed from 'vue-pose'
import * as homeApi from "../api/home/home"
import { clearTimeout, setTimeout } from 'timers';
export default {
  data () {
    return {
      showWinning:false, // 弹出奖品窗口
      headerModalShow:false,  //header上的蒙层
      infoShow:false,
      modalShow:false,
      knockIndex:null,
      delayKnock:false,
      residue:0,
      hammerStyle:{
        top:"0",
        left:"",
      },
      knock:false,
      eggList:[
        {
          id:1,
          status:0
          },{
          id:2,
          status:0
          },{
          id:3,
          status:0
          },{
          id:4,
          status:0
        },
      ],
      numList:{
        gift:"0000",
        giftB:"0000",
        giftC:"0000",
        giftD:"0000",
        giftE:"0000",
        giftF:"0000",
        giftG:"0000",
        betAmount:"",
        betsNum:""
      },
      vrShow:false,
      sportShow:false,
      eSportsShow:false,
      chessShow:false,
      ruleTextList:[
        {
          title:"【砸金蛋专享时间】",
          content:"2018年12月24日00:00:00-2018年12月25日23:59:59，2019年1月1日00:00:00- 23:59:59，3天为砸金蛋日期。"
        },
        {
          title:"【砸金蛋参与条件】",
          content:"会员在2018年12月24日-2019年1月1日，每累计存款达到2520元即可有一次砸蛋机会（可多次累计）。",
           text:[
            "以上砸金蛋操作会员无需申请，满足条件即可在“砸金蛋专享时间”自行操作。",
     
            ]
        },
        {
          title:"【砸金蛋领取方式】",
          content:"所有获奖励的会员，系统都会统一发放站内信至站内邮箱告知您所获奖励名称，请您遵循站内信息提示进行后续操作。",
          text:[
            "本活动遵循<礼遇圣诞 乐惠元旦 ManBetX万博敬请尊享岁末狂欢盛宴>的【温馨提示】",
            "*所获红包仅需一倍流水不限平台。"
            ]
          
        },
       

      ]
     
    }
  },
  created(){
    homeApi.queryGift().then(res=>{
      if(res.status ===200) {
        let _base = res.data.result
        _base.giftB = "" + this.pad(_base.giftB, 4)
        _base.gift = "" + this.pad(_base.gift, 4)
        _base.giftC = "" + this.pad(_base.giftC, 4)
        _base.giftD = "" + this.pad(_base.giftD, 4)
        _base.giftE = "" + this.pad(_base.giftE, 4)
        // _base.giftF = "" + this.pad(_base.giftF, 4)
        // _base.giftG = "" + this.pad(_base.giftG, 4)
        this.numList = _base
      }
    })
    homeApi.userDrawNum("yili004").then(res=>{
      if(res.status === 200) {
        this.residue = res.data.result

      }
    })
  },
  computed:{
  
  },
  mounted(){
    this.$nextTick(()=>{
      window.addEventListener("mousemove",this.move)
    })
  },
  methods:{
    // 锤子跟随鼠标
    move(event){
      let e = event || window.event
      let scrollTop=document.documentElement.scrollTop||document.body.scrollTop
      let scrollLeft=document.documentElement.scrollLeft||document.body.scrollLeft
      let _obj = {
        top:(e.clientY - this.$refs.hammer.parentElement.offsetTop +scrollTop)+"px",
        left: (e.clientX - this.$refs.hammer.parentElement.offsetLeft +scrollLeft)+"px"
      }
      this.hammerStyle =  _obj
    },
    // 敲蛋动效
    knockEgg(index){
      console.time("砸蛋时长")
      if(!this.delayKnock){
        if(this.eggList[index].status === 0){

          this.eggList[index].status = 1 
          this.delayKnock = true
          this.knockIndex = index
          setTimeout(()=>{
            this.knockIndex = null
            this.delayKnock = false
          },500)
          
        }else if(this.eggList[index].status === 1) {
          
          this.delayKnock = true
          this.knockIndex = index
          homeApi.doDraw({userName:"yili004"}).then(res=>{
            if(res.status===200){
              if(res.data.status){
                this.knockIndex = null
                // 弹出奖品
                this.showWinning = true
                this.modalShow = true


                if(this.residue > 0 && this.residue !== null){
                  this.residue -= 1
                }
                this.eggList[index].status = 2
                setTimeout(()=>{
                  console.timeEnd("砸蛋时长")
                  this.eggList[index].status = 0
                  
                  this.delayKnock = false
                },1000)
                
                
              } else {
                this.knockIndex = null
                this.delayKnock = false
                this.eggList[index].status = 0
                window.top.alert(res.data.message)
              }
            }
          }).catch(
            error=>{
              this.knockIndex = null
              this.delayKnock = false
            }
          )
          
          // let timer = setTimeout(() => {
          //   this.knockIndex = null
          //   this.delayKnock = false
          //   alert("活动暂未开始")
          // }, 500);
          
        }
      }
      
      
    },
    // 悬浮
    hover(value){
      if(value==="vr"){
        this.vrShow = true
      }else if(value==="sport"){
        this.sportShow = true
      }else if(value==="eSports"){
        this.eSportsShow = true
      }else if(value==="chess"){
        this.chessShow = true
      }
      
    },
    // 离开
    leave(value){
      if(value==="vr"){
        this.vrShow = false
      }else if(value==="sport"){
        this.sportShow = false
      }else if(value==="eSports"){
        this.eSportsShow = false
      }else if(value==="chess"){
        this.chessShow = false
      }
    },
    // 显示提示信息
    showInfo(){
      this.modalShow = true
      this.infoShow = true
    },
    // 隐藏modal
    hideModal(){
      this.modalShow = false
      this.infoShow = false
      this.showWinning = false
    },
    // 隐藏header的modal
    // hideVideo(){
    //   this.headerModalShow = false
    // },
    // 关闭中奖框
    closeWinning(){
      this.showWinning = false
      this.modalShow = false
    },
    // 跳转链接
    openUrl(value){
      switch (value) {
        case "vr":
          window.top.open("http://cn.man984.com/lottery/keno")
          break;
        case "chess":
          window.top.open("http://cn.91manbet.net/liveCasino/cardgame")
          break;
        case "sport":
          window.top.open("http://cn.91manbet.net/sports/msports")
          break;
        case "eSports":
          window.top.open("http://cn.91manbet.net/game/index")
          break;
        default:
          break;
      }
    },
    // 转换为字符串
    pad(value,num){
      let _len = value.toString().length
      while(_len < num){
        value = "0" + value
        _len++
      }
      return value
    },
  },
  components: {

  }
 }
</script>

<style lang="stylus" scoped>
#home{
  position relative
  .modal {
    position absolute
    left 0
    right 0
    bottom 0
    top 0
    background-color rgba(0,0,0,0.8)
    z-index 100
  }
  .center{
    min-width 1200px
  }
  .header{
    height 1000px
    background url("../image/header_bg.png") no-repeat top center/cover
    color #555555
    font-size 21px
    text-align center
    position relative
    .headerModal {
      position absolute
      top 0
      left 0
      right 0
      bottom 0
      background-color rgba(0,0,0,0.7)
      display -webkit-flex
      display flex
      
      justify-content center
      align-items center
      cursor pointer
      .videoBox {
        padding-top 10px
        box-sizing content-box
        width 980px
        height 550px
        cursor auto
        background url("../image/video_bg.png") no-repeat center/100% 100%
      }
    }
    .center {
      width 100%
      height 100%
      display -webkit-flex
      display flex

      justify-content center
      .videoImgBox {
        width 1200px
        display -webkit-flex
        display flex
        align-items flex-end
        height 100%
        .videoImg {
          cursor pointer
          width 363px
          height 213px
          background url("../image/header_img.png") no-repeat center/100% 100%
        }
      }
    }
    .textBox{
      position absolute
      bottom 80px
      left 50%
      transform translateX(-50%)
      .ff8 {
        color #ff8f49
        cursor pointer
      }
    }
  }
  .main{
    height 1080px
    background url("../image/main_bg.png") no-repeat top center/cover
    .winningBox {
      position absolute
      left 50%
      transform translateX(-50%)
      top 1100px
      width 893px
      z-index 102
      .winningBg {
        position relative
        height 500px
        background url("../image/luck.png") no-repeat center/100% 100%
        .text1 {
          position absolute
          top 140px
          left 50%
          min-width 600px
          transform translateX(-50%)
          font-size 50px
          text-align center
          color #fbe6af
          text-shadow 0px 0px 12px #d73e38,0px 0px 12px #d73e38,0px 0px 12px #d73e38,0px 0px 12px #d73e38
        }
        .text2 {
          display flex
          display -webkit-flex
          width 100%
          position absolute
          top 220px
          left 50%
          min-width 600px
          transform translateX(-50%)
          justify-content center
          span {
            display inline-block
            width 270px
            height 60px
            text-align center
            line-height 60px
            font-size 24px
            color #fff

          }
        }
        .winningImg {
          position absolute
          top 270px
          left 50%
          transform translateX(-50%)
        }
        
      }
      .winningClose {
        cursor pointer
        width 74px
        height 74px
        background url("../image/luck_close.png") no-repeat center/100% 100%
        position absolute
        top 40px
        right 120px
        z-index 200
      }
      .winningTitle {
        position relative
        display flex
        display -webkit-flex
        justify-content center
        .winningCenter {
          margin-top -180px
          width 660px
          height 287px
          background url("../image/luck1.png") no-repeat center/100% 100%
          position relative
          .text3 {
            position absolute 
            left 190px
            top 166px
            color #fff
            font-size 32px
          }
        }
      }

    }
    .numBox {
      width 100%
      display -webkit-flex
      display flex
      justify-content center
      .numCen {
        width 1120px
        height auto
        position relative
      }
      .num {
        position absolute
        width 100px
        height 24px
        background url("../image/num_box.png") no-repeat center center
        line-height 24px
        font-size 21px
        color #fff
        letter-spacing 15px
        padding 0 4px

      }
      .num1 {
        left 540px
        top 65px
      }
      .num2 {
        left 242px
        top 110px
      }
      .num3 {
        left 774px
        top 128px
      }
      .num4 {
        left 142px
        top 242px
      }
      .num5 {
        left 950px
        top 250px
      }
      .num6 {
        left 1002px
        top 390px
      }
      .num7 {
        left 124px
        top 436px
      }
    }
   
    .knockBox{
      padding-top 200px
      width 100%
      height 860px
      display -webkit-flex
      display flex
      justify-content center
      align-items flex-end
      flex-wrap wrap
      overflow hidden
      cursor none
    }
    .luckyBox{
      height 220px
      width 100%
      display -webkit-flex
      display flex
      justify-content center
      align-items center
      .itemBtn {
        cursor pointer
        width 251px
        height 71px
        text-align center
        line-height 71px
        padding-top 10px
        font-size 20px
        color #ffffff
        background url("../image/main_btn.png") no-repeat center center/100% 100%
      }
      .residue {
        margin-right 40px
        span{
          color #bd2c22
        }
      }
    }
    .eggList{
      display flex
      display -webkit-flex
      justify-content center
      user-select none
      -webkit-user-drag none
      .eggBox{
        width 1000px
        height 600px
        
        position relative
        // overflow hidden
        display flex
        justify-content center
        align-items flex-end
        .ItemBox{
          display flex
          display -webkit-flex
          justify-content center
          @keyframes jitter {
            0% {
              transform rotateZ(-10deg)
            }
           
            
            
            100% {
              transform rotateZ(10deg)
            }
          }
          @keyframes shaking {
            0% {
              transform rotateZ(0)
            }
           
             25% {
              transform rotateZ(-10deg)
            }
            50% {
              transform rotateZ(0)
            }
             75% {
              transform rotateZ(10deg)
            }
            100% {
              transform rotateZ(0)
            }
          }
          .egg{
            margin 0 20px
            width 175px
            height 282px
            user-select none
            -webkit-user-drag none
            display -webkit-flex
            display flex
            
            justify-content center
            align-items flex-end
            // animation jitter 0.5s ease-in-out infinite alternate
            transform-origin center bottom
            
          }
          .knockMe {
            animation shaking 0.5s linear infinite
          }
        }
        
        @keyframes hammerAnimate {
          0% {
            
            transform translate(0,-50%) rotateZ(0)
          }
          100% {
            transform:translate(0,-50%) rotateZ(10deg)
          }
        } 
        @keyframes knockAnimate {
          0% {
            transform:translate(0,-50%) rotateZ(10deg)
          }
          100% {
            transform:translate(0,-50%) rotateZ(-80deg)
          }
        }
        .hammer{
          width 137px
          height 105px
          position absolute
          transform translate(0,-50%) rotateZ(0) 
          z-index 100
          background-image url("../image/hammer.png")
          left -100%
          top -100%
          transition rotate 0.3s ease-in 
          pointer-events:none;
          animation hammerAnimate 0.5s ease-in-out infinite alternate
          &.knock{
            animation knockAnimate 0.4s ease-in 1
          }
        }

      }
    }
  }
  .gameBox{
    background url("../image/game_bg.png") no-repeat top center/cover
    height 1080px
    display -webkit-flex
    display flex
    justify-content center
    .itemBox{
      width 1200px
      height 1080px
      position relative
      .gameItemBox{
        position absolute
        .itemText{
          color #555555
          font-size 18px
          padding 10px 0
        }
      }
      .item {
        cursor pointer
        box-sizing content-box
        display -webkit-flex
        display flex
        align-items flex-end
        overflow hidden
        border 10px solid #ffffff
        &:hover {
          border 10px solid #ffb15c
        }
        .text {
          width 100%
          background-color rgba(255,255,255,0.7)
          height 54px
          line-height 54px
          font-size 24px
          color #555555
          text-align center
        }
      }
      .vr {
        top 360px
        left 40px
        
        .itemText {
          width 274px
        }
        
        .item{
          width 254px
          height 372px
          background url("../image/game1.png") no-repeat center center/100% 100%
        }
      }
      .sport {
        top 305px
        left 365px
        .itemText {
          width 423px
        }
        .item{
          width 403px
          height 565px
          
          background url("../image/game2.png") no-repeat center center/100% 100%
        }
        
      }
      .chess {
        left 840px
        top 240px
        .itemText {
          width 199px
        }
        .item{
          width 179px
          height 179px
        
          background url("../image/game3.png") no-repeat center center/100% 100%
        }
        .itemText{
          text-align right
        }
        
      }
      .eSports {
        left 788px
        top 530px
        .itemText {
          width 377px
        }
        .item{
          width 357px
          height 254px
      
          background url("../image/game4.png") no-repeat center center/100% 100%
        }
        .itemText{
          text-align right
        }
        
      }
    }
  }
  .ruleBox{
    height 1080px
    background url("../image/rule_bg.png") no-repeat top center/cover
    display -webkit-flex
    display flex
    justify-content center
    .center {
      width 1200px
      padding-top 100px
      display -webkit-flex
      display flex
      justify-content center
      align-items center
      .ruleTextBox {
        width 1000px
        min-height 680px
        height auto
        padding 40px 40px 40px 60px
        background-color #ffffff
        color #555555
        position relative
        .ruleInfo {
          position absolute
          width 1000px
          padding 20px
          background-color #ffffff
          z-index 200
          left 0
          top 100px
        }
        .prompt {
          position absolute
          right 60px
          top 20px
          font-size 24px
          cursor pointer
          color #fdd883
          //transform scale(1)
          transition all 0.3s ease-out
          &:hover {
            transform scale(1.2)
            
          }
        }
        .ruleItem {
          padding-bottom 30px
          &:last-of-type {
            padding-bottom 0
          }
          .textBox {
            padding-left 44px
            font-size 20px
            p {
              padding-bottom 10px
            }
          }
        }
        
        .ruleTitle {
          font-size 20px
          font-weight 600
          vertical-align middle
          &::before {
            content url("../image/rule_icon.png")
            vertical-align middle
            display inline-block
          }
        }
        .ruleText{
          font-size 20px
          padding-left 44px
          padding-bottom 10px
        }
        
      }
    }
  }
  .moreBox {
    height 1080px
    background url("../image/more_info.png") no-repeat top center/cover
    display -webkit-flex
    display flex
    justify-content center
    align-items center
    .center {
      display -webkit-flex
      display flex
      justify-content center
      .infoBox {
        width 840px
        min-height 600px
        font-size 24px
        color #555555
        padding-top 50px
        .bold {
          font-weight 600

        }
        .infoText {
          padding-bottom 30px
        }
        .infoBold {
          padding-bottom 10px
        }
        .lastInfo {
          text-align right
        }
        .infoTitle {
          font-size 36px
          line-height 60px
        
        }
        .moreBtn {
          display -webkit-flex
          display flex
          justify-content center
          padding-top 20px
          .btn {
            padding-top 10px
            width 201px 
            font-size 20px
            color #ffffff
            height 69px
            line-height 69px
            text-align center
            background url("../image/more_btn.png") no-repeat top center/100% 100%
            cursor pointer
          }
        }
      }
    }
  }
}
</style>
