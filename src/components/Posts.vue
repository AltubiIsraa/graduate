<script setup>
import { ref, onErrorCaptured } from "vue";
// import UserCardVue from "./UserCard.vue";
// const SelectedUser = ref(null);
const response = ref({});

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
  await fetch("https://jsonplaceholder.typicode.com/posts/")
).json();
</script>

<template>
  <div>
    <div
      v-for="item in response"
      v-bind:key="item.id"
      :value="item"
      class="card"
    >
      <p>Title:</p>
      <h5>{{ item.title }}</h5>
      <p>Post:</p>
      <h5>{{ item.body }}</h5>
    </div>
    <br /><br />
  </div>
</template>

<style>
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
