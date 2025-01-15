<template>
  <div class="data-fetcher">
    <h1>JSONPlaceholder API</h1>

    <div class="input-section">
      <h2>Input Details</h2>
      <form @submit.prevent="handleSubmit">
        <div>
          <label for="first-name">First Name:</label>
          <input type="text" id="first-name" v-model="formData.firstName" required />
        </div>
        <div>
          <label for="last-name">Last Name:</label>
          <input type="text" id="last-name" v-model="formData.lastName" required />
        </div>
        <div>
          <label for="email">Email:</label>
          <input type="email" id="email" v-model="formData.email" required />
        </div>
        <button type="submit">Submit</button>
      </form>
    </div>

    
    <div class="data-section">
      <h2>Posts</h2>
      <div class="cards">
        <div v-for="post in posts" :key="post.id" class="card">
          <h3>{{ post.title }}</h3>
          <p>{{ post.body }}</p>
        </div>
      </div>

      
      <h2>Comments</h2>
      <div class="cards">
        <div v-for="comment in comments" :key="comment.id" class="card">
          <strong>{{ comment.name }}</strong> ({{ comment.email }})
          <p>{{ comment.body }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'DataFetcher',
  data() {
    return {
      posts: [],
      comments: [],
      formData: {
        firstName: '',
        lastName: '',
        email: '',
      },
    };
  },
  created() {
    this.fetchPosts();
    this.fetchComments();
  },
  methods: {
    async fetchPosts() {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts');
        this.posts = response.data;
      } catch (error) {
        console.error('Error fetching posts:', error);
      }
    },
    async fetchComments() {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/comments');
        this.comments = response.data;
      } catch (error) {
        console.error('Error fetching comments:', error);
      }
    },
    handleSubmit() {
      console.log('Form Submitted:', this.formData);
      alert(`Hello ${this.formData.firstName} ${this.formData.lastName}, your email is ${this.formData.email} and form has been submitted`);
    }
  },
};
</script>

<style scoped>
.data-fetcher {
  font-family: Arial, sans-serif;
  padding: 20px;
  max-width: 800px;
  margin: 0 auto;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 8px;
}

h1 {
  text-align: center;
  color: #333;
}

.input-section {
  margin-bottom: 20px;
}

.input-section form {
  display: flex;
  flex-direction: column;
}

.input-section label {
  margin-bottom: 5px;
  font-weight: bold;
}

.input-section input {
  margin-bottom: 15px;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 10px 15px;
  background-color: black;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}


.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

.card {
  background-color:black;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 15px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.card h3 {
  margin-bottom: 10px;
  color: #007bff;
}

.card p {
  margin: 0;
  color:white;
}
</style>
