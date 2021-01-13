<template>
  <el-container>
    <el-aside width="200px">
      <notice></notice>
    </el-aside>
    <el-container>
      <el-header>
        <!--        菜单导航-->
        <el-menu
          :default-active="activeIndex2"
          class="el-menu-demo"
          mode="horizontal"
          @select="handleSelect"
          background-color="#545c64"
          text-color="#fff"
          active-text-color="#ffd04b">
          <el-menu-item index="1">首页</el-menu-item>
          <el-submenu index="2">
            <template slot="title">社区公益</template>
            <el-menu-item index="2-1">社区共享</el-menu-item>
            <el-menu-item index="2-2">志愿服务</el-menu-item>
            <el-menu-item index="2-3">选项3</el-menu-item>
            <el-submenu index="2-4">
              <template slot="title">选项4</template>
              <el-menu-item index="2-4-1">选项1</el-menu-item>
              <el-menu-item index="2-4-2">选项2</el-menu-item>
              <el-menu-item index="2-4-3">选项3</el-menu-item>
            </el-submenu>
          </el-submenu>
          <el-menu-item index="3" ><a href="https://baike.baidu.com/item/%E6%B7%87%E5%9B%AD%E6%9D%91/6511342" target="_blank">社区详情</a></el-menu-item>
          <el-menu-item index="4">意见反馈</el-menu-item>
          <el-dropdown  class="headPosition">
          <span class="el-dropdown-link">
            <el-avatar icon="el-icon-user-solid"></el-avatar><i class="el-icon-arrow-down el-icon--right"></i>
          </span>
            <el-dropdown-menu slot="dropdown" v-if="!noUser">
              <el-dropdown-item @click.native="changePicHeader">修改头像</el-dropdown-item>
              <el-dropdown-item @click.native="changePassword">修改密码</el-dropdown-item>
              <el-dropdown-item>退出登录</el-dropdown-item>
            </el-dropdown-menu>
            <el-dropdown-menu slot="dropdown" v-if="noUser">
              <el-dropdown-item @click.native="login">立即登录</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </el-menu>
      </el-header>

      <el-main>
        <!--        轮播图-->
        <el-carousel :interval="4000" type="card" height="200px">
          <el-carousel-item v-for="item in 4" :key="item">
            <h3 class="medium">{{ item }}</h3>
          </el-carousel-item>
        </el-carousel>

      </el-main>
      <el-footer>Footer</el-footer>
    </el-container>
    <change-password ref="changePassword"></change-password>
    <change-pic-header ref="changePicHeader"></change-pic-header>
  </el-container>
</template>

<script>
import notice from '../components/notice'
import changePassword from './components/changePassword'
import changePicHeader from './components/changePicHeader'
export default {
  name: 'HelloWorld',
  components: {
    changePicHeader: changePicHeader,
    notice: notice,
    changePassword: changePassword
  },
  data () {
    return {
      noUser: false, //判断是否已经登录，为true时说明没有登录，为false时说明已经登录
      activeIndex: '1',
      activeIndex2: '1'
    }
  },
  methods: {
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
    },

    login() {
      this.$router.push('/Login');
    },

    changePassword(){
      this.$refs.changePassword.outerVisible = true;
      this.$refs.changePassword. resetForm('pwdList');
    },

    changePicHeader(){
      this.$refs.changePicHeader.outerVisible = true;
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .headPosition{
    position: absolute;
    right: 5px;
    top: 10px;
  }

  .el-header, .el-footer {
    background-color: #B3C0D1;
    color: #333;
    text-align: center;
    line-height: 60px;
    padding: 0;
    margin: 0;
  }

  .el-aside {
    background-color: #D3DCE6;
    color: #333;
    text-align: center;
    line-height: 200px;
    padding: 0;
    margin: 0;
  }

  .el-carousel__item h3 {
    color: #475669;
    font-size: 14px;
    opacity: 0.75;
    line-height: 200px;
    margin: 0;
  }

  .el-carousel__item:nth-child(2n) {
    background-color: #99a9bf;
  }

  .el-carousel__item:nth-child(2n+1) {
    background-color: #d3dce6;
  }
  .el-container{
    height: 100%;
  }

  .el-aside {
    line-height: 20px;
  }

  .el-footer{
    position: absolute;
    bottom: 0;
    right: 0;
  }

  .el-main{
    padding: 0;
  }

</style>
