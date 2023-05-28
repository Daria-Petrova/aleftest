<template>
    <form class="form-wrapper">
      <p class="form-title">Персональные данные</p>
      <div class="form-container">
        <div class="input-wrapper">
          <label for="name" class="input-label">Имя</label>
          <input id="name" class="input-data" v-model="parentName"/>
        </div>
        <div class="input-wrapper">
          <label for="age" class="input-label">Возраст</label>
          <input id="age" class="input-data" v-model="parentAge"/>
        </div>
      </div>
      <div class="list-wrapper">
        <div class="list-title-wrapper">
          <h3 class="list-title">Дети (макс.5)</h3>     
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
  
<style>
.form-wrapper {
  margin: 0 auto;
  max-width: 620px;
  padding: 0 10px;
  width: 95%;
}

.form-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 33px;
  box-sizing: border-box;
  vertical-align: middle;
}

.form-title{
  margin: 30px 0 20px;
  font-family: var(--font);
  font-style: normal;
  font-weight: 500;
  font-size: var(--font-size-bigger);
  line-height: 24px;
}

.input-wrapper {
  box-sizing: border-box;
  border: 1px solid #dedede;
  padding: 8px 16px;
  border-radius: 5px;
  margin: 5px 0;
}

.input-label {
  display: block;
  color: var(--text-color-poor);
}

.input-data {
  width: 100%;
  color: #000000;
  border: none;
  outline: none;
  font-family: var(--font);
  font-style: normal;
  font-weight: 400;
  font-size: var(--font-size);
  line-height: 24px;
}

input:-webkit-autofill,
input:-webkit-autofill:hover, 
input:-webkit-autofill:focus {
  -webkit-box-shadow: 0 0 0px 40rem #ffff inset;
}

.list-wrapper{
  margin: 34px 0 30px; 
}

.list-title-wrapper{
  display: flex;
  align-items: center;
  width: 620px;
  margin-bottom: 10px;
}

.list-title {
  font-family: var(--font);
  font-style: normal;
  font-weight: 500;
  font-size: var(--font-size-bigger);
  line-height: 24px;
  margin-right: auto;
}

.list-title-wrapper {
  display: inline-flex;
}

.list-button {
  display: flex;
  justify-content: center;
  border: 3px solid var(--text-color-accent);
  width: 204px;
  border-radius: 100px;
  position: relative;
  text-align:center;
  vertical-align: middle;
  padding: 8px 0;
  box-sizing: border-box;
  color: var(--text-color-accent);
  background-color: var(--main-color);
  transition: border 0.3s, color 0.3s, background-color 0.3s;
  cursor: pointer;
  font-family: var(--font);
  align-self: center;
  font-weight: 400;
  font-size: var(--font-size);
  line-height: 24px;
}

.list-button:hover{
  border: 3px solid var(--text-color-accent);
  color: var(--main-color);
  transition: border 0.3s, color 0.3s, background-color 0.3s;
  background-color: var(--text-color-accent);
}

.list-icon {
  align-self: center;
}

.list-button-text {
  font-family: var(--font);
  align-self: center;
  font-weight: 400;
  font-size: var(--font-size);
  line-height: 24px;
  padding-left: 4px;
}

.list-button-delete {
  color: var(--text-color-accent);
  border: none;
  outline: none;
  background-color: var(--main-color);
  font-family: var(--font);
  font-style: normal;
  font-weight: 400;
  font-size: var(--font-size);
  line-height: 24px;
  cursor: pointer;
  transition: color 0.3s;
}

.list-button-delete:hover {
  color: #7c69e6;
  transition: color 0.3s;
}

.save-button {
  display: flex;
  justify-content: center;
  border: 3px solid var(--text-color-accent);
  width: 118px;
  border-radius: 100px;
  position: relative;
  text-align:center;
  vertical-align: middle;
  padding: 8px 0;
  box-sizing: border-box;
  color: var(--main-color);
  background-color: var(--text-color-accent);
  transition: border 0.3s,background-color 0.3s;
  cursor: pointer;
  font-family: var(--font);
  font-style: normal;
  font-weight: 400;
  font-size: var(--font-size);
  line-height: 24px;
}

.save-button:hover {
  border: 3px solid #0970a3;
  background-color: #0970a3;
  transition: border 0.3s, background-color 0.3s;
}
</style>