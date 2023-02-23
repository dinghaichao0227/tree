<template>
  <div class="header">
    <!--  用组件库的 -->
    <div class="header-left">
      <h2>element-plus</h2>
      <div>
        <el-tree :data="list" :props="defaultProps" @node-click="handleNodeClick" />
      </div>
    </div>
    <!-- 没有用组件 -->
    <div class="header-right">
      <h2>原生</h2>
      <div v-for="(item, index) in list" :key="index">
        <div class="text" @click="onOption">{{ item.name }} +</div>
        <div v-if="one === true" class="text father">
          {{ item.children[0].name }}
        </div>
        <div v-if="one === true" class="text Mother" @click="onMother">
          {{ item.children[1].name }} +
        </div>
        <div v-if="two === true && one === true" class="text sister">
          {{ item.children[1].children[0].name }}
        </div>
        <div v-if="two === true && one === true" class="text brother" @click="onBrother">
          {{ item.children[1].children[1].name }} +
        </div>
        <div v-if="three === true && two === true && one === true" class="text zhang1">
          {{ item.children[1].children[1].children[0].name }}
        </div>
        <div v-if="three === true && two === true && one === true" class="text zhang2">
          {{ item.children[1].children[1].children[1].name }}
        </div>
        <div v-if="two === true && one === true" class="text me">
          {{ item.children[1].children[2].name }}
        </div>
        <div v-if="two === true && one === true" class="text obj" @click="onObj">
          {{ item.children[1].children[3].name }}+
        </div>
        <div v-if="four === true && two === true && one === true" class="text ding1">
          {{ item.children[1].children[3].children[0].name }}
        </div>
        <div v-if="four === true && two === true && one === true" class="text ding2">
          {{ item.children[1].children[3].children[1].name }}
        </div>
      </div>
      <h6>注释：很丑，带有加号的可以展开，不带加号的没有子元素</h6>
    </div>
  </div>
</template>

<script setup>
import { onMounted, reactive, ref } from "vue";
import json from "../config/json.json";

let one = ref(false);
let two = ref(false);
let three = ref(false);
let four = ref(false);
let list = reactive([]);
const defaultProps = {
  children: "children",
  label: "name",
};
const onOption = () => {
  one.value = !one.value;
  // console.log(one, 1);
};
const onMother = () => {
  two.value = !two.value;
};
const onBrother = () => {
  three.value = !three.value;
};
const onObj = () => {
  four.value = !four.value;
};
const fn = () => {
  let map = {};
  // let result = [];
  json.forEach((el) => {
    map[el.id] = el;
  });

  json.forEach((item) => {
    const father = map[item.pid];
    if (father) {
      (father.children || (father.children = [])).push(item);
    } else {
      list.push(item);
      // console.log(list, 999);
    }
  });
};
const handleNodeClick = () => {
  console.log(34);
};

onMounted(() => {
  fn();
  list.map((item) => {
    console.log(item.name);
  });
});
</script>

<style lang="scss" scoped></style>
