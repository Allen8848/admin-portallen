<template>
  <section class="yoy-header-container robotWidth " ref="scrollTop" style="flex:1;">
    <bread class="navBar"></bread>
    <router-view class="view yoy-main listItem"  :style="{width:widthOS}"></router-view><footer-bar></footer-bar>
  </section>
</template>
<script>
  import Bread from './Bread'
  import FooterBar from './Footer';

  import store from '../../store/index';


  export default {
    data() {
      return {
        widthOS: '100%',
        setInterval: "",
      }
    },
    components: {
      Bread,
      FooterBar,
    },
    computed: {},
    watch: {
      '$route'(to, from) {
        if (to && from)
          this.scrollTop()
      }


    },
    created() {
      const res = this.getOs()
      if (res === 'Firefox') {
        const WIDTH = this.getScrollbarWidth()
        this.widthOS = res === 'Firefox' ? `calc(100% - ${WIDTH}px)` : '100%'
      }
    },
    methods: {
      myResize() {
        let robotWidthH = $(".robotWidth").outerHeight(true);
        // console.log("all", robotWidthH);
        let navBarH = $(".navBar").outerHeight(true);
        // console.log("fen001", navBarH);
        let listItem = $(".listItem").outerHeight(true);
        // console.log("fen002", listItem);
        let sum = navBarH + listItem + 50;
        if (robotWidthH > sum || robotWidthH == sum) {
          $(".robotFoot").css({
            "position": "absolute",
            "left": "0",
            "bottom": "0px",
            "z-index": "9",


          })
        } else {
          $(".robotFoot").css({
            "position": "static",
            "left": "0",
            "bottom": "0px",
            "z-index": "9",

          })
        }

      },
      getOs() {
        var OsObject = "";
        if (navigator.userAgent.indexOf("MSIE") > 0) {
          return "MSIE";
        }
        if (OsObject = navigator.userAgent.indexOf("Firefox") > 0) {
          return "Firefox";
        }
        if (OsObject = navigator.userAgent.indexOf("Safari") > 0) {
          return "Safari";
        }
        if (OsObject = navigator.userAgent.indexOf("Camino") > 0) {
          return "Camino";
        }
        if (OsObject = navigator.userAgent.indexOf("Gecko/") > 0) {
          return "Gecko";
        }
      },
      getScrollbarWidth() {
        var odiv = document.createElement('div'),//创建一个div
          styles = {
            width: '100px',
            height: '100px',
            overflowY: 'scroll'//让他有滚动条
          }, i, scrollbarWidth;
        for (i in styles) odiv.style[i] = styles[i];
        document.body.appendChild(odiv);//把div添加到body中
        scrollbarWidth = odiv.offsetWidth - odiv.clientWidth;//相减
        odiv.remove();//移除创建的div
        return scrollbarWidth;//返回滚动条宽度
      },
      scrollTop() {
        this.$refs.scrollTop.offsetParent.scrollTop = 0
      },
    },
  }
</script>
<style scoped>
  .robotWidth {
    /*display:flex ;*/
    width: 100%;

  }

  .listItem {
    /*padding-bottom: 50px;*/
  }

  .view {
    /*padding-bottom: 20px;*/
  }
</style>
<style lang="scss">
  @import '../../style/index';

  $bread-background: #2a8ce7;
  $bread-height: 48px;
  $title-height: 65px;
  .align-middle {
    vertical-align: middle;
  }

  .line {
    width: 2px;
    height: 20px;
    background-color: $primary-color;
    margin-right: 6px;
  }

  .yoy-main {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    padding-left: 40px;
    padding-right: 40px;
    min-height: calc(100vh - 238px);
  }

  .line {
    width: 2px;
    height: 24px;
    line-height: 24px;
    background: $primary-color;
    margin-right: 6px;
  }

</style>
