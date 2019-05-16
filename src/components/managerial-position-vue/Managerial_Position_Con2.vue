<template>
  <div class="Ma_Po_Se_Con2" >
    <div class="Ma_Po_Se_Con2_Midd">
      <div class="Ma_Po_Se_Con2_Card">
        <div class="Ma_Po_Se_Con2_Card_Btn">
          <div class="Ma_Po_Se_Con2_Card_Btn_left">
            <el-row class="Ma_Po_Se_Con2_Card_Btn_left_lists">
              <el-button
                type="primary"
                icon="el-icon-plus"
                class="Ma_Po_Se_Con2_Card_Btn_left_lists_single"
              >新增</el-button>
              <el-button
                type="success"
                icon="el-icon-edit"
                class="Ma_Po_Se_Con2_Card_Btn_left_lists_single"
              >修改</el-button>
              <el-button
                type="warning"
                icon="el-icon-close"
                class="Ma_Po_Se_Con2_Card_Btn_left_lists_single"
              >删除</el-button>
              <el-button
                type="danger"
                icon="el-icon-download "
                class="Ma_Po_Se_Con2_Card_Btn_left_lists_single"
              >导出</el-button>
            </el-row>
          </div>
          <div class="Ma_Po_Se_Con2_Card_Btn_right">
            <el-button-group>
              <el-button
                icon="el-icon-search"
                class="Ma_Po_Se_Con2_Card_Btn_right_lists_single"
                @click="change"
              ></el-button>
              <el-button icon="el-icon-refresh" class="Ma_Po_Se_Con2_Card_Btn_right_lists_single"></el-button>
              <el-button
                icon="el-icon-tickets"
                class="Ma_Po_Se_Con2_Card_Btn_right_lists_single"
                @click="showdata"
              ></el-button>
              <el-button icon="el-icon-s-grid" class="Ma_Po_Se_Con2_Card_Btn_right_lists_single">
              </el-button>
            </el-button-group>
          </div>
        </div>
        <div class="Ma_Po_Se_Con2_Card_Table_lists">
          <div class="Ma_Po_Se_Con2_Card_Table" v-if="Ma_Po_Se_Con2_Card_Table" >
            <table class="Ma_Po_Se_Con2_Card_Table_Con" style="width:100%;">
              <tr class="Ma_Po_Se_Con2_Card_Table_Con_first_tr">
                <td>
                  <input type="checkbox" class="checkboxinput">
                </td>
                <td>岗位编号</td>
                <td>岗位编码</td>
                <td>岗位名称</td>
                <td>显示顺序</td>
                <td>状态</td>
                <td>创建时间</td>
                <td>操作</td>
              </tr>
              <!--循环数据-->
              <tr
                class="Ma_Po_Se_Con2_Card_Table_Con_first_tr Ma_Po_Se_Con2_Card_Table_Con_first_tr1" :index="index" v-for="(item,index) in data"
              >
                <td>
                  <el-checkbox></el-checkbox>
                </td>
                <td>{{item.serialnumber}}</td>
                <td>{{item.coding}}</td>
                <td>{{item.name}}</td>
                <td>{{item.order}}</td>
                <td>
                  <el-button
                    round
                    style="font-size:12px;width:36px; height:18px;display: flex;justify-content: center;
background: #1ab394;color:#fff;padding: 4px 15px;"
                    align="center"
                  >{{item.status}}</el-button>
                </td>
                <td>{{item.time}}</td>
                <td>
                  <el-row
                    style=";display: flex;justify-content: center; align-items: center;
align-items: center;"
                  >
                    <el-button
                      type="primary"
                      icon="el-icon-edit"
                      style="font-size:12px;width:48px; height:22px;display: flex;justify-content: center;
align-items: center;padding: 4px 15px;"
                    >{{item.dosomething1}}</el-button>
                    <el-button
                      type="danger"
                      icon="el-icon-close"
                      style="font-size:12px;width:48px; height:22px;display: flex;justify-content: center;
padding: 4px 15px;padding: 4px 15px;"  @click="open"
                    >{{item.dosomething2}}</el-button>
                  </el-row>
                  <div class="Ma_Po_Se_Con2_Card_Table_Con_first_trdialog" >
                    <div class="Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd">
                      <div class="Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd_top">
                        <div class="Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd_top_left">修改岗位</div>
                        <div class="Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd_top_right">
                          <i class="el-icon-minus"></i>
                          <i class="el-icon-copy-document" style="margin:0 8px;"></i>
                          <i class="el-icon-close"></i>
                        </div>
                      </div>
                      <div class="Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd_Cen">
                        <el-form ref="form" :model="form" label-width="80px">
                          <el-form-item label="岗位名称">
                            <el-input v-model="form.name" ></el-input>
                          </el-form-item>
                          <el-form-item label="岗位编码">
                            <el-input v-model="form.name"></el-input>
                          </el-form-item>
                          <el-form-item label="显示顺序">
                            <el-input v-model="form.name"></el-input>
                          </el-form-item>
                          <el-form-item label="岗位状态">
                            <el-radio-group v-model="form.resource">
                              <el-radio label="正常"></el-radio>
                              <el-radio label="停用"></el-radio>
                            </el-radio-group>
                          </el-form-item>
                          <el-form-item label="备注">
                            <el-input type="textarea" v-model="form.desc"></el-input>
                          </el-form-item>
                        </el-form>
                      </div>
                      <div class="Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd_Bot">
                        <el-button type="primary">确认</el-button>
                        <el-button >取消</el-button>
                      </div>
                    </div>
                  </div>
                </td>
              </tr>

            </table>
          </div>
          <div class="Ma_Po_Se_Con2_Card_Table2" v-if="Ma_Po_Se_Con2_Card_Table2">
            <table class="Ma_Po_Se_Con2_Card_Table2_Con1" style="padding-bottom: 8px;" v-for="item in  data ">
              <tr class="Ma_Po_Se_Con2_Card_Table2_Con1_tr">
                <td>
                  <el-checkbox></el-checkbox>
                </td>
              </tr>
              <tr class="Ma_Po_Se_Con2_Card_Table2_Con1_tr">
                <td>{{item.serialnumbername}}</td>
                <td>{{item.serialnumber}}</td>
              </tr>
              <tr class="Ma_Po_Se_Con2_Card_Table2_Con1_tr">
                <td>{{item.codingname}}</td>
                <td>{{item.coding}}</td>
              </tr>
              <tr class="Ma_Po_Se_Con2_Card_Table2_Con1_tr">
                <td>{{item.username}}</td>
                <td>{{item.name}}</td>
              </tr>
              <tr class="Ma_Po_Se_Con2_Card_Table2_Con1_tr">
                <td>{{item.statusname}}</td>
                <td>
                  <el-button
                    round
                    style="font-size:12px;width:36px; height:18px;display: flex;justify-content: center;
background: #1ab394;color:#fff; padding: 4px 15px;"
                  >{{item.status}}</el-button>
                </td>
              </tr>
              <tr class="Ma_Po_Se_Con2_Card_Table2_Con1_tr">
                <td>{{item.timename}}</td>
                <td>{{item.time}}</td>
              </tr>
              <tr class="Ma_Po_Se_Con2_Card_Table2_Con1_tr">
                <td>{{item.dosomethingname}}</td>
                <td>
                  <el-row style=";display: flex; align-items: center;
align-items: center; ">
                    <el-button
                      type="primary"
                      icon="el-icon-edit"
                      style="font-size:12px;width:48px; height:22px;display: flex;justify-content: center;
align-items: center; padding: 4px 15px;"

                    >{{item.dosomething1}}</el-button>
                    <el-button
                      type="danger"
                      icon="el-icon-close"
                      style="font-size:12px;width:48px; height:22px;display: flex;justify-content: center;
padding: 4px 15px;"
                      @click="open">{{item.dosomething2}}</el-button>
                  </el-row>
                  <div class="Ma_Po_Se_Con2_Card_Table_Con_first_trdialog">
                    <div class="Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd">
                      <div class="Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd_top">
                        <div class="Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd_top_left">修改岗位</div>
                        <div class="Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd_top_right">
                          <i class="el-icon-minus"></i>
                          <i class="el-icon-copy-document" style="margin:0 8px;"></i>
                          <i class="el-icon-close"></i>
                        </div>
                      </div>
                      <div class="Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd_Cen">
                        <el-form ref="form" :model="form" label-width="80px">
                          <el-form-item label="岗位名称">
                            <el-input v-model="form.name"></el-input>
                          </el-form-item>
                          <el-form-item label="岗位编码">
                            <el-input v-model="form.name"></el-input>
                          </el-form-item>
                          <el-form-item label="显示顺序">
                            <el-input v-model="form.name"></el-input>
                          </el-form-item>
                          <el-form-item label="岗位状态">
                            <el-radio-group v-model="form.resource">
                              <el-radio label="正常"></el-radio>
                              <el-radio label="停用"></el-radio>
                            </el-radio-group>
                          </el-form-item>
                          <el-form-item label="备注">
                            <el-input type="textarea" v-model="form.desc"></el-input>
                          </el-form-item>
                        </el-form>
                      </div>
                      <div class="Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd_Bot">
                        <el-button type="primary">确认</el-button>
                        <el-button>取消</el-button>
                      </div>
                    </div>
                  </div>
                </td>
              </tr>
            </table>
          </div>
        </div>
        <div class="Ma_Po_Se_Con2_Card_Sum">
          <p class="Ma_Po_Se_Con2_Card_Text">第 1 到 4 条，共 4 条记录。</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Managerial_Position_Con2",
  props:["data"],
  data() {
    return {
      isShow: true,
      form: {
        name: "1",
        region: "",
        date1: "",
        date2: "",
        delivery: false,
        type: [],
        resource: "",
        desc: ""
      },
      multipleSelection: [],
      Ma_Po_Se_Con2_Card_Table: true,
      Ma_Po_Se_Con2_Card_Table2: false,
      Ma_Po_Se_Con2_Card_Table_Con_first_trdialog:false,
      id:"",

    };
  },
  
  methods: {
    onSubmit() {
      console.log("submit!");
    },

    showdata() {
      this.Ma_Po_Se_Con2_Card_Table = !this.Ma_Po_Se_Con2_Card_Table;
      this.Ma_Po_Se_Con2_Card_Table2 = !this.Ma_Po_Se_Con2_Card_Table2;

    },
    handleSelectionChange(val) {
      this.multipleSelection = val;
    },
    change() {
      this.$emit("change");
    },
/**
 * 点击编辑按钮让弹框显示onchangeshow（）
 *
 * **/





    /**点击删除按钮让弹框显示
     *
     *
     */

      open() {
        this.$alert(`<strong>
                        <div class="questionbox" style=" font-size:14px ;
      color:#676a6c;display: flex;align-items: center; ">
                          <span class="el-icon-question" style=" font-size:32px ;
    color:#3498db;margin-right: 10px;"></span>
                          确定删除这条信息吗？
                        </div>

                    </strong>`, '提示系统', {
          dangerouslyUseHTMLString: true
        });
      },
    },


};
</script>

<style scoped>
.Ma_Po_Se_Con2 {
  width: 100%;
  margin-top: 10px;
  box-sizing: border-box;
  background-clip: content-box;
}
.Ma_Po_Se_Con2_Midd {
  width: 100%;
  height: 100%;
  background: #ffffff;
  border-radius: 6px;
  box-shadow: 2px 1px 3px 0.5px #e1e1e2;
  border: 1px solid #ececed;
  box-sizing: border-box;
}
.Ma_Po_Se_Con2_Card {
  width: 100%;
  height: 100%;
  padding-top: 15px;
  padding-left: 14px;
  padding-right: 14px;
  box-sizing: border-box;
}
.Ma_Po_Se_Con2_Card_Btn {
  width: 100%;
  display: flex;
  padding-bottom: 10px;
}
.Ma_Po_Se_Con2_Card_Btn_left {
  width: 100%;
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.Ma_Po_Se_Con2_Card_Btn_right {
  width: 100%;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
.Ma_Po_Se_Con2_Card_Btn_left_lists {
  display: flex;
}
.Ma_Po_Se_Con2_Card_Btn_left_lists_single {
  width: 58px;
  height: 30px;
  font-size: 12px;
  display: flex;
  justify-content: center;
}
el-icon-caret-bottom {
  margin: 0;
  padding: 0;
}
.Ma_Po_Se_Con2_Card_Btn_right_lists_single {
  display: flex;
  align-items: center;
  height: 30px;
  font-size: 16px;
  color: #676a6c;
  border: 1px solid #c2c2c2;
}
.Ma_Po_Se_Con2_Card_Btn_right_lists_single:hover {
  background: #d4d4d4;
  color: #fff;
}
.Ma_Po_Se_Con2_Card_Table_lists {
  width: 100%;
}
.Ma_Po_Se_Con2_Card_Table {
  width: 100%;
  box-sizing: border-box;
}
.Ma_Po_Se_Con2_Card_Sum {
  width: 100%;
  padding-top: 15px;
  padding-bottom: 50px;
}
.Ma_Po_Se_Con2_Card_Text {
  font-size: 14px;
  color: #676a6c;
}
.Ma_Po_Se_Con2_Card_Table_Con tr:nth-child(1) {
  background: #eff3f8;
}
.Ma_Po_Se_Con2_Card_Table_Con tr td {
  font-size: 13px;
  color: #676a6c;
  border-bottom: 1px solid #e7eaec;
  padding: 14px 0;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_tr {
  width: 100%;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_tr td:nth-child(1) {
  width: 3.5%;
  padding-left: 8px;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_tr td:nth-child(2) {
  width: 10%;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_tr td:nth-child(3) {
  width: 14%;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_tr td:nth-child(4) {
  width: 14%;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_tr td:nth-child(5) {
  width: 15%;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_tr td:nth-child(6) {
  width: 7%;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_tr td:nth-child(7) {
  width: 15%;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_tr td:nth-child(8) {
  width: 20%;
  text-align: center;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_trdialog {
display: none;
  position: absolute;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  background: rgba(0, 0, 0, 0.4);
  z-index: 30;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd {
  position: absolute;
  left: 15%;
  top: 5%;
  width: 800px;
  height: 434px;
  background: #fff;
  z-index: 40;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd_top {
  width: 100%;
  display: flex;
  background: #f8f8f8;
  border-bottom: 2px solid #eeeeee;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd_top_left {
  width: 100%;
  display: flex;
  justify-content: flex-start;
  font-size: 13px;
  color: #333333;
  line-height: 43px;
  padding-left: 20px;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd_top_right {
  width: 100%;
  display: flex;
  justify-content: flex-end;
  font-size: 13px;
  align-items: center;
  color: #2e2d3c;
  padding-right: 20px;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_tr1:hover {
  background: #f5f5f5;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd_Cen {
  width: 100%;
  padding: 30px 130px 30px 57px;
  box-sizing: border-box;
  animation: leftcon 2s 1;
}
@keyframes leftcon {
  0% {
    transform: translateX(50px);
  }
  20% {
    transition-timing-function: linear;
  }
  100% {
    transform: translateX(0);
  }
}
el-button--small {
  padding: 4px 15px;
}
.Ma_Po_Se_Con2_Card_Table_Con_first_trdialog_Midd_Bot {
  display: flex;
  height: 58px;
  justify-content: flex-end;
  padding-right: 20px;
  align-items: center;
  width: 100%;
  border-top: 2px solid #eeeeee;
  background: #f0f4f7;
  box-sizing: border-box;
}
.Ma_Po_Se_Con2_Card_Table2_Con1 {
  width: 100%;
  padding-left: 8px;
  padding-top: 8px;
  padding-bottom: 8px;
  border-collapse: separate;
  border-bottom: 1px solid #e7eaec;
}
.checkboxinput {
  margin-right: 4px;
  position: relative;
  vertical-align: middle;
}
.checkboxinput::after {
  position: absolute;
  width: 14px;
  height:14px;
  top: 0;
  background-color: #dedede;
  content: " ";
  color: #fff;
  display: inline-block;
  visibility: visible;
  border-radius: 3px;
  border: 1px solid #f1f1f1;
}
.checkboxinput:checked::after {
  content: "√";
  width: 14px;
  height: 14px;
  font-size: 14px;
  color: #ffffff;
  text-align: center;
  line-height: 14px;
  background-color:#dedede;
}
.Ma_Po_Se_Con2_Card_Table2_Con1 tr:last-child {
  width: 100%;
  height: 24px;
  padding-bottom: 8px;
}
.Ma_Po_Se_Con2_Card_Table2_Con1:hover {
  background: #f5f5f5;
}
.Ma_Po_Se_Con2_Card_Table2_Con1_tr td {
  font-size: 14px;
  color: #676a6c;
  line-height: 22px;
}
.Ma_Po_Se_Con2_Card_Table2_Con1_tr td:nth-child(1) {
  font-weight: 900;
  width: 29%;
}
.Ma_Po_Se_Con2_Card_Table2_Con1_tr td:nth-child(2) {
  width: 71%;
}
.questionbox span{
  font-size:32px ;
  color:#3498db;
}
  .questionbox{
    font-size:14px ;
    color:#676a6c;
  }
</style>
