<template>
  <div class="home">
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <h2>user id</h2>
    <div>{{ userId }}</div>
    <hr />
    <h2>URL</h2>
    <div>{{ msg }}</div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import liff from "@line/liff";

export default {
  name: "Home",
  components: {
    HelloWorld,
  },
  data() {
    return {
      msg: "",
      userId: "",
    };
  },
  mounted() {
    liff
      .init({
        liffId: "1654463380-RJGL0Gog",
      })
      .then((res) => {
        if (!liff.isLoggedIn()) liff.login();

        liff.getProfile().then((profile) => {
          const userId = profile.userId;
          this.userId = userId;
          this.msg = window.location.href;
        });
      })
      .catch((err) => {
        alert(err.code, err.message);
        alert("綁定異常，請聯絡作者");
      });
  },
  methods: {},
};
</script>
