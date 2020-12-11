<template>
  <div class="noticeBox">
    <img src="../assets/titleIcon.png" class="titleIcon">
    <div>
      <span class="noticeTip">最新公告</span>
      <el-link @click="drawer = true" type="info" style="margin-left: 66px;">
        更多
      </el-link>
    </div>
    <div class="newNotice">
      <span>标题</span>
      <div>内容</div>
    </div>

    <!--  更多公告-->
    <el-drawer
      title="公告"
      :visible.sync="drawer"
      size="50%">
      <div>
        <el-button @click="innerDrawer = true">打开里面的!</el-button>
        <el-pagination
          :page-size="20"
          :pager-count="11"
          layout="prev, pager, next"
          :total="1000">
        </el-pagination>
<!--        公告评论-->
        <el-drawer
          title="评论详情"
          :append-to-body="true"
          :before-close="handleClose"
          :visible.sync="innerDrawer">
          <p>_(:зゝ∠)_</p>
        </el-drawer>
      </div>
    </el-drawer>
  </div>
</template>

<script>
  export default {
    name: "notice",
    data() {
      return {
        drawer: false,
        innerDrawer: false,
      }
    },
    methods: {
    }
  }
</script>

<style scoped>

.titleIcon{
  top:0;
  left:0;
  width:200px;
  height:150px;
  margin-bottom: 20px;
}

.newNotice{
  margin-top: 28px;
  margin-right:120px;
}

</style>
