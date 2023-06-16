<template>
  <div v-if="showModal" class="overlay">
    <div class="overlay-box">
      <h1>Post Data</h1>
      <label for="title">Title:</label>
      <input type="text" name="title">
      <label for="description">Description:</label>
      <textarea name="description" id="description" cols="30" rows="10" placeholder="description..."></textarea>
      <button @click="showModal = false">Submit Data</button>
      <button @click="showModal = false">Cancel</button>
    </div>
  </div>
  <nav class="navbar">
    <h1 class="title">Blog</h1>
    <button @click="showModal = true">Add new Post</button>
  </nav>

  <div>
    <h1>posts</h1>
    <button @click="showPosts">Show Posts</button>
    <p>{{ posts }}</p>
  </div>

</template>

<script setup>
import { ref } from "vue";
import axios from "axios"

const showModal = ref(false)
const posts = ref("")
let response
function showPosts() {
  response = axios.get({url: "http://localhost:5000/blog", headers: {"content-type": "application/json"}, data: {}})
  posts.value = response.data
}

</script>

<style>
.title{
  color: white;
  background-color: black;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  font-weight: bold;
  font-size: 2rem;
  border: 1px solid black;
  box-shadow: 3px 3px 15px 10px black;
}

.navbar{
  display: flex;
  justify-content: space-around;
  background-color: gray;
}

.navbar button {
  border: 0.25rem solid black;
  border-radius: 15px;
  background: linear-gradient(90deg, rgba(131,58,180,1) 0%, rgba(253,29,29,1) 50%, rgba(252,176,69,1) 100%);
  font-weight: bold;
  font-size: larger;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  margin: 15px;
  cursor: pointer;
  color: white;
}

.navbar button:hover {
  border-color: white;
}

.content {
  text-align: center;
}

.overlay{
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(48, 48, 48, 0.77);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.overlay-box{
  width: 750px;
  background-color: white;
  border-radius: 20px;
  border: 3px solid gray;
  box-shadow: 2px 2px 2px 2px gray;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.overlay-box button{
  padding: 10px 20px;
  font-size: 20px;
  widows: 100%;
  background-color: blueviolet;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
  border-radius: 20px;
}

.overlay-box input{
  margin-bottom: 10px;
}
</style>