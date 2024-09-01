<template>
  <div>
    <h1>Get All Users</h1>
    <div v-if="users.length">
      <div><b>จำนวนผู้ใช้งาน:</b> {{ users.length }}</div>
      <div v-for="user in users" :key="user.id">
        <div><b>id:</b> {{ user.id }}</div>
        <div><b>ชื่อผู้ใช้:</b> {{ user.name }} {{ user.lastname }}</div>
        <div><b>อีเมล:</b> {{ user.email }}</div>
        <div><b>status:</b> {{ user.status }}</div>
        <div><b>type:</b> {{ user.type }}</div>
        <div>
          <button @click="navigateTo('/user/' + user.id)">ดูข้อมูล</button>
        </div>
        <hr />
      </div>
    </div>
  </div>
</template>

<script>
import UsersService from "@/services/UsersService";

export default {
  data() {
    return {
      users: []
    };
  },
  async created() {
    try {
      this.users = (await UsersService.index()).data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    navigateTo(path) {
      this.$router.push(path);
    }
  }
};
</script>

<style>
</style>
