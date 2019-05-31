<template>
  <div class="myMap">
    <div id="bdMap"></div>
    <div id="r-result"><input type="text" id="suggestId" size="20" value="百度" style="width:150px;" /><button id="closed"></button></div>
    <div id="searchResultPanel" style="display: none;"></div>
    <div id="mapList"></div>
  </div>
</template>

<script>
import BMap from "BMap"; // 引入地图组件
export default {
  data() {
    return {};
  },
  mounted() {
    // 百度地图API功能
    function G(id) {
      return document.getElementById(id);
    }
    let map = new BMap.Map("bdMap"); // 创建地图实例
    map.centerAndZoom("西安", 13); // 显示城市西安,地图级别，级别越大，范围越大

    let ac = new BMap.Autocomplete({ input: "suggestId", location: map }); //建立一个自动完成的对象

    ac.addEventListener("onhighlight", function(e) {
      //鼠标放在下拉列表上的事件
      let str = "";
      let _value = e.fromitem.value;
      let value = "";
      if (e.fromitem.index > -1) {
        value =
          _value.province +
          _value.city +
          _value.district +
          _value.street +
          _value.business;
      }
      str =
        "FromItem<br />index = " + e.fromitem.index + "<br />value = " + value;
      value = "";
      if (e.toitem.index > -1) {
        _value = e.toitem.value;
        value =
          _value.province +
          _value.city +
          _value.district +
          _value.street +
          _value.business;
      }
      str +=
        "<br />ToItem<br />index = " +
        e.toitem.index +
        "<br />value = " +
        value;
      G("searchResultPanel").innerHTML = str;
    });
    let myValue;
    ac.addEventListener("onconfirm", function(e) {
      //鼠标点击下拉列表后的事件
      let _value = e.item.value;
      myValue =
        _value.province +
        _value.city +
        _value.district +
        _value.street +
        _value.business;
      G("searchResultPanel").innerHTML =
        "onconfirm<br />index = " + e.item.index + "<br />myValue = " + myValue;

      setPlace();
    });

    function setPlace() {
      map.clearOverlays(); //清除地图上所有覆盖物
      function myFun() {
        let pp = local.getResults().getPoi(0).point; //获取第一个智能搜索的结果
        map.centerAndZoom(pp, 18);
        map.addOverlay(new BMap.Marker(pp)); //添加标注
      }
      let local = new BMap.LocalSearch(map, {
        //智能搜索
        onSearchComplete: myFun
      });
      local.search(myValue);
    }

    map.enableScrollWheelZoom(); //启动鼠标滚轮缩放地图
    map.enableKeyboard(); //启动键盘操作地图
    map.enableInertialDragging(); // 开启惯性拖拽效果
  }
};
</script>

<style lang="less">
@import "../assets/base.less";
#bdMap {
  width: 100%;
  height: 100vh;
}
#r-result{
    position: absolute;
    left: 20px;
    top: 20px;
    background-color: #fff;
    box-shadow: 1px 2px 1px rgba(0,0,0,.15);
    button{
        display: block;
        width: 40px;
        height: 25px;
        background: url("@{images}close.png") no-repeat center center;
        background-size: 25px 25px;
        position: absolute;
        border-left: 1px solid #eee;
        right: 0px;
        top: 7.5px;
    }
    input{
        display: block;
        width: 350px !important;
        font-size: 1.4rem;
        line-height: 40px;
        text-indent: 1em;
    }
}
</style>
