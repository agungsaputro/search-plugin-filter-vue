<template>
  <div id="app">
    <Header/>
    <Search v-model="searchQuery" v-on:change="filteredResources" />
    <FlashMessage :position="'right top'"></FlashMessage>
    <div class="container mx-auto">
      <selected-item  :data="selectedItem" v-model="removeButton" v-on:click="removeItem"/>
    </div>
    <hr />
    <div class="container mx-auto">
    <item :data="searchItem" :loading="loading" v-model="addButton" v-on:click="addItem" />
    </div>
  </div>
</template>

<script>
import data from './dummy/data.js'
import Header from './components/Header.vue'
import Search from './components/Search.vue'
import Item from './components/Item.vue'
import SelectedItem from './components/SelectedItem.vue'


export default {
  name: 'App',
  components: {
    Header,
    Search,
    Item,
    SelectedItem
  },
  data() {
    return {
      loading: "",
      resources: data,
      searchItem: [],
      searchQuery: "",
      addButton: "",
      removeButton: "",
      selectedItem: [],
    };
  },
  methods: {
    addItem: function() {
      this.selectedItem.push(this.addButton);
      this.flashMessage.success({
        title: 'Success Add Item to cart',
        message: 'Hoorah, your selected item'
      });
      this.searchItem = this.searchItem.filter((data) => data.id != this.addButton.id);
      this.resources = this.resources.filter(
        (data) => data.id != this.addButton.id
      );
  },
  removeItem: function() {
      this.resources.push(this.addButton);
      this.searchItem.push(this.removeButton);
      this.flashMessage.info({
        title: 'Are you sure ?',
        message: 'you removed item'
      });
      this.selectedItem = this.selectedItem.filter(
        (data) => data.id != this.removeButton.id
      );
  },
  filteredResources: async function() {
      this.loading = true;
      if (this.searchQuery.length >= 3) {
        this.searchItem = [];
        await this.wait(1000);
        this.searchItem = this.resources.filter(
          (data) => data.title.indexOf(this.searchQuery) != -1
        );
        this.searchItem = this.searchItem.filter((data) => data);
      } else {
        this.searchItem = this.resources;
      }
      this.loading = false;
    },
    wait: async function(ms) {
      return new Promise((resolve) => setTimeout(resolve, ms));
    },
  },
  created() {
    this.filteredResources();
  },
}
</script>