<template>
    <div class="main-wrapper">
      <div class="header">
        <a href="email:info@alef.com" class="logo-link">
        <img src="../assets/logo.png" width="90" height="30"  alt="Alef logo">
        </a>
        <ul class="menu">
          <li class="menu-item" v-for="item in formList" :key="item" @click="current = item.name">{{ item.title }}</li>
        </ul>
      </div>
      <KeepAlive>
        <component :is="current" :info="parentInformation" @parentInfo="getParentInfo"></component>
      </KeepAlive>
      <div class="footer">
        <p>all rights reserved</p>
      </div>
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

<style>

.main-wrapper {
  display: grid;
  grid-template-areas:
    "header"
    "content"
    "footer";
  grid-template-columns: 1fr;
  grid-template-rows:
    auto
    1fr
    auto;
  min-height: 100vh;
  max-width: 1920px;
  margin: 0 auto;
  box-sizing: border-box;
  margin: 0 auto;
}

.header {
  margin: 0 auto;
  padding: 24px 60px;
  max-width: 1366px;
  width: 80%;
  display: flex;
  align-items: center;
  border-bottom: 1px solid #f2f2f2;
}


.footer {
  padding: 30px;
  background-color: #fafafa;
  text-align: center;
}

.menu {
  margin: 0 auto;
  display: flex;
  flex-direction: row;
  list-style: none;
}

.menu-item{
  padding: 0 12px;
  cursor: pointer;
}
</style>