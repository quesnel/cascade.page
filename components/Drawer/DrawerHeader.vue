<template>
  <div
    class="sticky bottom-6 left-4 flex flex-row items-center ml-4 z-20"
    @mousedown="mousedown"
  >
    <button
      class="
        mr-2
        text-gray-400
        hover:text-gray-300
        rounded-full
        hover:bg-gray-800
        backdrop-filter backdrop-blur
        transition
      "
      @click="toggleSidebar"
      v-if="edittable"
    >
      <svg
        class="h-5 w-5 m-1"
        focusable="false"
        viewBox="0 0 24 24"
        aria-hidden="true"
        fill="currentColor"
      >
        <path
          d="M4 18h16c.55 0 1-.45 1-1s-.45-1-1-1H4c-.55 0-1 .45-1 1s.45 1 1 1zm0-5h16c.55 0 1-.45 1-1s-.45-1-1-1H4c-.55 0-1 .45-1 1s.45 1 1 1zM3 7c0 .55.45 1 1 1h16c.55 0 1-.45 1-1s-.45-1-1-1H4c-.55 0-1 .45-1 1z"
        ></path>
      </svg>
    </button>
    <a href="/" class="rounded-full hover:bg-gray-900" v-else>
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-5 w-5 m-1"
        viewBox="0 0 20 20"
        fill="currentColor"
      >
        <path
          d="M10.707 2.293a1 1 0 00-1.414 0l-7 7a1 1 0 001.414 1.414L4 10.414V17a1 1 0 001 1h2a1 1 0 001-1v-2a1 1 0 011-1h2a1 1 0 011 1v2a1 1 0 001 1h2a1 1 0 001-1v-6.586l.293.293a1 1 0 001.414-1.414l-7-7z"
        />
      </svg>
    </a>
    <div
      class="flex flex-row p-2 backdrop-filter backdrop-blur"
      style="width: fit-content"
    >
      <a
        :href="'/' + $store.state.timelinePath"
        class="mr-4 flex items-center text-gray-300"
        v-if="$store.state.timelinePath"
      >
        @{{ $store.state.timelinePath }}
      </a>
      <display-settings></display-settings>
      <tags></tags>
      <button
        v-if="collapsible"
        class="
          ml-auto
          hover:bg-gray-500
          rounded
          px-3
          flex flex-row
          items-center
        "
        @click="$emit('input', !value)"
      >
        <span class="hidden md:block">{{ value ? "Expand" : "Collapse" }}</span
        ><svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-4 w-4 ml-1"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          v-if="!value"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M19 9l-7 7-7-7"
          />
        </svg>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-4 w-4 ml-1"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          v-if="value"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M5 15l7-7 7 7"
          />
        </svg>
      </button>
      <!-- <a
      v-else
      href="/"
      class="underline text-gray-300 hidden md:block flex-shrink-0 pl-2"
      >Make your own cascade</a
    > -->
    </div>
  </div>
</template>

<script lang="ts">
import Tags from "./Tags.vue";
import DisplaySettings from "./DisplaySettings.vue";
import Vue from "vue";

export default Vue.extend({
  components: {
    Tags,
    DisplaySettings,
  },
  props: ["value", "collapsible", "timelinePath", "edittable"],
  methods: {
    toggleSidebar() {
      this.$store.commit("sidebar/toggle");
    },
    mousedown(e: MouseEvent) {
      e.stopPropagation();
    },
  },
});
</script>

<style>
</style>