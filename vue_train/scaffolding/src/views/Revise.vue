<template>
  <div>
    <!-- 头部 -->
    <mt-header title="重置密码" class="header">
      <router-link to="/login" slot="left">
        <mt-button icon="back"></mt-button>
      </router-link>
    </mt-header>
    <div>
      <!-- 表单区域开始 -->
      <div class="bd">
        <mt-field
          class="biaodan"
          label="电话"
          placeholder="请输入11位号码"
          type="text"
          :attr="{ maxlength: 11 }"
          autocomplete="off"
          v-model="phone"
          :state="isphone"
          @blur.native.capture="checkPhone"
        ></mt-field>
        <mt-field
          class="biaodan"
          label="二代身份证"
          placeholder="请输入18位身份证号"
          type="text"
          :attr="{ maxlength: 18 }"
          autocomplete="off"
          v-model="user_card"
          :state="isuser_card"
          @blur.native.capture="checkCard"
        ></mt-field>
        <mt-field
          class="biaodan"
          label="新密码"
          placeholder="输入密码"
          type="password"
          :attr="{ maxlength: 16 }"
          autocomplete="off"
          v-model="upwd"
          :state="isupwd"
          @blur.native.capture="checkUpwd"
        ></mt-field>
        <mt-field
          class="biaodan"
          label="确认密码"
          placeholder="确认密码"
          type="password"
          :attr="{ maxlength: 15 }"
          autocomplete="off"
          v-model="conupwd"
          :state="isconupwd"
          @blur.native.capture="checkConupwd"
        ></mt-field>
      </div>
      <!-- 表单区域结束 -->
    </div>
    <mt-button class="dl" size="large" type="primary" @click="handle">确认</mt-button>
    <p class="ziti">温馨提示<br>新密码不能与原密码相同</p>
    <div id="tl"><p class="ziti">根据铁路部门要求，购买火车票需要实名制，请如实填写您的证件信息</p></div>
  </div>
</template>
<style>
  #tl>.ziti{
    background-color: #ddd;
  }
</style>
<script>
import { mapActions } from "vuex";
export default {
  data() {
    return {
      upwd: "",
      isupwd: "",
      conupwd: "",
      isconupwd: "",
      user_card: "",
      isuser_card: "",
      phone: "",
      isphone: "",
    };
  },
  methods: {
    checkCard() {
      //二代身份证
      let user_cardreg = /^\d{17}[0-9Xx]$/;
      if (user_cardreg.test(this.user_card)) {
        this.isuser_card = "success";
        return true;
      } else {
        this.isuser_card = "error";
        this.$toast({
          message: "请输入正确的身份证号", //内容
          position: "top", //位置
          duration: "2000", //2秒
        });
        return false;
      }
    },
    checkPhone() {
      //手机号码
      let phonereg = /^1[3-9]\d{9}$/;
      if (phonereg.test(this.phone)) {
        this.isphone = "success";
        return true;
      } else {
        this.isphone = "error";
        // 标准方式消息提示框
        this.$toast({
          message: "请输入正确的手机号", //内容
          position: "top", //位置
          duration: "2000", //2秒
        });
        return false;
      }
    },
    checkUpwd() {
      //密码
      let upwdreg = /^[0-9a-zA-Z]{8,16}$/;
      if (upwdreg.test(this.upwd)) {
        this.isupwd = "success";
        return true;
      } else {
        this.isupwd = "error";
        this.$toast({
          message: "请输入正确的密码格式", //内容
          position: "top", //位置
          duration: "2000", //2秒
        });
        return false;
      }
    },
    checkConupwd() {
      //校验两次密码
      if (this.upwd == this.conupwd && this.conupwd!="") {
        this.isconupwd = "success";
        return true;
      } else {
        this.$toast({
          message: "两次密码不一样",
          position: "top",
          duration: "2000",
        });
        return false;
      }
    },
    handle() {
      if (this.checkPhone &&this.checkCard && this.checkUpwd && this.checkConupwd) {
        this.axios
          .post(
            "/revise",
            "user_card=" + this.user_card + "&upwd=" + this.upwd
          )
          .then((res) => {
            if (res.data.code == 1) {
              this.$messagebox("注册提示", "别问,问就是不会");
              //this.$router.push("/register");
            } else {
              //用于显示提示框
              this.$messagebox("注册提示", "修改失败");
            }
          });
      }else{
        this.$messagebox("注册提示", "修改失败");
      }
    },
  },
  watch: {},
};
</script>