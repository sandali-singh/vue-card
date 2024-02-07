<template>
  <div>
    <div class="heading"><h1>My card portfolio</h1></div>
    <div id="card">
      <div
        class="portfolio"
        v-for="profile in profiles"
        :key="profile.id"
        :style="{
          backgroundColor: getRandomColor(),
        }"
      >
        <div class="porfile-img">
          <img :src="profile.avatar_url" alt="Avatar" class="avatar" />
        </div>
        <div class="profile-info">
          <h2>{{ profile.login }}</h2>
          <p>{{ profile.bio }}</p>
          <a :href="profile.html_url" target="_blank" style="color: #000"
            >View Profile</a
          >
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "card-profile",
  data() {
    return {
      profiles: [],
    };
  },
  created() {
    this.$http.get("https://api.github.com/users").then(function (data) {
      console.log(data.body.slice(0, 10));
      this.profiles = data.body.slice(0, 10);
    });
  },
  methods: {
    getRandomColor() {
      const letters = "0123456789ABCDEF";
      let color = "#";
      for (let i = 0; i < 6; i++) {
        color += letters[Math.floor(Math.random() * 16)];
      }
      return color;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

#card {
  width: 100%;
  display: flex;
  justify-content: space-evenly;
  flex-wrap: wrap;
}

.portfolio {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee;
  width: 400px;
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  border-radius: 10%;
}

.heading {
  text-align: center;
  margin: 0 20px;
  padding: 16px 0;
  font-size: 42px;
}

.porfile-img {
  text-align: center;
  padding-top: 10px;
}

.avatar {
  width: 200px;
  height: 200px;
  border-radius: 50%;
}

.profile-info {
  margin-top: 12px;
  margin: 10px;
  padding: 30px;
  text-align: center;
  font-size: 24px;
}
</style>
