<template>
  <div class="Index">
    <!-- 头部 -->
    <div class="header"></div>
    <!-- 内容 -->
    <div class="center">
      <div class="content">
        <div class="logo">
          <!-- logo部分 -->
          <div class="img">
            <img src="../assets/logo.png" alt />
            <h3>查询验证系统（持证人员查询）</h3>
          </div>
        </div>
        <!-- 主体区域 -->
        <div class="text">
          <!-- 主体左边 -->
          <div class="left">
            <div class="left-hea">
              <p>证书查询</p>
            </div>
            <!-- 表单 -->
            <div class="form">
              <el-form
                :label-position="labelPosition"
                :rules="rules"
                ref="ruleForm"
                label-width="80px"
                :model="formLabelAlign"
              >
                <el-form-item label="姓名" prop="name">
                  <el-input v-model="formLabelAlign.name"></el-input>
                </el-form-item>
                <el-form-item label="身份证" prop="idCards">
                  <el-input v-model="formLabelAlign.idCards"></el-input>
                </el-form-item>
                <el-form-item label="证书编号">
                  <el-input v-model="formLabelAlign.certificateNo"></el-input>
                </el-form-item>
                <el-form-item>
                  <el-button type="primary" @click="onSubmit('ruleForm')">查询</el-button>
                </el-form-item>
              </el-form>
            </div>
          </div>
          <!-- 主体右边 -->
          <div class="right">
            <div class="cont"></div>
            <div class="right-text">
              <p>友情提示</p>
            </div>
            <div class="chaXun">
              <p class="p-1">查询说明</p>
              <p class="p-2">1、姓名、身份证号、证书编号至少输入两项，姓名为必填项</p>
              <p class="p-3">2、未经过中国电子信息行业专业人才培训工程组织的培训和考试、考试未合格，不能取得此证书</p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- 尾部 -->
    <div class="footer">
      <div class="footer-text">版权所有：中国电子工业标准化技术协会教育培训委员会</div>
    </div>
  </div>
</template>
<!-- 引入element组件库 -->
<script src="https://unpkg.com/element-ui/lib/index.js"></script>

<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script>
import baserUrl from "../api/config";
import config from "../api/config";
export default {
  name: "Index",
  components: {},
  data() {
    return {
      labelPosition: "left",
      name: "13732141234",
      pass: "123456",
      formLabelAlign: {
        name: "",
        idCards: "",
        certificateNo: ""
      },
      rules: {
        name: [{ required: true, message: "请输入姓名", trigger: "blur" }],
        idCards: [
          { min: 18, max: 18, message: "身份证输入有误", trigger: "blur" }
        ]
      }
    };
  },
  methods: {
    //点击查询按钮
    onSubmit(formName) {
      //将文本框获取到的内容，存到obj里
      var object = {
        name: this.formLabelAlign.name,
        certificateNo: this.formLabelAlign.certificateNo,
        idCards: this.formLabelAlign.idCards
      };
      //转字符串
      var query = JSON.stringify(object);
      //判断姓名是否输入
      if (this.formLabelAlign.name == "") {
        //如果姓名为空，提示警告框
        this.$refs[formName].validate(valid => {
          if (valid) {
          } else {
            return false;
          }
        });
        //查询条件不成立，提示弹框
        this.$alert("输入信息有误，请核对信息", "错误", {
          confirmButtonText: "确定"
        });
        //判断身份证和证书编号是否为空
      } else if (
        this.formLabelAlign.idCards == "" &&
        this.formLabelAlign.certificateNo == ""
      ) {
        this.$alert("身份证号和证书号二选一", "错误", {
          confirmButtonText: "确定"
        });
      } else {
        //判断如果条件成立的话，就发送请求
        this.$axios
          .post(
            `${baserUrl.baseUrl}/certificate/get?name=${this.formLabelAlign.name}&idCards=${this.formLabelAlign.idCards}&certificateNo=${this.formLabelAlign.certificateNo}`
          )
          .then(res => {
            //如果返回数据为空
            if (res.data == "") {
              this.$alert("输入信息有误，请核对信息", "错误", {
                confirmButtonText: "确定"
              });
              //数据正确，数据存储，跳转页面
            } else {
              this.$message({
                message: "查询成功",
                type: "success"
              });
              //在请求成功之后就数据存储到会话存储里面
              window.sessionStorage.setItem("data", JSON.stringify(res.data));
              this.$router.push({
                path: `/Result`
              });
            }
          });
      }
    }
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
  background: #fef6f2;
}

.content {
  width: 62%;
  height: 100%;
  margin: 0 auto;
}
.logo {
  width: 100%;
  height: 140px;
  border-bottom: 1px solid #c0c0c0;
}
.img {
  width: 88%;
  height: 80px;
  margin: 0 auto;
  text-align: center;
}
.img img {
  width: 100%;
  height: 100%;
}
.img h3 {
  color: #ee4135;
}
.text {
  width: 90%;
  height: 320px;
  background: #ffffff;
  margin: 50px auto 0;
  box-shadow: 0px 0px 7px 0px rgba(0, 0, 0, 0.5),
    -10px 10px 10px 10px rgba(250, 250, 250, 0);
}
.text .left {
  width: 50%;
  height: 100%;
  float: left;
}
.left-hea {
  text-align: center;
  line-height: 60px;
}
.left-hea p {
  font-size: 24px;
}
.text .right {
  width: 50%;
  height: 100%;
  float: right;
}
.right .cont {
  height: 70%;
  border-left: 1px solid #c0c0c0;
  margin-top: 15%;
  float: left;
}
.right-text {
  width: 99%;
  margin: 12px auto 0;
}
.right-text p {
  text-align: center;
  color: #ee4135;
  font-size: 20px;
}
.chaXun {
  margin: 4px 0;
}
.p-1 {
  font-size: 14px;
}
.p-2 {
  font-size: 12px;
  margin: 8px 0;
}
.p-3 {
  color: #ee4135;
  font-size: 12px;
}

/* 表单 */
.form {
  width: 80%;
  text-align: center;
  margin: auto;
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
