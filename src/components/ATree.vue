<!--
 * @Author: JJking666 1337802617@qq.com
 * @Date: 2023-05-02 15:37:07
 * @LastEditors: JJking666 1337802617@qq.com
 * @LastEditTime: 2023-05-27 13:00:59
 * @FilePath: \treedemo\src\components\ATree.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->

<template>
  <div class="tree">
    <div class="tree__content">
      <div class="tree__item" v-for="(item, index) in tree" :key="index">
        <div class="item__info" :style="isLeaf(item)">
          <el-icon
            @click="setFolder(index)"
            v-if="item.children && item.children.length > 0"
            ><CirclePlus v-if="item.status === 0" />
            <Remove v-else />
          </el-icon>
          <div
            class="tree__info__icon-line"
            v-else
            :style="judgeNodeStatus(tree, index)"
          ></div>
          <div
            class="tree__info__middle-line"
            :style="isNeedMarginL(item)"
          ></div>
          <el-icon
            style="margin: 0px"
            v-if="!item.children || item.children.length === 0"
          >
            <img
              class="tree__info__diy-icon"
              :src="item.icon"
              v-if="item.icon"
            />
            <Document v-else />
          </el-icon>
          <el-icon style="margin: 0px" v-else-if="options.showIcon">
            <img
              class="tree__info__diy-icon"
              :src="item.icon"
              v-if="item.icon"
            />
            <Folder v-else-if="item.status === 0" />
            <FolderOpened v-else />
          </el-icon>
          <span :style="item.fontCss" @click="item.toUrl && item.toUrl()"
            >{{ item.name }} {{ getStatus(item) }}</span
          >
        </div>
        <div class="tree__item__son" :style="hasLine(tree, index)">
          <div
            class="tree__item__connect-line"
            :style="hasConnectLine(item)"
          ></div>
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
// 文件目录状态 缩回/展开
enum Status {
  CLOSE,
  OPEN,
}
// 组件属性类型
interface treeType {
  id: string; // id
  name: string; // 名称
  icon?: string; // 图标
  status: Status; // 状态
  fontCss?: unknown; // 字体
  toUrl: () => void | null; // 点击跳转链接（或其他点击事件）
  children?: Array<treeType> | null; // 子节点
}
// 组件属性类型
interface optionType {
  Tree: Array<treeType>; // 数据源
  options: {
    // 是否显示图标，连接线
    showIcon: boolean;
    showLine: boolean;
  };
  firstNodeId?: string; // 解决第一层头个结点css问题
}

const props = defineProps<optionType>();

const tree = reactive(props.Tree);
const options = reactive(props.options);
// 判断节点的状态来修改css
function judgeNodeStatus(tree: treeType[], index: number) {
  return tree[index].id === props.firstNodeId
    ? checkFirstNode(tree, index) // 整个树中的第一个
    : isLastIconLine(tree, index); // 判断是否为当前节点列表最后一位
}

// 是否显示连接线
function isShowLine() {
  return {
    borderColor: options.showLine ? "" : "transparent",
  };
}
// 返回文件目录状态（折叠|展开）
function getStatus(item: treeType) {
  let status = item.status === 0 ? "-折叠" : "-展开";
  if (!item.children || item.children.length === 0) return "";
  return status;
}
// 根据节点在树中位置调整连接线css
function checkFirstNode(tree: treeType[], index: number) {
  let height = "";
  let alignSelf = "";
  //该结点是该树的第一个子节点调整连接线css
  height = "50%";
  alignSelf = "end";
  //若该节点也是树的最后一个子节点调整连接线css
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
// 若节点处于当前节点列表中最后一位调整css样式
function isLastIconLine(tree: treeType[], index: number) {
  return Object.assign(
    {
      height: index === tree.length - 1 ? "60%" : "110%",
    },
    isShowLine()
  );
}
// 若节点是叶子节点
function isLeaf(item: treeType) {
  return {
    margin:
      item.children && item.children.length > 0
        ? "0 0 8px 0"
        : "-7px -5px 4px 15px",
  };
}
// 若节点有子节点修改css样式
function isNeedMarginL(item: treeType) {
  return Object.assign(
    {
      marginLeft: item.children && item.children.length > 0 ? "3px" : "0px",
    },
    isShowLine()
  );
}
// 若节点有子节点且处于展开状态添加连接线
function hasConnectLine(item: treeType) {
  return Object.assign(
    {
      borderLeft:
        item.children && item.status === 1 ? "2px dotted #9a9898" : "0px",
    },
    isShowLine()
  );
}
// 当树不存在时隐藏连接线，否则当该节点处于树的最后一位时隐藏往下延伸的连接线
function hasLine(tree: treeType[], index: number) {
  if (!tree || tree.length === 0) return { borderLeft: "0px" };
  return Object.assign(
    {
      borderLeft: index === tree.length - 1 ? "0px" : "2px dotted #9a9898",
    },
    isShowLine()
  );
}
// 点击文件目录图标修改展开关闭状态
function setFolder(index: number) {
  tree[index]["status"] = tree[index]["status"] === 0 ? 1 : 0;
}
</script>

<style lang="less" scoped>
@lineColor: rgb(154, 152, 152);
.tree {
  min-width: 300px;
  display: flex;
  &__content {
    display: flex;
    flex-direction: column;
  }
  &__item {
    display: flex;
    flex-direction: column;
    line-height: 1em;
    margin-top: 10px;
    position: relative;
    &__son {
      min-height: 10px;
      display: flex;
      flex-direction: column;
      margin-left: 15px;
      padding-left: 18px;
      text-align: left;
      border-left: 2px dotted @lineColor;
      position: relative;
    }
    &__connect-line {
      top: -5px;
      margin-left: 15px;
      height: 12px;
      width: 20px;
      border-left: 2px dotted @lineColor;
    }
  }
  &__info {
    display: flex;
    margin-bottom: 8px;
    &__icon-line {
      height: 110%;
      width: 2px;
      border-left: 2px dotted @lineColor;
    }

    &__middle-line {
      margin: 0 3px;
      width: 10px;
      height: 50%;
      border-bottom: 2px dotted @lineColor;
    }
    &__diy-icon {
      width: 100%;
      height: 100%;
    }
    .el-icon,
    span {
      cursor: pointer;
      margin-left: 8px;
    }

    span:nth-of-type(1) {
      margin: 0;
    }
  }
}
</style>
