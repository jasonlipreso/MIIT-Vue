<template>
  <main>
    <div class="container-bar p-3 m-3 bg-success">
      <h1 class="text-center bg-warning">GET ALL</h1>
      <button @click="getRecord()">Get All</button>
      <table class="table">
        <tbody>
          <tr v-for="(user, i) in users" :key="i">
            <td>{{ user?.fname }}</td>
            <td>{{ user?.lname }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="container-bar p-3 m-3">
      <h1 class="text-center">Delete</h1>
    </div>
  </main>
</template>
<script lang="ts">

  import axios from "axios";

  export default {
    name: "Home",
    data() {
      return {
        users: {} as any
      }
    },
    methods: {
      async getRecord() {
        await axios.get("http://127.0.0.1:8000/api/user/getAll").then( async (response) => {
          this.users = response.data;
        });
      }
    },
    
  }
</script>
<style scope>
  .container-bar {
    border: 3px solid black;
  }
</style>
