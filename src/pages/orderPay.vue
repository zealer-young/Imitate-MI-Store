<template>
  <div class="order-pay">
    <order-header title="订单支付">
      <template v-slot:tip>
        <span>谨防钓鱼链接或诈骗电话</span>
      </template>
    </order-header>
    <div class="wrapper">
      <div class="container">
        <div class="order-wrap">
          <div class="item-order">
            <div class="icon-succ"></div>
            <div class="order-info">
              <h2>订单提交成功！去付款咯～</h2>
              <p>请在<span>30分</span>内完成支付, 超时后将取消订单</p>
              <p>收货信息：{{addressInfo}}</p>
            </div>
            <div class="order-total">
              <p>应付总额：<span>{{payment}}</span>元</p>
              <p>订单详情<em class="icon-down" :class="{'up':showDetail}" @click="showDetail = !showDetail"></em></p>
            </div>
          </div>
          <div class="item-detail" v-if="showDetail">
            <div class="item">
              <div class="detail-title">订单号：</div>
              <div class="detail-info theme-color">{{orderId}}</div>
            </div>
            <div class="item">
              <div class="detail-title">收货信息：</div>
              <div class="detail-info">{{addressInfo}}</div>
            </div>
            <div class="item good">
              <div class="detail-title">商品名称：</div>
              <div class="detail-info">
                <ul>
                  <li v-for="(item,index) in list2" :key="index">
                    <img v-lazy="item.productImage"/>{{item.productName}}
                  </li>
                </ul>
              </div>
            </div>
            <div class="item">
              <div class="detail-title">发票信息：</div>
              <div class="detail-info">电子发票 个人</div>
            </div>
          </div>
        </div>
        <div class="item-pay">
          <h3>选择以下支付方式付款</h3>
          <div class="pay-way">
            <p>支付平台</p>
            <!-- <div class="pay pay-ali" :class="{'checked':payType==1}" @click="paySubmit(1)"></div> -->
            <!-- <div class="pay pay-wechat" :class="{'checked':payType==2 }" @click="paySubmit(2)"></div> -->
            <div class="pay pay-wechat" :class="{'checked':payType==2 }" @click="paySubmit()"></div>
          </div>
        </div>
      </div>
    </div>
    <scan-pay-code v-if="showPay" @close="closePayModal" v-bind:img="payImg"></scan-pay-code>
    <modal
    title="支付确认"
    btnType="3"
    :showModal="showPayModal"
    sureText="查看订单"
    cancleText="未支付"
    @cancel="showPayModal=false"
    @submit="getOrderList"
    >
    <template v-slot:body>
      <p>您确认是否完成支付？</p>
    </template>
    </modal>
  </div>
</template>
<script>
// import QRCode from 'qrcode'
import OrderHeader from './../components/OrderHeader'
import ScanPayCode from './../components/ScanPayCode'
import Modal from './../components/Modal'
export default{
  name:'order-pay',
  data(){
    return {
      orderId:this.$route.query.orderNo,//获取订单编号
      addressInfo:'',//收货人地址信息
      orderDetail:[],//订单详情中，包含商品列表
      showDetail:false,//是否显示订单详情，默认是false
      payType:'',//支付类型
      showPay:false,//是否显示微信支付弹框
      payImg:'',//微信支付的二维码地址
      showPayModal:false,//是否显示二次支付确认弹框
      payment:0,//订单总金额
      T:'',//定时器id
      list2:[],
    }
  },
  components:{
    OrderHeader,
    ScanPayCode,
    Modal
  },
  mounted(){
    this.getOrderDetail();
  },
  methods:{
    //获取订单详情
   getOrderDetail(){
      this.axios.get(`/orders/${this.orderId}`).then((res)=>{
        let item = res.shippingVo;
        this.addressInfo = `${item.receiverName} ${item.receiverMobile} ${item.receiverProvince} ${item.receiverCity} ${item.receiverDistrict} ${item.receiverAddress}`;
        this.orderDetail = res.orderItemVoList;
        this.payment = res.payment;
        let list = this.orderDetail;
        for(let item of list){
        if(item.productId===30){
          item.productName = '魅族 17';
          item.productImage = 'https://openfile.meizu.com/group1/M00/07/C4/Cgbj0F6zwMuANEeWAAw6yQFAJXM097.png@240x240.jpg';
        }
        if(item.productId===31){
          item.productName = '魅族 17 Pro';
          item.productImage = 'https://openfile.meizu.com/group1/M00/07/C5/Cgbj0F6zwUqAdPsoAAtCAjTT7ek670.png@240x240.jpg'
        }
        if(item.productId===32){
          item.productName = '魅族 17 Pro 晓芳窑艺术典藏版';
          item.productImage = 'https://openfile.meizu.com/group1/M00/07/CF/Cgbj0F61BXaARxdvAAqWtjjyY08964.png@240x240.jpg'
        }
        if(item.productId===33){
          item.productName = '魅族16T';
          item.productImage = 'https://openfile.meizu.com/group1/M00/07/62/Cgbj0F2upwyAKqQSAAlGpvLiEdc809.png@240x240.jpg'
        }
        if(item.productId===34){
          item.productName = '魅族 16Xs';
          item.productImage = 'https://openfile.meizu.com/group1/M00/07/2C/Cgbj0FzvRI6AWu1jAAxIbnS8M5Q295.png@240x240.jpg'
        }
        if(item.productId===35){
          item.productName = '魅族 16th';
          item.productImage = 'https://openfile.meizu.com/group1/M00/05/E2/Cgbj0FtqgnmAFgJPAAhgnScaoFg724.png@240x240.jpg'
        }
        if(item.productId===36){
          item.productName = '魅族 X8';
          item.productImage = 'https://openfile.meizu.com/group1/M00/06/A9/Cgbj0FusSK2AQZgiAAlFKHoO-co889.png@240x240.jpg'
        }
        if(item.productId===37){
          item.productName = '魅族 16 X';
          item.productImage = 'https://openfile.meizu.com/group1/M00/06/BC/Cgbj0FvINLWACd0AAAh2dGv5_R0516.png@240x240.jpg'
        }
      }
      this.list2 = list;
      })
    },
    //支付提交
    // paySubmit(payType){
    //   if (payType == 1) {//支付宝跳转
    //     window.open('/#/order/alipay?orderId='+this.orderId,'_blank')
    //   }else{//支付宝跳转
    //     this.axios.post('/pay',{
    //       orderId:this.orderId,
    //       orderName:"Vue高仿小米商城",
    //       amount:0.01,//单位元
    //       payType:2,//1.支付宝 2.微信
    //     }).then((res)=>{
    //       QRCode.toDataURL(res.content)//将res.content的内容转化为图片地址
    //       .then(url =>{
    //         this.showPay = true;//显示微信支付弹框
    //         this.payImg = url;//二维码生成
    //         this.loopOrderState();//轮询当前订单支付状态
    //       })
    //       .catch(() => {
    //         this.$message.error('微信二维码生成失败，请稍后重试')
    //       })
    //     })
    //   }
    // },
    paySubmit(){
      this.showPay = true;//显示微信支付弹框
      this.payImg = require("../../public/imgs/qrcode.png")//二维码生成
    },
    //关闭微信支付弹框
    closePayModal(){
      this.showPay = false;
      this.showPayModal = true;
      clearInterval(this.T);
    },
    //轮询当前订单支付状态
    //订单状态：0-已取消，10-未付款，20-已付款，40-已发货，50-交易成功，60-交易关闭
    loopOrderState(){
      this.T = setInterval(()=>{
        this.axios.get(`/orders/${this.orderId}`).then((res)=>{
          if (res.status == 20) {
            clearInterval(this.T);
            this.getOrderList();
          }
        })
      },1000)
    },
    //获取订单列表
    getOrderList(){
      this.$router.push('/order/list')
    },
  }
}
</script>
<style lang="scss">
  .order-pay{
    .wrapper{
      background-color:#F5F5F5;
      padding-top:30px;
      padding-bottom:61px;
      .order-wrap{
        padding: 62px 50px;
        background-color: #fff;
        font-size:14px;
        margin-bottom:30px;
        .item-order{
          display: flex;
          align-items: center;
          .icon-succ{
            width: 90px;
            height: 90px;
            border-radius: 50%;
            background:url('/imgs/icon-gou.png') #80c58a no-repeat center;
            background-size:60px;
            margin-right:40px;
          }
          .order-info{
            margin-right: 248px;
            h2{
              font-size:24px;
              color:#333333;
              margin-bottom:20px;
            }
            p{
              color:#666666;
              span{
                color:#e02b41;
              }
            }
          }
          .order-total{
            &>p:first-child{
              margin-bottom:30px;
            }
            span{
              color: #e02b41;
              font-size: 20px;
              font-weight: bolder;
            }
            .icon-down{
              display:inline-block;
              width:14px;
              height:10px;
              background:url('/imgs/icon-down.png') no-repeat center;
              background-size:contain;
              margin-left:9px;
              transition:all .5s;
              cursor:pointer;
              &.up{
                transform: rotate(180deg);
              }
            }
            .icon-up{
              transform: rotate(180deg);
            }
          }
        }
        .item-detail{
          border-top: 1px solid #D7D7D7;
          padding-top: 47px;
          padding-left: 130px;
          font-size: 14px;
          margin-top: 45px;
          .item{
            margin-bottom:19px;
            .detail-title{
              float:left;
              width:100px;
            }
            .detail-info{
              display:inline-block;
              img{
                width: 30px;
                vertical-align: middle;
              }
            }
          }
        }
      }
      .item-pay{
        padding:26px 50px 72px;
        background-color:#ffffff;
        color: #333333;
        h3{
          font-size: 20px;
          font-weight: 200;
          color: #333333;
          padding-bottom: 24px;
          border-bottom: 1px solid #D7D7D7;
          margin-bottom: 26px;
        }
        .pay-way{
          font-size:18px;
          .pay{
            display:inline-block;
            width:188px;
            height:64px;
            border:1px solid #D7D7D7;
            cursor:pointer;
            &:last-child{
              margin-left:20px;
            }
            &.checked{
              border:1px solid #188ffc;
            }
          }
          .pay-ali{
            background:url('/imgs/pay/icon-ali.png') no-repeat center;
            background-size:103px 38px;
            margin-top:19px;
          }
          .pay-wechat{
            background:url('/imgs/pay/icon-wechat.png') no-repeat center;
            background-size:103px 38px;
          }
        }
      }
    }
  }
</style>
