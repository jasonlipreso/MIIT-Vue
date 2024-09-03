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
      <button @click="deleteRecord()">Delete</button>
      <input v-model="id" type="number">
    </div>
  </main>
</template>
<script lang="ts">

  import axios from "axios";
  import swal from 'sweetalert';

  export default {
    name: "Home",
    data() {
      return {
        users: {} as any,
        id: 0
      }
    },
    methods: {
      async getRecord() {
        await axios.get("http://127.0.0.1:8000/api/user/getAll").then( async (response) => {
          this.users = response.data;
        });
      },
      async deleteRecord() {
        swal({
          title: "Are you sure?",
          text: "Delete selected record?",
          icon: "warning",
          buttons: true,
          dangerMode: true,
        })
        .then( async (willDelete) => {
          if (willDelete) {
            await axios.get("http://127.0.0.1:8000/api/user/deleteByID/" + this.id).then( async (response) => {
              if(response.data?.success) {
                swal({
                  title: "Deleted",
                  text: response.data?.message,
                  icon: "success",
                  button: "Aww yiss!",
                });
              }
              else {
                swal({
                  title: "Fail",
                  text: response.data?.message,
                  icon: "warning",
                  button: "Aww yiss!",
                });
              }
            });
          }
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
