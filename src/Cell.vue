<template>
<div>
  <div class="cell" v-on:click="onClickSelf">
    <template v-if="a">{{text}}</template>
    <template v-else></template> 
  </div>
</div>
</template>

<script>
export default {
    props: ["n",`finished`],
    data() {
    return { a: false, text: "" };
  },
  methods: {
      onClickSelf() {
          if (this.text !== ""){
              return;
          }
          if (this.finished){
              return;
          }
          this.a= true;
          this.text = this.n % 2 === 0 ? "x" : "o";
          this.$emit("click",this.text);
         
      }
  }
};
</script>

<style>
.cell {
  border: 1px solid #CCCCCC;
  width: 100px;
  height: 100px;
  display: flex;
  justify-content:center;
  align-items: center;
  font-size: 90px;
  background-color: bisque;
}
</style>
