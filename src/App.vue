<template>
  <div class= "wrapper">
    <span>井字棋</span>
    <div class="header">第 {{n}} 手</div>
    <div class="chess">
    <div class="row">
      <Cell v-on:click="onClickCell(0, $event)" v-bind:n="n" v-bind:finished="finished" /><!-- v-on: 可缩写为 @ ，v-bind 可以省略 -->
      <Cell v-on:click="onClickCell(1, $event)" v-bind:n="n" v-bind:finished="finished"/>
      <Cell v-on:click="onClickCell(2, $event)" v-bind:n="n" v-bind:finished="finished"/>
    </div>
    <div class="row">
      <Cell v-on:click="onClickCell(3, $event)" v-bind:n="n" v-bind:finished="finished" />
      <Cell v-on:click="onClickCell(4, $event)" v-bind:n="n" v-bind:finished="finished"/>
      <Cell v-on:click="onClickCell(5, $event)" v-bind:n="n" v-bind:finished="finished"/>
    </div>
    <div class="row">
      <Cell v-on:click="onClickCell(6, $event)" v-bind:n="n" v-bind:finished="finished"/>
      <Cell v-on:click="onClickCell(7, $event)" v-bind:n="n" v-bind:finished="finished"/>
      <Cell v-on:click="onClickCell(8, $event)" v-bind:n="n" v-bind:finished="finished"/>
    </div>
    </div>
    <!-- v-on:click="onClickCell 对应 Cell.vue 的 this.$emit: ("click") 
    v-bind:n="n"  对应 Cell.vue 的 props : ["n"]
    -->
    <div class="result">结果：{{result === null ? '紧张决战中...': `游戏结束， 恭喜 ${result} 方胜利！`}}</div>
    <p>tips:两个玩家，一个打圈(o)，一个打叉（x），轮流在3乘3的格上打自己的符号，最先以横、直、斜连成一线则为胜。</p>
  </div>
</template>

<script>
import Cell from "./Cell";
export default {
  components: { Cell },
  data() {
    return {
     n:0,
     map: [
       [null, null, null],
       [null, null, null],
       [null, null, null]
    ],
     result: null,
     finished: false
     };
  },
  methods: {
    onClickCell(i,text) {
      console.log(`${i}被点击，内容是: ${text}`);
      this.map[Math.floor(i/3)][i%3] = text;
      this.n += 1;
      this.tell();
    },
    tell() {
      const map = this.map;
      for (let i = 0; i<=2; i++){
       if(
         map[i][0] !== null && 
         map[i][0] === map[i][1] && 
         map[i][1] === map[i][2]
         ) {
         this.result = map[i][0];
         this.finished = true;
       } 
      }
      for(let j=0;j<=2;j++){
        if( 
          map[0][j] !== null && 
          map[0][j]===map[1][j] &&
          map[1][j]===map[2][j]
          ) {
          this.result = map[0][j];
          this.finished = true;
        }
      }
      if(
        map[0][0] !== null && 
        map[0][0] === map[1][1] && 
        map[1][1]===map[2][2]
        ){
          this.result = map[0][0];
          this.finished = true;
        }
       if(
        map[0][2] !== null && 
        map[0][2] === map[1][1] && 
        map[1][1]===map[2][0]
        ){
          this.result = map[0][2];
          this.finished = true;
        }
    }
  }
};
</script>

<style>
.row{
  display: flex;
}
.wrapper{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background-color:#E1E1E1;
  height: 100vh;

}
.result{
  margin-top: 10px;
  font-size: 18px;
  color:dimgrey;
}
span{
  margin-top: 10px;
  margin-bottom: 10px;
  font-size: 18px;
  color:black;
}
</style>
