<template>
  <div class="tableBox">
    <table class="tab">
      <thead>
        <tr>
          <td>
            <input type="checkBox" class="checkBtn">
          </td>
          <td>编号</td>
          <td>姓名</td>
          <td>电话</td>
          <td>邮箱</td>
          <td>现居地</td>
          <td>渠道</td>
          <td>任职类型</td>
          <td>面试</td>
          <td>面试人</td>
          <td>意向情况</td>
          <td>操作</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for=" (item,index) in p" :key="item.reId">
          <td>
            <input type="checkBox" class="checkBtn" :checked="item.isChecked">
          </td>
          <td>{{ item.reId }}</td>
          <td>{{ item.reName }}</td>
          <td>{{ item.rePhone }}</td>
          <td>{{ item.reEmail }}</td>
          <td>{{ item.reAddress }}</td>
          <td>{{ item.reDitch }}</td>
          <td>{{ item.reType }}</td>
          <td>{{ item.reInter}}</td>
          <td>{{ item.rePerson }}</td>
          <td>{{ item.case }}</td>
          <td>
            <el-button type="primary" icon="el-icon-edit-outline" size="mini" @click="open(index,item.reId)">编辑</el-button>
          </td>
        </tr>
      </tbody>
    </table>
    <!--分页-->
    <div class="block">
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page.sync="currentPage"
        :page-size="pageSize"
        layout="prev, pager, next, jumper"
        :total="dataCount"
      ></el-pagination>
    </div>
  </div>
</template>

<script>
export default {
  name: "cbRecruitTable",
  props:["p"],
  data() {
    return {
      currentPage: 1,
      dataCount: 0,
      pageSize: 5
    };
  },
  methods: {
    handleSizeChange(val) {
      // console.log(`每页 ${val} 条`);
    },
    handleCurrentChange(val) {
      // console.log(`当前页: ${val}`);
    },
    open(index,id) {
      let _this = this
      this.$prompt("意向情况", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消"
      }).then(({ value }) => {
        console.log(id)
          $.post('http://10.35.164.14:3000/reperson/api/setReperson',{reId:id,case:value},
            (data)=>{
            console.log(data)
              if(data == 1){
                this.$message({
                  type: "success",
                  message: "本次面试: " + value
                });
                _this.p[index].case = value;
              }else if(data == 0){
                this.$message({
                  message:"修改失败，请重新修改！"
                })
              }
           })
         })
        .catch(() => {
          this.$message({
            type: "info",
            message: "取消输入"
          });
        });
    }
  },
  created() {
    // console.log("candidates", this.p);
  }
};
</script>

<style scoped>
.tableBox {
  width: calc(100% - 30px);
  height: calc(100% - 38px);
  padding: 15px;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.2);
}
.tab {
  width: 100%;
  height: 300px;
  text-align: center;
  border-collapse: collapse;
  overflow-x: scroll;
}
.tab tbody {
  display: block;
  height: 200px;
  overflow-y: scroll;
}
.tab thead,
tbody tr {
  display: table;
  width: 100%;
  table-layout: fixed;
}
.tab thead {
  background-color: #f5f5f5;
  color: #141414;
  width: calc(100% - 16px);
}
.tab tr {
  border-bottom: 1px solid #e4eeeb;
  height: 40px;
  color: #323232;
}
.checkBtn {
  width: 15px;
  height: 15px;
  background: #fff;
  cursor: pointer;
}
.tab tr td:nth-child(1) {
  width: 25px;
}
.tab tr td:nth-child(2) {
  width: 35px;
}
.tab tr td:nth-child(4) {
  width: 100px;
}
.tab tr td:nth-child(5) {
  width: 150px;
}
.tab tr td:nth-child(12) {
  width: 100px;
}
</style>
