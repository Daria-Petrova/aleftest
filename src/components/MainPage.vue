<template>
    <div>
      <ul>
        <li 
          v-for="item in formList"
          :key="item"
          @click="current = item.name">{{ item.title }}</li>
      </ul>
      <component :is="current" :info="parentInformation" @parentInfo="getParentInfo"></component>
    </div>
  </template>
  
  <script>
  import ParentForm from "./ParentForm.vue";
  import ParentPreview from "./ParentPreview.vue";

  export default {
    name: "MainPage",
    components: {
      ParentPreview, 
      ParentForm},
    data(){
      return {
        current: 'ParentForm',
        formList: [
          { 
            name: 'ParentForm',
            title: 'Форма'
          },
          { 
            name: 'ParentPreview',
            title: 'Превью'
          }],
        parentInformation: null
      }
    },
    methods: {
      getParentInfo(info) {
        this.parentInformation = info
      }
    }
  }
  </script>