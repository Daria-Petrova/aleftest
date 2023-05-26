<template>
    <form class="form-wrapper">
      <div class="input-wrapper">
        <label for="name" class="input-label">Имя</label>
        <input id="name" class="input-data" v-model="parentName"/>
      </div>
      <div class="input-wrapper">
        <label for="age" class="input-label">Возраст</label>
        <input id="age" class="input-data" v-model="parentAge"/>
      </div>
      <div class="list-wrapper">
        <div class="list-title-wrapper">
          <p class="list-title">Дети (макс.5)</p>
          <button @click.prevent="addNewChild" v-if="childList.length < 5" class="list-button">Добавить ребёнка</button>
        </div>
        <div v-for="(child, index) in childList" :key="index" class="d-flex flex-row">
          <child-component
            @setName="updateChildName" 
            @setAge="updateChildAge" 
            :childIndex="index" 
            :childInfo="child"
          />
          <button @click="removeChild(index)">Удалить</button>
        </div>
      </div>
      <button class="bgbutton" @click.prevent="saveParentInfo" type="submit">Сохранить</button>
    </form>
  </template>
  
  <script>
  
  import ChildComponent from "./ChildComponent.vue"
  export default {
    name: "ParentForm",
    components: {ChildComponent},
    data(){
      return {
        parentName: '',
        parentAge: '',
        childList: [],
        
        childName: '',
        childAge: '',
        
        parent: {
          name: null,
          age: null,
          children: []
        },
      }
    },
    methods: {
      saveParentInfo: function() {
        if (this.parentName && this.parentAge){
          this.parent.name = this.parentName
          this.parent.age = this.parentAge
          this.parent.children = this.childList
          console.log('this.parent',this.parent)
          this.$emit('parentInfo', this.parent);
        }
      },
      addNewChild: function() {
        const newChild = {
          name: this.childName,
          age: this.childAge
        }
        this.childList.push(newChild);
      },
      removeChild: function(index) {
        this.childList.splice(index, 1);
      },
      updateChildAge: function(ageInfo) {
        let index  = ageInfo.index
        let age = ageInfo.childAge
        for (let i = 0 ; i < this.childList.length; i++) {
          if (i === index) {
            this.childList[i].age = age
            break
          }
        }
      },
      updateChildName: function(nameInfo) {
        let index  = nameInfo.index
        let name = nameInfo.childName
        for (let i = 0 ; i < this.childList.length; i++) {
          if (i === index) {
            this.childList[i].name = name
            break
          }
        }
      }
    }
  }
  </script>
  
  <style>
  .form-wrapper {
    margin: 0 auto;
    max-width: 800px;
    width: 100%;
  }
  
  .input-wrapper {
    border: 1px solid #dedede;
    padding: 5px 10px;
    border-radius: 5px;
    margin: 5px 0;
  }
  
  .input-label {
    display: block;
    padding: 2px;
    color: #b1b1b1;
  }
  
  .input-data {
    padding: 2px;
    color: #000000;
    border: none;
    outline: none;
  }
  
  .list-title-wrapper {
    display: inline-flex;
  }
  
  .list-button{
    border: 3px solid #00b0ff;
    padding: 2px 15px;
    border-radius: 25%;
  }
  </style>