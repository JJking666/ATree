<!--
 * @Author: JJking666 1337802617@qq.com
 * @Date: 2023-05-02 15:37:07
 * @LastEditors: JJking666 1337802617@qq.com
 * @LastEditTime: 2023-05-09 22:31:11
 * @FilePath: \treedemo\src\components\ATree.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->

<template>
  <div class="tree">
    <div class="tree-content">
      <div class="tree-item" v-for="(item, index) in tree" :key="index">
        <div class="item-info" :style="isLeaf(item)">
          <el-icon
            @click="setFolder(index)"
            v-if="item.children && item.children.length > 0"
            ><CirclePlus v-if="item.status === 0" />
            <Remove v-else />
          </el-icon>
          <div
            class="icon-line"
            v-else
            :style="
              tree[index].id === props.firstNodeId
                ? checkFirstNode(tree, index)
                : isLastIconLine(tree, index)
            "
          ></div>
          <div class="middle-line" :style="isNeedMarginL(item)"></div>
          <el-icon
            style="margin: 0px"
            v-if="!item.children || item.children.length === 0"
          >
            <img class="diyIcon" :src="item.icon" v-if="item.icon" />
            <Document v-else />
          </el-icon>
          <el-icon style="margin: 0px" v-else-if="options.showIcon">
            <img class="diyIcon" :src="item.icon" v-if="item.icon" />
            <Folder v-else-if="item.status === 0" />
            <FolderOpened v-else />
          </el-icon>
          <span :style="item.fontCss" @click="item.toUrl && item.toUrl()"
            >{{ item.name }} {{ getStatus(item) }}</span
          >
        </div>
        <div class="item-son" :style="hasLine(tree, index)">
          <div class="connect-line" :style="hasConnectLine(item)"></div>
          <ATree
            v-if="item.children && item.status === 1"
            :Tree="item.children"
            :options="options"
          ></ATree>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, defineProps } from "vue";

enum Status {
  CLOSE,
  OPEN,
}
interface treeType {
  id: string;
  name: string;
  icon?: string;
  status: Status;
  fontCss?: unknown;
  toUrl: () => void | null;
  children?: Array<treeType> | null;
}
interface optionType {
  Tree: Array<treeType>;
  options: {
    showIcon: boolean;
    showLine: boolean;
  };
  firstNodeId?: string; // 解决第一层头个结点css问题
}

const props = defineProps<optionType>();

const tree = reactive(props.Tree);
const options = reactive(props.options);

function isShowLine() {
  return {
    borderColor: options.showLine ? "" : "transparent",
  };
}
function getStatus(item: treeType) {
  let status = item.status === 0 ? "-折叠" : "-展开";
  if (!item.children || item.children.length === 0) return "";
  return status;
}
function checkFirstNode(tree: treeType[], index: number) {
  let height = "";
  let alignSelf = "";
  if (tree[index].id === props.firstNodeId) {
    height = "50%";
    alignSelf = "end";
  }
  if (index === tree.length - 1) {
    height = "0%";
    alignSelf = "start";
  }

  return Object.assign(
    {
      height,
      alignSelf,
    },
    isShowLine()
  );
}
function isLastIconLine(tree: treeType[], index: number) {
  return Object.assign(
    {
      height: index === tree.length - 1 ? "60%" : "110%",
    },
    isShowLine()
  );
}
function isLeaf(item: treeType) {
  return {
    margin:
      item.children && item.children.length > 0
        ? "0 0 8px 0"
        : "-7px -5px 4px 15px",
  };
}
function isNeedMarginL(item: treeType) {
  return Object.assign(
    {
      marginLeft: item.children && item.children.length > 0 ? "3px" : "0px",
    },
    isShowLine()
  );
}
function hasConnectLine(item: treeType) {
  return Object.assign(
    {
      borderLeft:
        item.children && item.status === 1 ? "2px dotted #9a9898" : "0px",
    },
    isShowLine()
  );
}
function hasLine(tree: treeType[], index: number) {
  if (!tree || tree.length === 0) return { borderLeft: "0px" };
  return Object.assign(
    {
      borderLeft: index === tree.length - 1 ? "0px" : "2px dotted #9a9898",
    },
    isShowLine()
  );
}
function setFolder(index: number) {
  tree[index]["status"] = tree[index]["status"] === 0 ? 1 : 0;
}
</script>

<style lang="less" scoped>
@lineColor: rgb(154, 152, 152);
.tree {
  min-width: 300px;
  display: flex;
  .tree-content {
    display: flex;
    flex-direction: column;
    .tree-item {
      display: flex;
      flex-direction: column;
      line-height: 1em;
      margin-top: 10px;
      position: relative;
      .item-info {
        display: flex;
        margin-bottom: 8px;
        .icon-line {
          height: 110%;
          width: 2px;
          border-left: 2px dotted @lineColor;
        }
        .open-icon {
          display: flex;
        }
        .el-icon,
        span {
          cursor: pointer;
          margin-left: 8px;
          .diyIcon {
            width: 100%;
            height: 100%;
          }
        }
        span:nth-of-type(1) {
          margin: 0;
        }
        .middle-line {
          margin: 0 3px;
          width: 10px;
          height: 50%;
          border-bottom: 2px dotted @lineColor;
        }
      }
      .item-son {
        min-height: 10px;
        display: flex;
        flex-direction: column;
        margin-left: 15px;
        padding-left: 18px;
        text-align: left;
        border-left: 2px dotted @lineColor;
        position: relative;
        .connect-line {
          top: -5px;
          margin-left: 15px;
          height: 12px;
          width: 20px;
          border-left: 2px dotted @lineColor;
        }
      }
    }
  }
}
</style>
