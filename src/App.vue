https://5xcamp.us/auo-app1
<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const urlName = ref('');
const url = ref('');
const likeList = ref([]);

onMounted(() => {
  const storage = localStorage.getItem('likeList-strg');
  if (storage != undefined) {
    const result = JSON.parse(storage);
    console.log(result);
    likeList.value = result;
  }
});

const addLike = () => {
  console.log('click');
  if (url != '') {
  }
  const like = { url: url.value, name: urlName.value };
  likeList.value.push(like);
  localStorage.setItem('likeList-strg', JSON.stringify(likeList.value));
};

const clearLike = () => {
  likeList.value = [];
  localStorage.removeItem('likeList-strg');
};

const delLike = (i) => {
  likeList.value.splice(i, 1);
  localStorage.setItem('likeList-strg', JSON.stringify(likeList.value));
};
</script>

<template>
  <h1 class="text-3xl">我的最愛</h1>
  <h1 class="text-s">輸入要儲存的網址</h1>
  <input @keyup.enter="addLike" v-model.trim="url" type="text" class="input" />
  <h1 class="text-s">給它取個名字</h1>
  <input v-model.trim="urlName" type="text" class="input" />
  <button @click="addLike" class="btn btn-large">新增看看</button>
  <button @click="clearLike" class="btn btn-large">清空</button>
  <hr />
  <ul>
    <li v-for="(l, i) in likeList" :key="l.id">
      {{ i + 1 }}.
      <a :href="l.url" target="_blank">{{ l.name }}</a>
      <button @click="delLike(i)" class="btn btn-large">刪除</button>
    </li>
  </ul>
</template>
