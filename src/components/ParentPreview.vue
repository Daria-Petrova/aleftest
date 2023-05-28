<template>
    <div class="form-wrapper" v-if="parent">
      <p class="form-title">Персональные данные</p>
      <p class="parent">{{ parent.name}}, {{ parent.age }} лет</p>
      <p class="form-title">Дети</p>
      <div v-for="(child, index) in parent.children" :key="index" class="child-wrapper">
        <span v-if="child" class="child">{{ child.name }}, {{ child.age }} лет</span>
      </div>
    </div>
  </template>
  
<script>
export default {
  name: "ParentPreview",
  props: ['info'],
  data() {
    return{
      parent: this.info
    }
  }
}
</script>

<style>

.parent{
  font-family: var(--font);
  font-style: normal;
  font-weight: 700;
  font-size: var(--font-size-bigger);
  line-height: 24px;
  margin-bottom: 60px;
}

.child{
  border-radius: 5px;
  display: block;
  float: left;
  clear: left;
  background-color: #f1f1f1;
  padding: 10px 20px;
  margin-bottom: 20px;
  font-family: var(--font);
  font-style: normal;
  font-weight: 700;
  font-size: var(--font-size-bigger);
  line-height: 24px;
}
</style>