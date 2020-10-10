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
      @favorite="toggleFavorite"
    />
  </ul>
  <form
    class="create-twoot-panel"
    @submit.prevent="createNewTwoot"
    :class="{ '--exceeded': newTwootCharacterCount > 180 }"
  >
    <label for="newTwoot"
      ><strong>New Twoot</strong> ({{ newTwootCharacterCount }}/180)</label
    >
    <textarea id="newTwoot" rows="4" v-model="this.newTwootContent" />

    <div class="create-twoot-panel__submit">
      <div class="create-twoot-type">
        <label for="newTwootType"><strong>Type: </strong></label>
        <select id="newTwootType" v-model="this.selectedTwootType">
          <option
            :value="option.value"
            v-for="(option, index) in this.twootTypes"
            :key="index"
          >
            {{ option.name }}
          </option>
        </select>
      </div>

      <button>Twoot It!</button>
    </div>
  </form>
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
      newTwootContent: "",
      selectedTwootType: "instant",
      twootTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant Twoot" },
      ],
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
newTwootCharacterCount(){
  return this.newTwootContent.length
}
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavorite(id) {
      console.log("hii", id);
    },
     createNewTwoot() {
      if (this.newTwootContent && this.selectedTwootType !== 'draft') {
        this.user.twoots.unshift({
          id:this.user.twoots.length+1,
          content:this.newTwootContent
        })
        this.newTwootContent = '';
      }
    }
  },
  //   mounted() {
  //     this.followUser();
  //   },
};
</script>

<style lang="scss" scoped>
.create-twoot-panel {
  margin-top: 20px;
  padding: 20px 0;
  display: flex;
  flex-direction: column;
  textarea {
    border: 1px solid #DFE3E8;
    border-radius: 5px;
  }
  .create-twoot-panel__submit {
    display: flex;
    justify-content: space-between;
    .create-twoot-type {
      padding: 10px 0;
    }
    button {
      padding: 5px 20px;
      margin: auto 0;
      border-radius: 5px;
      border: none;
      background-color: deeppink;
      color: white;
      font-weight: bold;
    }
  }
  &.--exceeded {
    color: red;
    border-color: red;
    .create-twoot-panel__submit {
      button {
        background-color: red;
        color: white;
      }
    }
  }
}
</style>
