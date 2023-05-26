<template>
    <div class="wrap">
      <div class="input-wrapper child-input">
        <label for="name" class="input-label">Имя</label>
        <input  id="name" class="input-data" v-model="childName"/>
      </div>
      <div class="input-wrapper child-input">
        <label for="age" class="input-label">Возраст</label>
        <input id="age" class="input-data" v-model="childAge"/>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: "ChildComponent",
    props: {
      childIndex: {
        type: Number,
        default: null 
      },
      childInfo: {
        name: {
          type: String,
          default: ''
        },
        age: {
          type: Number,
          default: null
        }
      }
    },
    data(){
      return {
        childName: '',
        childAge:''
      }
    },
    watch: {
      childName() {
        this.$emit('setName', {childName: this.childName,  index: this.childIndex });
      },
      childAge() {
        this.$emit('setAge', { childAge: this.childAge, index: this.childIndex });
      },
      childInfo() {
        this.childName = this.childInfo.name
        this.childAge = this.childInfo.age
      }
    }
  }
  </script>
  
  <style>
  .child-input.input-wrapper {
    margin-right: 20px;
  }
  .wrap {
    display: inline-flex;
  }
  </style>