<template>
  <div id="app">
    <div id="header">
      <Header/>
    </div>
    <div id="content">
      <div class="leftNav">
        <LeftNav/>
      </div>
      <div class="rightContent">
        <router-view/>
      </div>
    </div>
    <div id="footer">
      <Footer/>
    </div>
  </div>
</template>

<script>
import Header from "@/components/common/Header";
import Footer from '@/components/common/Footer';
import LeftNav from "@/components/pages/LeftNav";
export default {
  name: "App",
  data() {
    return {};
  },
  components: {
    Header,
    LeftNav,
    Footer
  }
};
</script>

<style lang="less">
    @import "assets/base.less";
    #content{
        width: 100%;
        height: 100vh;
        position: relative;
        .leftNav{
            width: 260px;
            height: 100%;
            background-color: @bgcolor1;
        }
        .rightContent{
            width: calc(~"100% - 260px");
            position: absolute;
            left: 260px;
            top: 0; 
            height: 100%;
        }
    }
</style>
