<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong> {{ followers }}
      </div>
    </div>
    <div class="user-profile__tweets-wrapper">
      <TweetItem
        v-for="tweet in user.tweets"
        :key="tweet.id"
        :username="user.username"
        :tweet="tweet"
        @favorite="toggleFavorite"
      />
    </div>
  </div>
</template>

<script>
import TweetItem from "./TweetItem";
export default {
  name: "UserProfile",
  components: { TweetItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "_RahulDogra",
        firstname: "Rahul",
        lastname: "Dogra",
        email: "rahuldogra1998@gmail.com",
        isAdmin: true,
        tweets: [
          { id: 1, content: "Tweeter is Amazing" },
          { id: 2, content: "Dont forget ot follow" },
        ],
      },
    };
  },
  watch: {
    followers(newFollowCount, oldFollowCount) {
      if (oldFollowCount < newFollowCount) {
        console.log(`${this.user.username} has gained Follower`);
      }
    },
  },
  computed: {
    fullName() {
      return `${this.user.firstname} ${this.user.lastname}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavorite(id) {
      console.log(`Favorited Tweet #${id}`);
    },
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-gap: 50px;
  padding: 50px 5%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}
h1 {
  margin: 0;
}
.user-profile__admin-badge {
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}
.user-profile__twoots-wrapper {
  display: grid;
  grid-gap: 10px;
  margin-bottom: auto;
}
</style>