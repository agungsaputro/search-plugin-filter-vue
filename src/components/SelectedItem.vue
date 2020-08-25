<template>
  <div>
    <h1 class="font-bold">Cart</h1>
    <div v-if="data.length < 1">Not Item</div>
    <div class="selected-item flex flex-wrap">
      <div
        v-for="(list, idx) in data"
        class="w-1/2 sm:w-1/3 sm:px-2"
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
            Remove
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SelectedItem",
  props: {
    test: String,
    data: {
      type: Array,
      required: true,
    },
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