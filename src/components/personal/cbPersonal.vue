<template>
  <div class="personal">
    <el-row :gutter="20" style="margin:0">
      <el-col :xs="6" :sm="6" :md="6" :lg="6" class="perLeft">
        <div class="title">
          <span>个人资料</span>
        </div>
        <div class="headimg">
          <img src="../../assets/img/user.jpg" alt>
          <a href="javascript:;">修改头像</a>
        </div>
        <ul class="infoList">
          <li>
            <div class="left">
              <span></span>
              登录名称:
            </div>
            <div class="user">{{ userInfo.userName }}</div>
          </li>
          <li>
            <div class="left">
              <span></span>
              手机号码:
            </div>
            <div class="tel">{{ userInfo.tel }}</div>
          </li>
          <li>
            <div class="left">
              <span></span>
              所属部门:
            </div>
            <div class="depart">{{ userInfo.part }}</div>
          </li>
          <li>
            <div class="left">
              <span></span>
              邮箱地址:
            </div>
            <div class="eamil">{{ userInfo.email }}</div>
          </li>
          <li>
            <div class="left">
              <span></span>
              创建时间:
            </div>
            <div class="createTime">{{ userInfo.joinTime }}</div>
          </li>
        </ul>
      </el-col>
      <el-col :xs="12" :sm="15" :md="16" :lg="17" v-loading="loading">
        <div class="title">
          <span>基本资料</span>
        </div>
        <el-tabs type="border-card">
          <el-tab-pane label="基本资料">
            <el-form ref="form" :model="form" label-width="80px">
              <el-form-item label="用户名称">
                <el-input v-model="form.name"></el-input>
              </el-form-item>
              <el-form-item label="手机号码">
                <el-input v-model="form.tel"></el-input>
              </el-form-item>
              <el-form-item label="邮箱">
                <el-input v-model="form.email"></el-input>
              </el-form-item>
              <div class="radioBtn">
                <el-radio v-model="radio" label="1">男</el-radio>
                <el-radio v-model="radio" label="2">女</el-radio>
              </div>
              <el-form-item>
                <el-button type="primary" @click="onSubmit">立即创建</el-button>
                <el-button>取消</el-button>
              </el-form-item>
            </el-form>
          </el-tab-pane>
          <el-tab-pane label="修改密码">
            <el-form ref="form" :model="form" label-width="80px">
              <el-form-item label="旧密码">
                <el-input v-model="form.pastPass"></el-input>
              </el-form-item>
              <el-form-item label="新密码">
                <el-input v-model="form.nowPass"></el-input>
              </el-form-item>
              <el-form-item label="确认密码">
                <el-input v-model="form.confirmPass"></el-input>
              </el-form-item>
              <el-form-item>
                <!--<el-button type="primary" @click=""></el-button>-->
                <el-button :plain="true" @click="savePass">保存</el-button>
                <el-button>关闭</el-button>
              </el-form-item>
            </el-form>
          </el-tab-pane>
        </el-tabs>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: "cbPersonal",
  data() {
    return {
      form: {
        name: "",
        email: "",
        tel: "",
        pastPass: "",
        nowPass: "",
        confirmPass: ""
      },
      radio: "",
      userInfo: "",
      userId: "",
      userPass: "",
      loading: false
    };
  },
  methods: {
    initUser() {
      let user = JSON.parse(localStorage.getItem("user"));
      this.userInfo = user;
      this.userPass = user.userPass;
      this.userId = user.userId;
      this.form.name = user.userName;
      this.form.tel = user.tel;
      this.form.email = user.email;
      this.radio = user.sex == "男" ? "1" : "2";
    },
    onSubmit() {
      // console.log("submit!");
    },
    savePass() {
      if (this.userPass !== this.form.pastPass) {
        alert("原密码错误");
        return;
      }

      if (this.form.nowPass && this.form.confirmPass) {
        if (this.form.nowPass !== this.form.confirmPass) {
          alert("两次密码不一致");
          return;
        } else {
          this.loading = true;
          $.post(
            "http://localhost:3000/user/api/updateUser",
            {
              userId: this.userId,
              userPass: this.form.nowPass
            },
            (data, status, xhr) => {
              this.loading = false;
              if (data == 1) {
                this.$message("修改成功");
                this.initUser();
              } else {
                this.$message("修改失败");
              }
            },
            "json"
          );
        }
      }
    }
  },
  created() {
    this.initUser();
  }
};
</script>

<style lang="scss" scoped>
.personal {
  .title {
    padding: 13px;
    width: 100%;
    background: #d3dce6;
    position: absolute;
    left: 0;
    top: 0;
    box-sizing: border-box;
  }
  color: #000;
  .el-col,
  .el-col-6 {
    background: #fff;
    position: relative;
  }
  .perLeft {
    margin: 0 18px;
    border-radius: 5px;

    .headimg {
      max-width: 120px;
      height: 120px;
      margin-top: 45px;
      text-align: center;
      margin-bottom: 20px;
      margin: 60px auto 40px;
      img {
        display: block;
        width: 100%;
        max-height: 120px;
        border-radius: 50%;
      }
    }
    .infoList {
      padding-bottom: 30px;
      li {
        display: flex;
        justify-content: space-between;
        border: 1px solid #e7eaec;
        border-left: 0;
        border-right: 0;
        padding: 10px 0;
        .left {
          color: #000;
        }
      }
    }
  }
  .el-col-17 {
    height: 425px;
    padding-bottom: 20px;
    .radioBtn {
      width: 140px;
      margin: 0 auto;
    }
  }
}
</style>
