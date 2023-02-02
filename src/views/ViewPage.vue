<template>
    <div>
        <base-header class=" pb-6 pt-5 pt-md-2 bg-gradient-success"></base-header>
      <h1>{{ itemName }}</h1>
    </div>
  </template>
  
  <script>
  export default {
    computed: {
      itemName() {
        return this.$route.params.name;
      },
    },
  };
  </script>