<script setup>
import { ref, onErrorCaptured } from "vue";
import PostsCardVue from "./PostsCard.vue";
import UserCardVue from "./UserCard.vue";
const SelectedPos = ref(null);
const SelectedUser = ref({});
const response = ref({});
const responsepost = ref({});

// adding delay

await new Promise((resolve) => {
  setTimeout(() => {
    resolve();
  }, 1000);
});

onErrorCaptured((err) => {
  // error processing
});

response.value = await (
  await fetch("https://jsonplaceholder.typicode.com/users/")
).json();

async function onChange() {
  console.log("hi");

  responsepost.value = await (
    await fetch(
      `https://jsonplaceholder.typicode.com/users/${SelectedUser.value.id}/posts`
    )
  ).json();
}
</script>

<template>
  <br /><br />
  <div class="box">
    <select class="choose" v-model="SelectedUser" @change="onChange">
      <option v-for="item in response" v-bind:key="item.id" :value="item">
        {{ item.name }}
      </option>
    </select>
  </div>
  <br /><br />
  <UserCardVue :user="SelectedUser" />
  <br /><br />
  <H3>Posts by this User</H3>
  <div v-for="item in responsepost" v-bind:key="item.id" :value="item">
    <div class="card">
      <p>Title:</p>
      <h5>{{ item.title }}</h5>
      <p>Post:</p>
      <h5>{{ item.body }}</h5>
    </div>
  </div>
  <br /><br />
</template>
<style>
/* .box {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
} */

.box select {
  background-color: #194e3763;
  color: white;
  padding: 12px;
  width: 250px;
  border: none;
  font-size: 20px;
  box-shadow: 0 5px 25px rgba(0, 0, 0, 0.2);
  -webkit-appearance: button;
  appearance: button;
  outline: none;
}

.box::before {
  content: "\f13a";
  font-family: FontAwesome;
  position: absolute;
  top: 0;
  right: 0;
  width: 20%;
  height: 100%;
  text-align: center;
  font-size: 28px;
  line-height: 45px;
  color: rgba(255, 255, 255, 0.5);
  background-color: rgba(255, 255, 255, 0.1);
  pointer-events: none;
}

.box:hover::before {
  color: rgba(255, 255, 255, 0.6);
  background-color: rgba(255, 255, 255, 0.2);
}

.box select option {
  padding: 30px;
}
.card {
  box-shadow: 0 4px 8px 0 rgba(255, 255, 255, 0.827);
  transition: 0.3s;
  width: 40%;
  border-radius: 5px;
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgb(255, 255, 255);
}

.container {
  padding: 2px 16px;
}
</style>
