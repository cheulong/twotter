<template>
  <div id="app">
    {{ user.userName }}-{{ fullName }} <strong>followers:</strong
    >{{ followers }}
    <br />
    <div v-if="!user.isAdmin">Admin</div>
  </div>
  <button @click="followUser">Follow</button>
  <ul>
    <TwootItem
      v-for="twoot in user.twoots"
      :key="twoot.id"
      :userName="user.userName"
      :twoot="twoot"
    />
  </ul>
</template>

<script>
import TwootItem from "./TwootItem";
export default {
  name: "UserProfile",
  components: { TwootItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        userName: "userName",
        firstName: "firstName",
        lastName: "lastName",
        isAdmin: false,
        twoots: [
          {
            id: 1,
            content: "1",
          },
          {
            id: 2,
            content: "2",
          },
        ],
      },
    };
  },
  watch: {
    followers(newData, oldData) {
      if (oldData < newData) {
        console.log(`${this.user.userName} has gained follower`);
      }
    },
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
  },
  //   mounted() {
  //     this.followUser();
  //   },
};
</script>

<style>
</style>