<template>
  <div class="switchableGrid">
    <div class="container">
      <!-- top bar -->
      <div class="bar">
        <div class="btnHolder">
          <button
            :class="{ barActive: layout === 'grid' }"
            @click="layout = 'grid'"
          >
            <i class="fas fa-th"></i> Grid
          </button>
          <button
            :class="{ barActive: layout === 'list' }"
            @click="layout = 'list'"
          >
            <i class="fas fa-list"></i> List
          </button>
        </div>
      </div>
      <!-- content -->
      <div class="content">
        <!-- grid view -->
        <ul v-if="layout === 'grid'" class="grid">
          <li v-for="content in contents" :key="content.id">
            <div class="image">
              <img :src="content.imageSrc" />
            </div>
          </li>
        </ul>
        <!-- list view -->
        <ul v-if="layout === 'list'" class="list">
          <li v-for="content in contents" :key="content.id">
            <img :src="content.imageSrc" />
            <div class="listContent">
              <h2>{{ content.title }}</h2>
              <p>{{ content.description }}</p>
              <a class="btn" href="#">Read more</a>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Product",
  data() {
    return {
      layout: "grid",
      contents: null,
    };
  },
  created: function () {
    axios
      .get("http://localhost:8080/demo/vue/switchable-grid/api/products.json")
      .then((res) => {
        this.contents = res.data;
      });
  },
};
</script>