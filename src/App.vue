<template>
  <div id="App" class="flex container h-screen w-full">
    <!-- SIDE NAVBAR -->
    <div
      class="w-1/5 border-r border-lighter px-8 py-2 flex flex-col justify-between"
    >
      <div>
        <!-- TWITTER ICON -->
        <button
          class="h-12 w-12 hover:bg-lightblue text-3xl rounded-full text-blue"
        >
          <i class="fab fa-twitter"></i>
        </button>
        <!-- LIST IN NAVBAR -->
        <div>
          <button
            v-for="(tab, index) in tabs"
            :key="index"
            @click="id = tab.id"
            :class="`focus:outline-none hover:text-blue flex items-center py-2 px-4 hover:bg-light-blue rounded-full mr-auto mb-3 ${
              id === tab.id ? 'text-blue' : ''
            }`"
          >
            <!-- ICONS -->
            <i :class="`${tab.icon} text-2xl mr-4 text-left`"></i>
            <!-- TITLE -->
            <p :id="tab.id" class="text-lg font-semibold text-left">
              {{ tab.title }}
            </p>
          </button>
        </div>
        <button
          class="text-white bg-blue rounded-full font-semibold focus:outline-none w-full p-3 hover:bg-darkblue"
        >
          Tweet
        </button>
      </div>
      <!-- BUTTON TWEET -->
      <div class="w-full">
        <button
          class="flex items-center w-full hover:bg-lightest rounded-full p-2"
        >
          <img
            src="img/profile.png"
            class="w-12 h-12 rounded-full border border-lighter"
          />
          <div class="ml-4 text-left">
            <p class="text-sm font-bold leading-tight">Daffa Zaky</p>
            <p class="text-sm leading-tight">@daffaz</p>
          </div>
          <i class="fas fa-angle-down ml-auto text-lg"></i>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data: function () {
    return {
      tabs: [
        { icon: "fas fa-home", title: "Home", id: "home" },
        { icon: "fas fa-hashtag", title: "Explore", id: "explore" },
        { icon: "far fa-bell", title: "Notifications", id: "notifications" },
        { icon: "far fa-envelope", title: "Messages", id: "messages" },
        { icon: "far fa-bookmark", title: "Bookmarks", id: "bookmarks" },
        { icon: "fas fa-clipboard-list", title: "Lists", id: "lists" },
        { icon: "far fa-user", title: "Profile", id: "profile" },
        { icon: "fas fa-ellipsis-h", title: "More", id: "more" },
      ],
      id: "home",
    };
  },
  components: {},
};
</script>

<style>
</style>
