<template>

  <Header />

  <div class="container mt-5 mb-5">

    <Hello message-hello="Hello VueJs 💚" />

    <div class="row">

      <div class="col-8">

        <!-- Button to toggle table visibility -->
        <span class="btn btn-info mt-4 mb-4 h3" @click="toggleTableVisibility">{{ isShow ? 'Hide 🤪' : 'Show 🫠'
          }}</span>

        <!-- Table to display posts -->
        <table class="table" v-if="isShow">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Name</th>
              <th scope="col">Description</th>
              <th scope="col">Status</th>
              <th scope="col">Toggle</th>
              <th scope="col">Edit</th>
              <th scope="col">Delete</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="post in posts" :key="post.id">
              <th scope="row">{{ post.id }}</th>
              <td>{{ post.name }}</td>
              <td>{{ post.description }}</td>
              <td>{{ post.status == 1 ? '🔛' : '📴' }}</td>
              <td><button @click="togglePostStatus(post)" class="btn btn-sm btn-outline-secondary">👽</button></td>
              <td><button @click="editPost(post)" class="btn btn-sm btn-outline-warning">🖋️</button></td>
              <td><button @click="deletePost(post)" class="btn btn-sm btn-outline-danger">❌</button></td>
            </tr>
          </tbody>
        </table>

      </div>

      <div class="col-4">

        <!-- Form for creating a new post -->
        <form @submit.prevent="createPost" class="mb-5 mt-5">
          <div class="mb-3">
            <label for="name" class="form-label">Name:</label>
            <input type="text" class="form-control" id="name" v-model="newPost.name" placeholder="Enter name" required>
          </div>
          <div class="mb-3">
            <label for="status" class="form-label">Status:</label>
            <select v-model="newPost.status" class="form-select" name="status" id="status" required>
              <option selected value="">Choose</option>
              <option value="1">On</option>
              <option value="0">Off</option>
            </select>
          </div>
          <div class="mb-3">
            <label for="description" class="form-label">Description:</label>
            <textarea class="form-control" id="description" v-model="newPost.description" rows="5"
              placeholder="Enter description" required></textarea>
          </div>
          <button type="submit" class="btn btn-primary">Create</button>
        </form>

      </div>

    </div>

  </div>

</template>


<script>
import Header from './components/Header.vue';
import Hello from './components/Hello.vue';

export default {
  components: {
    Hello,
    Header
  },
  data() {
    return {
      isShow: true,
      message: 'Hello VueJs',
      posts: [
        { id: 1, name: 'Post 1', description: 'Description for post 1', status: 1 },
      ],
      newPost: {
        id: null,
        name: '',
        description: '',
        status: '',
      },
    };
  },
  methods: {
    // Toggle table visibility
    toggleTableVisibility() {
      this.isShow = !this.isShow;
    },
    // Create a new post
    createPost() {
      const newId = this.posts.length + 1;
      this.posts.push({
        id: newId,
        name: this.newPost.name,
        description: this.newPost.description,
        status: parseInt(this.newPost.status), // Ensure status is a number
      });
      // Reset the form
      this.newPost = {
        id: null,
        name: '',
        description: '',
        status: '',
      };
    },
    // Toggle post status
    togglePostStatus(post) {
      post.status = post.status === 1 ? 0 : 1;
    },
    // Edit post (placeholder)
    editPost(post) {
      alert(`Edit post with ID: ${post.id}`);
    },
    // Delete post
    deletePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id);
    },
  },
};
</script>