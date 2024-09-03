<template>
  <main>
    <h1 class="p-5">GET ALL</h1>
    <button @click="fetchAll()">Get All</button>
  </main>
</template>
<script lang="ts">
  import axios from "axios";
  export default {
    name: "Home",
    methods: {
      async fetchAll() {
        axios.get("http://127.0.0.1:8000/api/user/getAll").then( async (response) => {
          console.log(response);
        });
      }
    },
  }
</script>
