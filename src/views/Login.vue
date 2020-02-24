<template>
  <div>
    <ul>
      <li>用户名：<input
          v-model="username"
          placeholder="请输入用户名"
          autofocus
        ></li>
      <li> 密码 ：<input
          v-model="password"
          type="password"
          placeholder="请输入密码"
          @keyup.enter="handLogin"
        >
        <Icon
          :type="visible ? 'iconxianshimima':'iconbuxianshimima'"
          @onclick="handleShow"
        ></Icon>
      </li>
      <li><button @click="handLogin">登录</button></li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import Icon from "../components/Icon";

export default {
  // 数据
  data() {
    return {
      username: "",
      password: "",
      visible:false
    };
  },
  components: {
    Icon
  },
  // 事件绑定功能
  methods: {
    handLogin() {
      if (this.username.trim() === "") {
        alert("用户名不能为空");
        return;
      }
      if (this.password.trim() === "") {
        alert("密码不能为空");
        return;
      }
      axios({
        url: "/api/login",
        data: { username: this.username, password: this.password },
        method: "post"
      }).then(res => {
        if (res.data.code === 200) {
          localStorage.setItem("username", res.data.data.username);
        } else if (res.data.code === 400) {
          alert(res.data.message);
        }
      });
    },
    handleShow(){
      this.visible = !this.visible
    }
  }
};
</script>

<style>
</style>