<template>
  <!-- 收藏页第一栏 -->
  <div class="aside-subs">
    <el-card class="subs-card">
      <div>
        <div class="subsNum">
          <div class="subsM">关注者</div>
          <div class="subsN">{{subNum}}</div>
        </div>
        <el-divider direction="vertical"></el-divider>
        <div class="queNum">
          <div class="queM">问题数</div>
          <div class="queN">{{quenum}}</div>
        </div>
      </div>
    </el-card>
    <el-card class="F-S-card">
      <div>
        <div>
          <div class="Ftitle">父话题</div>
          <div>
            <el-button type="text">
              <el-tag class="Ftag">{{Ftop.topicName}}</el-tag>
            </el-button>
          </div>
        </div>
        <div>
          <div class="Ftitle" style="margin-top:20px;">子话题</div>
          <div style="width:250px;margin-left:-7px;">
            <el-button
              type="text"
              v-for="Sontop in SonTops"
              :key="Sontop.topicId"
              style="margin-left: 10px;"
            >
              <el-tag class="Ftag">{{Sontop.topicName}}</el-tag>
            </el-button>
          </div>
        </div>
      </div>
    </el-card>
  </div>
</template>

<script>
import { reqGetFathTop } from "../../api/topicFS";
import { reqGetSonTop } from "../../api/topicFS";
export default {
  name: "asideSubs",
  props: {
    topicId: String,
    quenum: Number
  },
  data() {
    return {
      subNum: "2",
      // queNum: "31231",
      // Ftop: '教育',
      // Sontops: [
      //   { topic: '高考志愿' },
      //   { topic: '高考的高超技巧' },
      //   { topic: '理工' },
      //   { topic: '高考志愿123' },
      //   { topic: '高考的高超技巧1' },
      //   { topic: '理工123' }
      // ]
      Ftop: "",
      SonTops: []
    };
  },
  mounted() {
    this._loadData();
  },
  methods: {
    _loadData() {
      let params = "topicId=" + this.topicId;
      // console.info(this.topicId);
      reqGetFathTop(params).then(res => {
        if (res.resultCode === 200) {
          // console.info(res.data);
          this.Ftop = res.data;
          //console.info(this.Ftop);
        }
      });
      reqGetSonTop(params).then(res => {
        if (res.resultCode === 200) {
          //console.info(res.data);
          this.SonTops = res.data;
          //console.info(this.SonTops);
        }
      });
    }
  }
};
</script>

<style lang="scss">
.aside-subs {
  margin-top: 20px;
  .F-S-card {
    margin-top: 15px;
    .Ftitle {
      font-weight: bold;
      font-size: 15px;
      margin-bottom: 10px;
    }
    .Ftag {
      font-size: 14px;
      border-radius: 20px;
      margin-top: -10px;
      color: #0084ff;
      background: #0084ff1a;
    }
    el-buttion {
      margin-left: 0px;
    }
  }
  .subs-card {
    text-align: center;
    .el-card__body {
      padding: 15px;
    }
    .category-button {
      text-align: center;
      i {
        margin: 6px;
        font-size: 30px;
      }
    }
    .el-divider {
      height: 3em;
      margin-left: -20px;
    }
    .subsNum {
      float: left;
      width: 100px;
      margin-left: 10px;
      .subsM {
        color: #8590a6;
      }
      .subsN {
        font-size: 18px;
        color: #1a1a1a;
        font-weight: 600;
        margin-top: 3px;
      }
    }
    .queNum {
      float: right;
      widows: 100px;
      margin-right: 40px;
      .queM {
        color: #8590a6;
      }
      .queN {
        font-size: 18px;
        color: #1a1a1a;
        font-weight: 600;
        margin-top: 3px;
      }
    }
  }
}
</style>
