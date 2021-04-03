<template>
  <div>
    <h1>User</h1>
    <ul>
      <li v-for="(user, index) in users" :key="user.id">
        {{ user.name }}
        <router-link :to="`/user/${user.id}`" class="btn btn-primary"
          >詳細</router-link
        >
        <router-link :to="`/user/${user.id}/edit`" class="btn btn-success"
          >更新</router-link
        >
        <span class="btn btn-danger" @click="userDelete(index, user.id)"
          >削除</span
        >
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: [],
    };
  },
  methods: {
    userDelete(index, id) {
      axios
        .delete("/api/user/" + id)
        .then((response) => {
          // this.users.slice(id, 1);
          this.users.splice(index, 1);
        })
        .catch((error) => console.log(error));
    },
  },
  created() {
    axios
      .get("/api/user")
      .then((response) => {
        this.users = response.data.users;
      })
      .catch((error) => {
        console.log(error);
      });
  },
};
</script>
