<template>
    <div class="add-book">
      <h1>Add a New Book</h1>
      <form @submit.prevent="submitBook">
        <label>Title:</label>
        <input type="text" v-model="book.title" required />
  
        <label>Author:</label>
        <input type="text" v-model="book.author" required />
  
        <label>Published Date:</label>
        <input type="date" v-model="book.publishedDate" required />
  
        <label>Publisher:</label>
        <input type="text" v-model="book.publisher" required />
  
        <label>Description:</label>
        <textarea v-model="book.description" required></textarea>
  
        <label>Cover Image URL:</label>
        <input type="text" v-model="book.coverImage" required />
  
        <label>Average Rating:</label>
        <input type="number" v-model="book.rating.average" required step="0.1" min="0" max="5" />
  
        <label>Rating Count:</label>
        <input type="number" v-model="book.rating.count" required min="0" />
  
        <label>Tags (comma-separated):</label>
        <input type="text" v-model="tagsInput" placeholder="e.g., fiction, adventure" />
  
        <label>Initial Quantity:</label>
        <input type="number" v-model="book.initialQty" required min="0" />
  
        <label>Quantity:</label>
        <input type="number" v-model="book.qty" required min="0" />
  
        <button type="submit">Add Book</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        book: {
          title: "",
          author: "",
          publishedDate: "",
          publisher: "",
          description: "",
          coverImage: "",
          rating: {
            average: 0,
            count: 0,
          },
          tags: [],
          initialQty: 0,
          qty: 0,
        },
        tagsInput: "",
      };
    },
    methods: {
      async submitBook() {
        this.book.tags = this.tagsInput.split(",").map((tag) => tag.trim());
        try {
          const response = await fetch("http://localhost:5000/api/books", {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(this.book),
          });
          if (response.ok) {
            alert("Book added successfully!");
            this.$router.push("/");
          } else {
            alert("Failed to add book.");
          }
        } catch (error) {
          console.error("Error adding book:", error);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .add-book {
    max-width: 600px;
    margin: auto;
    padding: 1rem;
    background-color: #f9f9f9;
    border: 1px solid #ddd;
    border-radius: 8px;
  }
  label {
    display: block;
    margin-top: 10px;
  }
  input,
  textarea {
    width: 100%;
    margin-bottom: 10px;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  button {
    padding: 10px 20px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  button:hover {
    background-color: #0056b3;
  }
  </style>
  