<template>
    <div id="app" class="font-sans text-gray-800">
      <!-- Header dengan navigasi -->
      <header class="bg-green-600 text-white py-4">
        <nav>
          <ul class="flex justify-center space-x-8">
            <li>
              <router-link
                to="/"
                class="hover:text-gray-300"
                active-class="underline font-bold"
              >
                Home
              </router-link>
            </li>
            <li>
              <router-link
                to="/add"
                class="hover:text-gray-300"
                active-class="underline font-bold"
              >
                Add Book
              </router-link>
            </li>
          </ul>
        </nav>
      </header>
  
      <!-- Konten utama -->
      <main class="container mx-auto p-6">
        <router-view />
      </main>
    </div>
  </template>
  
  <script lang="ts">
  export default {
    name: "App",
  };
  </script>
  
  <style>
  /* Kosong karena semua styling menggunakan Tailwind CSS */
  </style>
  