<template>
  <div class="section-box section-comment-box container">
    <div class="section-title">
      <h3>社区热贴</h3>
    </div>
    <div class="section-box-row">
      <div class="index-center-wrapper">
        <ul class="clearfix">
          <li class="phone1" v-for="(items) in phoneList " :key="items.id">
            <div class="section-item-box goods-box">
              <a
                class="box-img box-img-retina"
                href="https://bbs.meizu.cn/"
                target="_blank"
                data-mtype="gw_index_rp_1_1"
                data-bh="click_index_rp_1_1"
              >
                <div class="comment-img-wp">
                  <img
                    class="goods-img lazy-img loaded-img"
                    data-src="https://fms.res.meizu.com/dms/2019/02/28/dc6c4a26-479e-40ea-bde2-3c0ed2024d1c.jpg"
                    actived="actived"
                    v-lazy="items.commentImgWpUrl"
                  />
                </div>
                <div class="comment-user-info">
                  <img class="user-header" v-lazy="items.userHeaderUrl" alt />
                  <span class="comment-username">{{items.commentUserName}}</span>
                </div>
                <p>{{items.p}}</p>
                <span class="comment-tip">{{items.commentTip}}</span>
              </a>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      phoneList: [
        {
          id: "phoneList-0",
          commentImgWpUrl: require("../../public/imgs/Community/comment-img-wp-0.jpg"),
          userHeaderUrl: require("../../public/imgs/Community/user-header-0.jpeg"),
          commentUserName: "hooyeah",
          p: "魅族 Note9 邀请函 JK 服妹子出镜，谁才是最美游戏姬？",
          commentTip: "魅族 Note9"
        },
        {
          id: "phoneList-1",
          commentImgWpUrl: require("../../public/imgs/Community/comment-img-wp-1.jpg"),
          userHeaderUrl: require("../../public/imgs/Community/user-header-1.jpeg"),
          commentUserName: "xrx3p",
          p: "摄影离不开适当的后期，好在如今你可以在魅族手机上轻松完成操作。",
          commentTip: "摄影技巧"
        },
        {
          id: "phoneList-2",
          commentImgWpUrl: require("../../public/imgs/Community/comment-img-wp-2.jpg"),
          userHeaderUrl: require("../../public/imgs/Community/user-header-2.jpeg"),
          commentUserName: "小墨灰",
          p:
            "工作和学习中的沟通总离不开邮件，而 Flyme 邮箱的出色体验为我们带来的不只是生产力。",
          commentTip: "功能解析"
        },
        {
          id: "phoneList-3",
          commentImgWpUrl: require("../../public/imgs/Community/comment-img-wp-3.jpg"),
          userHeaderUrl: require("../../public/imgs/Community/user-header-3.jpeg"),
          commentUserName: "Keicy520",
          p: "妙用 Flyme 分身，做生活和工作的「两面派」。",
          commentTip: "功能解析"
        },
        {
          id: "phoneList-4",
          commentImgWpUrl: require("../../public/imgs/Community/comment-img-wp-4.jpg"),
          userHeaderUrl: require("../../public/imgs/Community/user-header-4.jpeg"),
          commentUserName: "歩惊云",
          p: "这款匠心精神打造的十五周年旗舰机，再不下手就要后悔啦~",
          commentTip: "魅族 15"
        },
        {
          id: "phoneList-5",
          commentImgWpUrl: require("../../public/imgs/Community/comment-img-wp-5.jpg"),
          userHeaderUrl: require("../../public/imgs/Community/user-header-5.jpeg"),
          commentUserName: "郑金龙",
          p:
            "千元最强性能手机登场，高通骁龙 710 次旗舰级处理器加持，玩王者荣耀 Vulkan 模式请认准魅族 X8。",
          commentTip: "魅族 X8"
        },
        {
          id: "phoneList-6",
          commentImgWpUrl: require("../../public/imgs/Community/comment-img-wp-6.jpg"),
          userHeaderUrl: require("../../public/imgs/Community/user-header-6.jpeg"),
          commentUserName: "屌丝扮海绵",
          p: "窗含西岭千秋雪” 魅族 16th 用旗舰双摄带你领略诗句中的美景。",
          commentTip: "魅族 16th"
        },
        {
          id: "phoneList-7",
          commentImgWpUrl: require("../../public/imgs/Community/comment-img-wp-7.jpg"),
          userHeaderUrl: require("../../public/imgs/Community/user-header-7.jpeg"),
          commentUserName: "醉刘的摄影狮",
          p: "“准旗舰游戏拍照手机魅族 X8，不止有实力，还有最美刘海屏！",
          commentTip: "魅族 X8"
        }
      ]
    };
  }
};
</script>
<style lang="scss">
.section-box {
  background: #f4f4f4;
  // margin-bottom: 50px;
  padding-bottom: 50px;
  width: 100%;
  height: 849px;
  .section-title {
    font-size: 30px;
    text-align: center;
    margin-bottom: 10px;
    h3 {
      font-size: 30px;
      font-weight: 400;
    }
  }
  .section-box-row {
    box-sizing: border-box;
    .index-center-wrapper {
      width: 1248px;
      margin: auto;
      ul {
        list-style: none;
        &::after,
        &::before {
          content: "";
          display: table;
          height: 0;
          clear: both;
          visibility: hidden;
        }

        li {
          list-style: none;
          height: 388px;
          float: left;
          position: relative;
          width: 303px;
          margin-right: 9px;
          margin-bottom: 9px;
          background-color: #fff;
          overflow: hidden;
          transition: all 0.3s ease;
          display: list-item;
          text-align: -webkit-match-parent;
          
          a.box-img {
            position: relative;
            display: block;
            width: 100%;
            height: 100%;
            text-align: center;
            background-repeat: no-repeat;
            background-position: 50%;
            text-decoration: none;
            color: #515151;

            .comment-img-wp {
              height: 190px;
              position: relative;
              overflow: hidden;

              img {
                display: block;
                margin: 0 auto;
                width: 100%;
                height: 100%;
                border: 0;
              }
            }

            .comment-user-info {
              overflow: hidden;
              height: 42px;
              line-height: 42px;
              margin-top: 10px;
              padding: 0 15px;

              img.user-header {
                box-sizing: border-box;
                width: 36px;
                height: 36px;
                border: 1px solid #fff;
                border-radius: 50%;
                float: left;
                box-shadow: 1px 1px 1px 1px #eee;
              }

              span.comment-username {
                margin-left: 15px;
                text-align: left;
                float: left;
                font-size: 14px;
                color: #515151;
              }
            }

            p {
              box-sizing: border-box;
              padding: 10px 15px 15px;
              font-size: 16px;
              line-height: 27px;
              text-align: left;
              height: 66px;
              display: -webkit-box;
              -webkit-box-orient: vertical;
              -webkit-line-clamp: 3;
              overflow: hidden;
              max-height: 100%;
            }

            span.comment-tip {
              font-size: 14px;
              color: #999;
              display: block;
              padding: 0 15px;
              margin-top: 10px;
              text-align: left;
            }
          }
        }
        li:hover {
            transition: opacity 0.2s linear;
            opacity: 0.8;
             box-shadow: 0px 0px 15px rgba(0,0,0,0.5);
          }
      }
    }
  }
}
</style>
