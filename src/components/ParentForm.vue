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
          <button @click.prevent="addNewChild" v-if="childList.length<5" class="list-button">
            <svg 
              width="24"
              height="24"
              class="list-icon"
              role="img">
              <use xlink:href="../assets/plus-icon.svg#plus-icon"></use>
            </svg><span class="list-button-text">Добавить ребёнка</span>
          </button>
        </div>
        <div v-for="(child, index) in childList" :key="index">
          <child-component
            @setName="updateChildName" 
            @setAge="updateChildAge" 
            :childIndex="index" 
            :childInfo="child"
          />
          <button @click.prevent="removeChild(index)" class="list-button-delete">Удалить</button>
        </div>
      </div>
      <button @click.prevent="saveParentInfo" type="submit" class="save-button">Сохранить</button>
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
  
  <style >
  </style>