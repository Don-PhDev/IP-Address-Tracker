<template>
  <div class="flex flex-col h-screen max-h-screen">
    <div
      class="flex justify-center relative bg-hero-bg bg-cover px-4 pt-8 pb-32"
    >
      <div class="w-full max-w-screen-sm">
        <h1 class="text-white text-center text-3xl pb-4">
          IP Address Tracker
        </h1>
        <div class="flex">
          <input
            class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none"
            type="text"
            placeholder="Search for IP address or leave empty to get your IP info"
          >
          <i class="
            cursor-pointer
            bg-black text-white
            px-4 text-lg
            rounded-tr-md rounded-br-md
            flex items-center
            fas fa-chevron-right"
          ></i>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  components: {
  }
}
</script>
