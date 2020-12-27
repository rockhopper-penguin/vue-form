<template>
  <div class="hello">
    <div class="block">
      <p>Array</p>
      <div v-for="index in forms" :key="index">
        <input type="text" v-model="array[index - 1]" @change="onChange" />
        <span v-if="index == 1">
          <button @click="addForms">+</button>
        </span>
        <span v-else>
          <button @click="removeForms(index - 1)">-</button>
        </span>
      </div>
    </div>
    <div class="block">
      <p>JSON</p>
      <p>{{ toJson }}</p>
    </div>
    <div class="block">
      <p>JSON to array</p>
      <div v-for="index in toArray" :key="index">
        <input type="text" :value="index" @change="onChange" />
      </div>
    </div>
  </div>
</template>

<style>
.hello {
  width: 100%;
}
.block {
  width: 80%;
  margin: auto;
  border: solid 1px black;
  padding: 10px;
}
</style>

<script lang="ts">
import { Component, Prop, Vue, Watch } from "vue-property-decorator";

@Component
export default class HelloWorld extends Vue {
  penguin = "Rockhopper-Penguin";

  // 配列
  array = [];
  // フォーム数
  forms = 1;
  // JSONに変換
  toJson = JSON.stringify(this.array);
  // JSONから配列に変換
  toArray = JSON.parse(this.toJson);

  addForms() {
    // 直近の要素が空出ない場合、インプットボックスを追加
    if (this.array[this.forms - 1]) {
      this.forms++;
      this.onChange();
    }
  }

  removeForms(deleteId: number) {
    this.forms--;
    this.array.splice(deleteId, 1);
    this.onChange();
  }

  // @Watch("array")
  onChange() {
    // JSONに変換
    this.toJson = JSON.stringify(this.array);
    // JSONから配列に変換
    this.toArray = JSON.parse(this.toJson);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
