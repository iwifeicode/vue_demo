<template>
  <div class="login">
    <van-nav-bar
      title="注册"
      left-text="返回"
      right-text="登陆"
      left-arrow
      @click-left="goback"
      @click-right="go"
    />

    <van-swipe :height="150" :autoplay="3000">
      <van-swipe-item v-for="(item, index) in images" :key="index">
        <img :src="item" class="swipe-item-img">
      </van-swipe-item>
    </van-swipe>

    <van-cell-group>
      <van-field
        v-model="username"
        clearable
        label="用户名"
        placeholder="请输入用户名"
        @click-right-icon="$toast('question')"
      />

      <van-field v-model="password" type="password" label="密码" placeholder="请输入密码"/>

      <van-field v-model="nikename" type="nikename" label="昵称" placeholder="输入昵称"/>
    </van-cell-group>
    <li class="teli" v-show="error">注册失败</li>
    <van-button type="default" @click="reg">注册</van-button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      password: "",
      nikename: "",
      error: false,
      images: [
        "./img/a1.jpeg",
        "./img/a2.jpg",
        "./img/a3.jpg",
        "./img/a4.png",
        "./img/a5.jpeg"
      ]
    };
  },
  methods: {
    goback() {
      this.$router.go(-1);
    },
    go() {
      this.$router.push("/login");
    },
    reg() {
      let formData = new FormData();
      formData.append("username", this.username);
      formData.append("password", this.password);
      formData.append("nikename", this.nikename);
      axios({
        url: "http://localhost:3008/api/reg",
        data: formData,
        method: "POST"
      }).then(res => {
        if (res.data.error == 0) {
          this.$router.push("/login");
        } else {
          this.error = true;
        }
      });
    }
  }
};
</script>


<style scoped>
.van-button {
  width: 100%;
  margin-top: 30px;
}
.swipe-item-img {
  width: 100%;
}
.van-cell-group {
  margin-top: 26px;
}
.van-cell__title {
  margin-left: 20px;
}
.van-swipe {
  margin-top: 20px;
}
/* .teli{} */
</style>