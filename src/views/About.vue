<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div id="header"></div>
    <div id="text">
      <div class="yuan">
        <div class="bg"></div>
      </div>
    </div>

    <!-- 轮播图 -->
    <div>
      <el-carousel height="300px" type="card">
        <!-- 
          type="card" 卡片化
          arrow="always" 左右箭头的显示时机 默认hover显示，always一直显示，never一直隐藏
          indicator-position="outside" 下方指示点的位置，默认在里面，outside在外面，none不会显示 
          trigger="click" 与指示点的交互，默认hover，click点击
          direction="vertical" 轮播图滑动方向，默认horizontal水平方向，vertical垂直方向
          loop="true" 是否循环，默认是
          autoplay="true"  自动切换，默认是
          initial-index=0  幻灯片的初始索引，默认0
        -->
        <el-carousel-item v-for="item in swiperDatas" :key="item.id">
          <img :src="item.src" alt="" />
        </el-carousel-item>
      </el-carousel>
    </div>

    <!-- 折叠面板，手风琴效果 -->
    <div>
      <!-- 通过 accordion 属性来设置是否以手风琴模式显示，只能有一个展开 -->
      <el-collapse v-model="activeNames" accordion>
        <el-collapse-item title="一致性 Consistency" name="1">
          <div>与现实生活一致：与现实生活的流程、逻辑保持一致，遵循用户习惯的语言和概念；</div>
          <div>在界面中一致：所有的元素和结构需保持一致，比如：设计样式、图标和文本、元素的位置等。</div>
        </el-collapse-item>
        <el-collapse-item title="反馈 Feedback" name="2">
          <div>控制反馈：通过界面样式和交互动效让用户可以清晰的感知自己的操作；</div>
          <div>页面反馈：操作后，通过页面元素的变化清晰地展现当前状态。</div>
        </el-collapse-item>
        <el-collapse-item name="3">
          <template slot="title">
          效率 Efficiency<i class="header-icon el-icon-info"></i>
          </template>
          <div>简化流程：设计简洁直观的操作流程；</div>
          <div>清晰明确：语言表达清晰且表意明确，让用户快速理解进而作出决策；</div>
          <div>帮助用户识别：界面简单直白，让用户快速识别而非回忆，减少用户记忆负担。</div>
        </el-collapse-item>
      </el-collapse>
    </div>

    <!-- 抽屉 -->
    <div>
      <el-radio-group v-model="direction">
        <el-radio label="ltr">从左往右开</el-radio>
        <el-radio label="rtl">从右往左开</el-radio>
        <el-radio label="ttb">从上往下开</el-radio>
        <el-radio label="btt">从下往上开</el-radio>
      </el-radio-group>

      <el-button @click="drawer = true" type="primary" style="margin-left: 16px;">
        点我打开
      </el-button>

      <!-- :with-header="false"隐藏标题 -->
      <el-drawer
        title="我是标题"
        :visible.sync="drawer"
        :with-header="false"  
        :direction="direction"
        :before-close="handleClose"
        size="50%">
        <span>我来啦!</span>
        <div>
        <el-button @click="innerDrawer = true">打开里面的!</el-button>
        <el-drawer
          title="我是里面的"
          :append-to-body="true"
          :direction="direction"
          :before-close="handleClose"
          :visible.sync="innerDrawer"
          size="20%">
          <p>_(:зゝ∠)_</p>
        </el-drawer>
        </div>
      </el-drawer>
    </div>

    <!-- 导航 -->
    <div>
      <!-- 垂直导航 -->
      <el-menu
      class="el-menu-vertical-demo"
      background-color="#545c64"
      text-color="#fff"
      active-text-color="#ffd04b">
      <!-- 一级标题 -->
      <el-submenu index="1">
        <template slot="title">电影</template>
        <el-menu-item index="1-1">喜剧</el-menu-item>
        <el-submenu index="1-2">
          <template slot="title">动作</template>
          <el-menu-item index="1-2-1">选项1</el-menu-item>
        </el-submenu>
      </el-submenu>
      <!-- 一级标题 -->
      <el-submenu index="2">
        <span slot="title">小说</span>
        <el-submenu index="2-1">
          <span slot="title">小说1</span>
            <el-submenu index="2-1-1">
              <span slot="title">小说11</span>
              <el-menu-item index="2-1-1-1">小说111</el-menu-item>
            </el-submenu>
        </el-submenu>
      </el-submenu>
      <!-- 一级标题 -->
      <el-menu-item index="3" disabled>
        <span slot="title">音乐</span>
      </el-menu-item>
    </el-menu>
      <!-- 关于菜单导航 用<el-menu>标签
      1.如果一级菜单下面没有二级菜单，用<el-menu-item>,有二级导航用<el-submenu>
      2.垂直侧边导航建议只有两层，多层有bug,水平顶部导航可以有多层 -->

    <!-- 水平导航 -->
    <el-menu
      class="el-menu-horizontal-demo"
      background-color="#545c64"
      text-color="#fff"
      mode="horizontal"
      active-text-color="#ffd04b">
      <!-- 一级标题 -->
      <el-submenu index="1">
        <template slot="title">电影</template>
        <el-menu-item index="1-1">喜剧</el-menu-item>
        <el-submenu index="1-2">
          <template slot="title">动作</template>
          <el-menu-item index="1-2-1">动作1</el-menu-item>
          <el-menu-item index="1-2-2">动作2</el-menu-item>
          <el-menu-item index="1-2-3">动作3</el-menu-item>
          <el-menu-item index="1-2-4">动作4</el-menu-item>
          <el-menu-item index="1-2-5">动作5</el-menu-item>
          <el-menu-item index="1-2-6">动作6</el-menu-item>
          <el-submenu index="1-2-7">
            <template slot="title">动作7</template>
            <el-menu-item index="1-2-7-1">动作111</el-menu-item>
          </el-submenu>
        </el-submenu>
        <el-menu-item index="1-3">武打</el-menu-item>
        <el-menu-item index="1-4">科幻</el-menu-item>
        <el-menu-item index="1-5">古装</el-menu-item>
        <el-menu-item index="1-6">爱情</el-menu-item>
        <el-menu-item index="1-7">玄幻</el-menu-item>
      </el-submenu>
      <!-- 一级标题 -->
      <el-submenu index="2">
        <span slot="title">小说</span>
        <el-submenu index="2-1">
          <span slot="title">小说1</span>
            <el-submenu index="2-1-1">
              <span slot="title">小说11</span>
                <el-submenu index="2-1-1-1">
                  <span slot="title">小说111</span>
                    <el-submenu index="2-1-1-1-1">
                      <span slot="title">小说1111</span>
                      <el-menu-item index="2-1-1-1-1-1">小说11111</el-menu-item>
                    </el-submenu>
                </el-submenu>
            </el-submenu>
        </el-submenu>
      </el-submenu>
      <!-- 一级标题 -->
      <el-menu-item index="3" disabled>
        <span slot="title">音乐</span>
      </el-menu-item>
    </el-menu>
    </div>


    <div>
      <el-radio-group v-model="tabPosition" style="margin-bottom: 30px;">
        <el-radio-button label="top">top</el-radio-button>
        <el-radio-button label="right">right</el-radio-button>
        <el-radio-button label="bottom">bottom</el-radio-button>
        <el-radio-button label="left">left</el-radio-button>
      </el-radio-group>

        <!-- tab-position动态切换加:号，固定方向的话不加:号 -->
      <el-tabs :tab-position="tabPosition" style="height: 200px;">
        <el-tab-pane label="用户管理">用户管理</el-tab-pane>
        <el-tab-pane label="配置管理">配置管理</el-tab-pane>
        <el-tab-pane label="角色管理">角色管理</el-tab-pane>
        <el-tab-pane label="定时任务补偿">定时任务补偿</el-tab-pane>
      </el-tabs>
        </div>
        <div style="width:100%;height:500px"></div>
      </div>
</template>


<script>
//这里可以导入其他文件（比如：组件，工具js，第三方插件js，json文件，图片文件等等）
//例如：import 《组件名称》 from '《组件路径》';

export default {
//import引入的组件需要注入到对象中才能使用
components: {},
data() {
//这里存放数据
return {
  swiperDatas:[{
    id:1,
    src: require('@/assets/images/swiper1.jpg')
  },{
    id:2,
    src: require('@/assets/images/swiper2.jpg')
  },{
    id:3,
    src: require('@/assets/images/swiper3.jpg')
  },{
    id:4,
    src: require('@/assets/images/swiper4.jpg')
  },{
    id:5,
    src: require('@/assets/images/swiper5.jpg')
  }],
  activeNames: ['1'],
  drawer: false,
  innerDrawer: false,
  direction: 'rtl',
  tabPosition: 'left'
};
},
//监听属性 类似于data概念
computed: {},
//监控data中的数据变化
watch: {},
//方法集合
methods: {
  handleClose(done) {
    this.$confirm('确认关闭？').then(() => {
            done();
          }).catch(()=> {});
  }
},
beforeCreate() {}, //生命周期 - 创建之前
//生命周期 - 创建完成（可以访问当前this实例）
created() {

},
beforeMount() {}, //生命周期 - 挂载之前
//生命周期 - 挂载完成（可以访问DOM元素）
mounted() {

},
beforeUpdate() {}, //生命周期 - 更新之前
updated() {}, //生命周期 - 更新之后
beforeDestroy() {}, //生命周期 - 销毁之前
destroyed() {}, //生命周期 - 销毁完成
activated() {}, //如果页面有keep-alive缓存功能，这个函数会触发
}
</script>

<style lang="less">
#header{
  width: 500px;
  height: 120px;
  margin: 0 auto;
  background: linear-gradient(to right,#05C63A,#04B434);
}
  
#text{
  width: 500px;
  height: 100px;
  overflow: hidden;
  position: relative;
  margin: 0 auto;
  .yuan{
    width: 1300px;
    height: 1300px;
    position: absolute;
    bottom: 50px;
    left: 50%;
    margin-left: -650px;
    border-radius: 50%;
    overflow: hidden;
    .bg{
      width: 500px;
      height: 100px;
      background: linear-gradient(to right,#05C63A,#04B434);
      position: absolute;
      bottom: -50px;
      left: 50%;
      margin-left: -250px;
    }
  }
}
.el-menu-vertical-demo:not(.el-menu--collapse) {
    width: 200px;
    min-height: 400px;
  }
</style>