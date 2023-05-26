<template>
    <div>
      Превью родителя
      {{parent}}
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