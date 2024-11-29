<template>
    <div class="home">
      <h1>Books</h1>
      <button @click="$router.push('/add')">Add New Book</button>
      <div v-if="books.length">
        <div v-for="book in books" :key="book._id" class="book-item">
          <img :src="book.coverImage" alt="Book Cover" />
          <h2>{{ book.title }}</h2>
          <p>Author: {{ book.author }}</p>
          <p>Publisher: {{ book.publisher }}</p>
          <p>Quantity: {{ book.qty }}</p>
        </div>
      </div>
      <p v-else>No books available.</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        books: [],
      };
    },
    async created() {
      try {
        const response = await fetch("http://localhost:5000/api/books");
        if (response.ok) {
          this.books = await response.json();
        } else {
          console.error("Failed to fetch books.");
        }
      } catch (error) {
        console.error("Error fetching books:", error);
      }
    },
  };
  </script>
  
  <style scoped>
  .home {
    max-width: 800px;
    margin: auto;
    text-align: center;
  }
  .book-item {
    border: 1px solid #ddd;
    border-radius: 8px;
    margin: 10px 0;
    padding: 10px;
    display: flex;
    align-items: center;
    gap: 20px;
  }
  img {
    width: 100px;
    height: 150px;
    object-fit: cover;
    border-radius: 4px;
  }
  </style>
  