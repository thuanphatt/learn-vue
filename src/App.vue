<template>
  <div class="container mx-auto px-60">
    <h1 class="text-3xl font-bold text-center my-8">Github search</h1>

    <div class="mb-3">
      <div class="relative mb-4 flex w-full flex-wrap items-stretch">
        <input
          v-model="username"
          @keyup.enter="handleSearch"
          type="search"
          class="relative m-0 -mr-0.5 block w-[1px] min-w-0 flex-auto rounded-l border border-solid border-neutral-300 bg-transparent bg-clip-padding px-3 py-[0.25rem] text-base font-normal leading-[1.6] text-neutral-700 outline-none transition duration-200 ease-in-out focus:z-[3] focus:border-primary focus:text-neutral-700 focus:shadow-[inset_0_0_0_1px_rgb(59,113,202)] focus:outline-none dark:border-neutral-600 dark:text-neutral-200 dark:placeholder:text-neutral-200 dark:focus:border-primary"
          placeholder="Search"
          aria-label="Search"
          aria-describedby="button-addon1"
        />

        <!--Search button-->
        <button
          @click="handleSearch"
          class="relative z-[2] flex items-center rounded-r bg-blue-900 px-6 py-2.5 text-xs font-medium uppercase leading-tight text-white shadow-md transition duration-150 ease-in-out hover:bg-primary-700 hover:shadow-lg focus:bg-primary-700 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-primary-800 active:shadow-lg"
          type="button"
          id="button-addon1"
          data-te-ripple-init
          data-te-ripple-color="light"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 20 20"
            fill="currentColor"
            class="h-5 w-5"
          >
            <path
              fill-rule="evenodd"
              d="M9 3.5a5.5 5.5 0 100 11 5.5 5.5 0 000-11zM2 9a7 7 0 1112.452 4.391l3.328 3.329a.75.75 0 11-1.06 1.06l-3.329-3.328A7 7 0 012 9z"
              clip-rule="evenodd"
            />
          </svg>
        </button>
      </div>
    </div>
    <div v-if="user">
      <h2>Username:{{ user.login }}</h2>

      <img :src="user.avatar_url" alt="User avatar" />
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      username: "",
      user: null,
    };
  },
  methods: {
    async handleSearch() {
      try {
        const response = await axios.get(
          `https://api.github.com/users/${this.username}`
        );
        this.user = response.data;
        console.log("response.data: ", response.data);
        this.username = response.data.login;
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>
