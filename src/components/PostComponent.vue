<template>

<!-- Container -->
<div class="container">

  <!-- Form -->
  <form class="create-post">
    <div id="first">
    <label for="create-post">Exercises</label><br>
    <input type="text" id="create-post" v-model="text" placeholder="Add your exercises..">
    </div>
    <div id="second">
    <label id="set" for="create-time">Reps</label><br>
    <input type="text" id="create-time" v-model="sets" placeholder="Add your reps..">
    </div>
    <button class="add" v-on:click="createPost"><span>+</span>Add to list</button>
  </form>

  <!-- Create post -->
  <p class="error" v-if="error">{{ error }} </p>
  <div class="post-container">
  <div class="post"
        v-for="(post, index) in posts"
        v-bind:item="post"
        v-bind:index="index"
        v-bind:key="post._id"
      >
      
      <!-- Text -->
      <p class="text"
        v-if ="!post.editmode"
        >
        {{post.text}}
        {{post.sets}}
      </p>
      <input class="input-field"
        v-else
        v-model="post.text"
        >

    <!-- Buttons -->
    <button class="edit" v-on:click="enterEditmode(post)"><i class="fas fa-edit"></i></button>
    <button class="update" v-on:click="updatePost(post._id, post.text)"><i class="far fa-save"></i></button>
    <button class="delete" v-on:click="deletePost(post._id)"><i class="far fa-trash-alt"></i></button>
    </div>
  </div>
</div>
</template>

<!-- Script -->
<script>
import PostService from '../PostService';

export default {
  name: 'PostComponent',
  data() {
    return {
      posts: [],
      error: "",
      text: "",
      sets: "",
      isFinished:true,
    }
  },
  async created() {
    try {
      this.posts = await PostService.getPosts();
    } catch(err) {
      this.error = err.message;
    }
  },
  methods: {
    // Create post
    async createPost() {
      await PostService.insertPost(this.text+ " x " + this.sets);
      this.posts = await PostService.getPosts();
    },
    // Uppdate post
    async updatePost(id, text) {
      await PostService.updatePost(id, text);
      this.posts = await PostService.getPosts();
    },
    // Edit post
    enterEditmode(post) {
      post.editmode = true;
      this.posts = [...this.posts];
    },
    // Delete post
     async deletePost(id) {
      await PostService.deletePost(id);
      this.posts = await PostService.getPosts();
    }

  }
}
</script>

<!-- Style -->
<style scoped>

div.container {
  max-width: 700px;
  margin: 0px auto;
  text-align: left;
  background-color: #fff;
}

form {
  padding: 40px 20px;
  display: grid;
  grid-template-columns: 50% 50%;
}

form input {
  width: 100%;
}

p.error {
  color: #ff7272;
}

label {
  font-size: 26px;
  font-weight: 800;
}


input {
  padding: 10px 0;
  border: none;
  background-color: transparent;
}

input::placeholder {
  font-size: 14px;
  font-weight: 100;
  color: #333;
}

.input-field {
  padding: 20px;
  margin: 0;
  font-family: 'Muli', arial, sans-serif;
  font-size: 16px;
  font-weight: 400;
  color: blue;
}

button.add {
  width: 120px;
  padding: 5px;
  margin-top: 5px;
  font-family: 'Open Sans', 'Muli', arial, sans-serif;
  font-size: 14px;
  font-weight: 600;
  background-color: #d6dde2;
  border: none;
  cursor: pointer;
  text-align: left;
}

button.add span {
  padding: 5px 10px;
  margin-left: -5px;
  margin-right: 10px;
  background-color: #c2ccd3;
}

button.edit {
  margin-left: 20px;
  position: absolute;
  top: 20px;
  right: 160px;
  color: #000;  
  cursor: pointer;
  border: none;
  background-color: transparent;
  font-size: 16px;
}

button.update {
  margin-left: 20px;
  position: absolute;
  top: 20px;
  right: 90px;
  color: #000;  
  cursor: pointer;
  border: none;
  background-color: transparent;
  font-size: 16px;
}

button.delete {
  position: absolute;
  top: 20px;
  right: 20px;
  color: red;  
  cursor: pointer;
  border: none;
  background-color: transparent;
  font-size: 16px;
}

div.post {
  position: relative;
  background-color: #e9edf0;
}

p.text {
  padding: 20px;
  margin: 0;
  font-size: 16px;
  font-weight: 400;
}

@media only screen and (max-width: 1024px) {
div.container {
  max-width: 800px;
}
}

</style>
