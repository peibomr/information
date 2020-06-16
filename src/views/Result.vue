<template>
  <div>
    <!-- 头部 -->
    <div class="header"></div>
    <!-- 内容 -->
    <div class="center">
      <div class="img">
        <img src="../assets/result.png" alt />
        <div class="text">
          <p class="p1">{{arr.certificateName}}</p>
          <p class="p2">{{arr.name}}</p>
          <p class="p3">{{arr.idCards}}</p>
          <p class="p4">{{arr.certificateNo}}</p>
          <p class="p5">{{this.tme}}</p>
        </div>
      </div>
    </div>
    <!-- 尾部 -->
    <div class="footer">
      <div class="footer-text">版权所有：中国电子工业标准化技术协会教育培训委员会</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      arr: {},
      time: "",
      tme: ""
    };
  },
  methods: {},
  created() {
    //获取会话存储的内容，并赋值
    this.arr = JSON.parse(sessionStorage.getItem("data"));
    //将数组里面的时间戳转换为年月日
    this.time = new Date(this.arr.createDate);
    //将时间戳转换为年
    var year = this.time.getFullYear();
    //将时间戳转换为月
    var month = this.time.getMonth() + 1;
    this.tme = year + "年" + month + "月";
  }
};
</script>
<style scoped>
/* 头部 */
.header {
  width: 100%;
  height: 6px;
  background: #ee4135;
}
/* 中间 */
.center {
  width: 100%;
  height: 544px;
}
.img {
  width: 80%;
  height: 100%;
  margin: 0 auto;
  position: relative;
}
.img img {
  width: 100%;
  height: 100%;
}
.text {
  width: 26%;
  height: 196px;
  position: absolute;
  right: 117px;
  /* background: red; */
  top: 208px;
}
.p1 {
  margin-top: 7px;
}
.p2 {
  margin-top: 22px;
}
.p3 {
  margin-top: 24px;
}
.p4 {
  margin-top: 22px;
}
.p5 {
  margin-top: 21px;
}
p {
  text-align: center;
}
/* 底部 */
.footer {
  width: 100%;
  height: 58px;
  background: #ee4135;
}
.footer-text {
  width: 50%;
  height: 100%;
  text-align: center;
  margin: auto;
  line-height: 58px;
  color: #ffffff;
}
</style>
