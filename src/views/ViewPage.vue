<template>
    <div>
        <base-header class=" pb-6 pt-5 pt-md-2 bg-gradient-success"></base-header>

        <div class="mt-4 ml-4">
            <h1>{{ itemName }}</h1>
            <h4>{{ itemBody }}</h4>
        </div> 
    </div>
  </template>
  
  <script>
  export default {
    computed: {
      itemName() {
        return this.$route.params.name;
      },
      itemBody() {
        return this.$route.params.body;
      },
    },
  };
  </script>