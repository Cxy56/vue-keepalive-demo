<template>
  <div style="height:100%;">
    <drawer
      width="60%;"
      :show.sync="drawerVisibility"
      :show-mode="showModeValue"
      :placement="showPlacementValue"
      :drawer-style="{'background-color':'white', width: '50%'}">
      <div slot="drawer">
        <group :title="username" width="20px;">
        <div touchstart v-for='(item, index) in menuOption'  class="normalItem home" @click='clickItem(item)' :key='index'>{{item.name}}</div>
        </group>
      </div>
      <view-box ref="viewBox"  body-padding-bottom="20px">
        <x-header slot="header" 
          class='headerStyle'
           :title="title"
        >
            <span slot="overwrite-left" @click="drawerVisibility = !drawerVisibility">
              <x-icon type="navicon" size="35"  style="fill:#fff;position:relative;top:-8px;left:-3px;"></x-icon>
            </span>
        </x-header>
           <keep-alive>
              <router-view v-if="$route.meta.keepAlive" class="router-view">
              </router-view>
          </keep-alive>
         <router-view v-if='!$route.meta.keepAlive' class="router-view" ></router-view>
     </view-box>
     </drawer>
  </div>
</template>

<style lang="less" scoped>
body {
  background: rgba(245, 245, 249, 1);
  font-family: PingFangSC-Regular;
}
.vux-header .vux-header-title {
  height: 50px;
  font-size: 18px;
}

.normalItem {
  height: 34px;
  font-size: 17px;
  padding-top: 16px;
  padding-left: 20px;
  border-bottom: 1px solid #ccc;
  color: rgba(76, 87, 100, 1);
}
.active {
  background-color: #2eb897;
  color: white;
}
.home {
  color: #2eb897;
}
</style>

<script>
import { Group, Cell, Drawer, ViewBox, XHeader } from "vux";
export default {
  components: {
    Group,
    Cell,
    Drawer,
    ViewBox,
    XHeader
  },
  data() {
    return {
      username: "陈先生",
      showMenu: false,
      drawerVisibility: false,
      menuOption: [],
      showModeValue: "push",
      showPlacementValue: "left",
    };
  },
  mounted() {
    let menuArr = this.$router.options.routes.find(
      item => item.path === "/home"
    );
    this.menuOption = menuArr.children.filter(
      item => !item.hidden || item.hidden !== true
    );
  },
  computed: {
    title() {
      return this.$route.name;
    }
  },
  methods: {
    clickItem(item) {
      this.$router.push(item.path);
      this.drawerVisibility = false;
    }
  },
  watch: {
    $route(to, from) {
      let _this = this;
      if (from.meta.keepAlive) {
        this.global.saveScrollTop = this.$refs.viewBox.getScrollTop();
      }
      if (to.meta.isBack) {
        setTimeout(function() {
          _this.$refs.viewBox.scrollTo(_this.global.saveScrollTop);
        }, 0);
      }
    }
  }
};
</script>
