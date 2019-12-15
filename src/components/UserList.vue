<template>
  <div class="user">
    <ul>
      <li v-for="user in users" :key="user.id">
        <UserItem v-bind:user="user" />
      </li>
    </ul>
  </div>
</template>

<script>
import UserItem from "@/components/UserItem.vue";

export default {
  name: "UserList",
  props: {
    msg: String
  },
  data: () => {
    return {
      users: []
    };
  },
  created: function() {
    let vm = this;
    fetch('http://telles-user-service.herokuapp.com/v1/users/', {mode: 'cors'})
      .then((response) => {
        return response.json()
          .then((json)=> { vm.$data.users = json; });
    });
  },
  components: {
    UserItem
  }
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
a {
  color: #42b983;
}
.cardapio {
  padding-top: 72px;
}
</style>