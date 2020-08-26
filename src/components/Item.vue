<template>
  <div class="mt-5">
    <h1 class="font-bold">Product</h1>
    <hr />
    <!-- <div>{{ loading ? "mengetik..." : data.length>1 ? "" : "Data tidak ditemukan" }}</div> -->
    <div class="selected-item flex flex-wrap">
      <div
        v-for="(list, idx) in data"
        class="w-1/3 p-2 mx-auto"
        style="min-width:200px"
        v-bind:key="idx">
        <div class="flex">
          <div class="title">
            <span :title="list.title">{{ trim(list.title) }}</span>
          </div>
        </div>
        <div>
          <img :src="list.thumbnailUrl" class="img-box"/>
        </div>
        <div class="flex p-4">
          <div>
            <span>{{list.price | currency}}</span>
          </div>
          <button class="bg-red-600 hover:bg-red-700 text-white text-sm px-3 py-1  border rounded-full" v-on:click="addArray(list)">
            Add
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FilteredItem",
  props: {
    data: {
      type: Array,
      required: true,
    },
    loading:{
      type:Boolean
    }
  },
  model: {
    prop: "button",
    event: "click",
  },
  methods: {
    addArray(data) {
      return this.$emit("click", data);
    },
    trim: function(words, count = 15, seperator = "...") {
      if (words.length > count) words = words.slice(0, count) + seperator;
      return words;
    },
  },
};
</script>