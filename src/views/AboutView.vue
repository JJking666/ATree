<!--
 * @Author: JJking666 1337802617@qq.com
 * @Date: 2023-04-30 16:53:38
 * @LastEditors: JJking666 1337802617@qq.com
 * @LastEditTime: 2023-05-08 22:06:10
 * @FilePath: \treedemo\src\views\AboutView.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
  <div class="about">
    <h1>This is an zTree demo</h1>
    <div class="button-list">
      <el-button type="primary" @click="changeShowIcon">{{
        options.showIcon ? "隐藏图标" : "显示图标"
      }}</el-button>
      <el-button type="success" @click="changeShowLine">{{
        options.showLine ? "隐藏连接线" : "显示连接线"
      }}</el-button>
    </div>
    <div class="content">
      <ATree :Tree="tree" :options="options" :firstNodeId="tree[0].id"></ATree>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from "vue";
import ATree from "../components/ATree.vue";

let options = reactive({
  showIcon: true,
  showLine: true,
});

const tree = reactive([
  {
    id: 0,
    name: "父节点1",
    icon: require("../assets/niu.png"),
    status: 0,
    fontCss: {
      fontFamily: "fantasy",
      color: "red",
      textDecoration: "line-through",
    },
    toUrl: () => {
      console.log("ss");
      window.open("https://www.baidu.com", "_blank");
    },
    children: [
      {
        name: "子节点1",
        status: 0,
        icon: require("../assets/laohu.png"),
        fontCss: {
          fontFamily: "fantasy",
          color: "red",
          textDecoration: "line-through",
        },
        toUrl: () => {
          console.log("ss");
          window.open("https://www.baidu.com", "_blank");
        },
        children: [
          {
            id: 1,
            name: "子节点1",
            status: 0,
            fontCss: {
              fontFamily: "幼圆",
              color: "green",
              textDecoration: "cursive",
            },
            toUrl: () => {
              window.open("https://juejin.cn/", "_blank");
            },
          },
          {
            id: 1,
            name: "子节点2",
            status: 0,
            fontCss: {
              fontFamily: "幼圆",
              color: "green",
              textDecoration: "cursive",
            },
            toUrl: () => {
              window.open("https://juejin.cn/", "_blank");
            },
          },
        ],
      },
      {
        name: "子节点2",
        status: 0,
        icon: require("../assets/laohu.png"),
        fontCss: {
          fontFamily: "幼圆",
          color: "green",
          textDecoration: "cursive",
        },
        toUrl: () => {
          window.open("https://juejin.cn/", "_blank");
        },
        children: [
          {
            id: 1,
            name: "子节点1",
            status: 0,
            fontCss: {
              fontFamily: "幼圆",
              color: "green",
              textDecoration: "cursive",
            },
            toUrl: () => {
              window.open("https://juejin.cn/", "_blank");
            },
            children: [
              {
                id: 1,
                name: "子节点1",
                status: 0,
                fontCss: {
                  fontFamily: "fantasy",
                  color: "red",
                  textDecoration: "line-through",
                },
                toUrl: () => {
                  console.log("ss");
                  window.open("https://www.baidu.com", "_blank");
                },
              },
              {
                id: 1,
                name: "子节点2",
                status: 0,
                icon: require("../assets/laohu.png"),
                fontCss: {
                  fontFamily: "fantasy",
                  color: "red",
                  textDecoration: "line-through",
                },
                toUrl: () => {
                  console.log("ss");
                  window.open("https://www.baidu.com", "_blank");
                },
                children: [
                  {
                    id: 1,
                    name: "子节点1",
                    status: 0,
                    fontCss: {
                      fontFamily: "fantasy",
                      color: "red",
                      textDecoration: "line-through",
                    },
                    toUrl: () => {
                      console.log("ss");
                      window.open("https://www.baidu.com", "_blank");
                    },
                    children: [
                      {
                        id: 1,
                        name: "子节点1",
                        status: 0,
                        icon: require("../assets/pangxie.png"),
                        fontCss: {
                          fontFamily: "fantasy",
                          color: "red",
                          textDecoration: "line-through",
                        },
                        toUrl: () => {
                          console.log("ss");
                          window.open("https://www.baidu.com", "_blank");
                        },
                      },
                      {
                        id: 1,
                        name: "子节点2",
                        status: 0,
                        icon: require("../assets/pangxie.png"),
                        fontCss: {
                          fontFamily: "幼圆",
                          color: "green",
                          textDecoration: "cursive",
                        },
                        toUrl: () => {
                          window.open("https://juejin.cn/", "_blank");
                        },
                      },
                    ],
                  },
                  {
                    name: "子节点2",
                    status: 0,
                    children: [
                      {
                        id: 1,
                        name: "子节点1",
                        icon: require("../assets/ma.png"),
                        status: 0,
                        fontCss: {
                          fontFamily: "幼圆",
                          color: "green",
                          textDecoration: "cursive",
                        },
                        toUrl: () => {
                          window.open("https://juejin.cn/", "_blank");
                        },
                        children: [
                          { id: 1, name: "子节点1", status: 0 },
                          {
                            id: 1,
                            name: "子节点2",
                            status: 0,
                            fontCss: {
                              fontFamily: "fantasy",
                              color: "red",
                              textDecoration: "line-through",
                            },
                            toUrl: () => {
                              console.log("ss");
                              window.open("https://www.baidu.com", "_blank");
                            },
                          },
                        ],
                      },
                      {
                        id: 1,
                        name: "子节点2",
                        status: 0,
                        fontCss: {
                          fontFamily: "fantasy",
                          color: "red",
                          textDecoration: "line-through",
                        },
                        toUrl: () => {
                          console.log("ss");
                          window.open("https://www.baidu.com", "_blank");
                        },
                      },
                    ],
                  },
                ],
              },
            ],
          },
          {
            id: 1,
            name: "子节点2",
            status: 0,
            icon: require("../assets/niu.png"),
            fontCss: {
              fontFamily: "fantasy",
              color: "red",
              textDecoration: "line-through",
            },
            toUrl: () => {
              console.log("ss");
              window.open("https://www.baidu.com", "_blank");
            },
          },
        ],
      },
    ],
  },
  {
    id: 1,
    name: "父节点2",
    status: 0,
    icon: require("../assets/ma.png"),
    fontCss: {
      fontFamily: "fangsong",
      color: "blue",
      textDecoration: "overline",
    },
    toUrl: () => {
      window.open("https://juejin.cn/", "_blank");
    },
    children: [
      {
        id: 1,
        name: "子节点1",
        status: 0,
        icon: require("../assets/pangxie.png"),
        fontCss: {
          fontFamily: "fantasy",
          color: "red",
          textDecoration: "line-through",
        },
        toUrl: () => {
          console.log("ss");
          window.open("https://www.baidu.com", "_blank");
        },
      },
      {
        id: 1,
        name: "子节点2",
        status: 0,
        icon: require("../assets/pangxie.png"),
        fontCss: {
          fontFamily: "fantasy",
          color: "red",
          textDecoration: "line-through",
        },
        toUrl: () => {
          console.log("ss");
          window.open("https://www.baidu.com", "_blank");
        },
      },
    ],
  },
  {
    id: 2,
    name: "父节点3",
    status: 0,
    icon: require("../assets/mogu.png"),
    fontCss: {
      fontFamily: "幼圆",
      color: "green",
      textDecoration: "cursive",
    },
    toUrl: () => {
      window.open("https://juejin.cn/", "_blank");
    },
    children: [
      {
        id: 1,
        name: "子节点1",
        status: 0,
        icon: require("../assets/ma.png"),
        fontCss: {
          fontFamily: "fantasy",
          color: "red",
          textDecoration: "line-through",
        },
        toUrl: () => {
          console.log("ss");
          window.open("https://www.baidu.com", "_blank");
        },
      },
      {
        id: 1,
        name: "子节点2",
        status: 0,
        icon: require("../assets/laohu.png"),
        fontCss: {
          fontFamily: "幼圆",
          color: "green",
          textDecoration: "cursive",
        },
        toUrl: () => {
          window.open("https://juejin.cn/", "_blank");
        },
      },
    ],
  },
]);

function changeShowIcon() {
  options.showIcon = !options.showIcon;
  console.log("changeShowIcon", options);
}
function changeShowLine() {
  options.showLine = !options.showLine;
  console.log("changeShowLine", options);
}
</script>

<style lang="less" scoped>
.about {
  display: flex;
  width: 100vw;
  min-height: 120vh;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  .button-list {
    display: flex;
    justify-content: center;
    width: 300px;
    margin-bottom: 20px;
  }
  .content {
    width: fit-content;
    background-color: #dafff3;
    padding: 30px 15px;
  }
}
</style>
