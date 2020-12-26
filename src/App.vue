<template>
  <div id="App" class="flex container h-screen w-full">
    <!-- SIDE NAVBAR -->
    <div
      class="lg:w-1/5 border-r border-lighter px-2 lg:px-6 py-2 flex flex-col justify-between"
    >
      <div>
        <!-- TWITTER ICON -->
        <button
          class="h-12 w-12 mb-1 ml-2 hover:bg-lightblue text-3xl rounded-full text-blue focus:outline-none"
        >
          <i class="fab fa-twitter"></i>
        </button>
        <!-- LIST IN NAVBAR -->
        <div>
          <button
            v-for="(tab, index) in tabs"
            :key="index"
            @click="id = tab.id"
            :class="`focus:outline-none hover:text-blue flex items-center py-1 px-4 hover:bg-light-blue rounded-full mr-auto mb-2 ${
              id == tab.id ? 'text-blue' : ''
            }`"
          >
            <!-- ICONS -->
            <i :class="`${tab.icon} text-2xl mr-4 text-left`"></i>
            <!-- TITLE -->
            <p
              :id="tab.id"
              class="text-lg font-semibold text-left hidden lg:block"
            >
              {{ tab.title }}
            </p>
          </button>
        </div>
        <button
          class="text-white bg-blue rounded-full font-semibold focus:outline-none w-12 h-12 lg:h-auto lg:w-full p-3 hover:bg-darkblue"
        >
          <p class="hidden lg:block">Tweet</p>
          <i class="fas fa-plus lg:hidden"></i>
        </button>
      </div>
      <!-- USER SECTION-->
      <div class="lg:w-full relative">
        <button
          @click="dropDown = !dropDown"
          class="flex items-center w-full hover:bg-lightblue focus:outline-none rounded-full p-2"
        >
          <img
            src="img/profile.jpg"
            class="w-10 h-10 rounded-full border border-lighter"
          />
          <div class="ml-4 text-left hidden lg:block">
            <p class="text-sm font-bold leading-tight">Daffa Zaky</p>
            <p class="text-sm leading-tight text-dark">@daffaz</p>
          </div>
          <i class="fas fa-angle-down ml-auto text-lg hidden lg:block"></i>
        </button>
        <!-- THE DROPDOWN MENU MODAL -->
        <div
          v-if="dropDown"
          class="absolute bottom-0 left-0 w-64 rounded-lg shadow-md border-lightest bg-white mb-16"
        >
          <button
            @click="dropDown = !dropDown"
            class="p-3 flex items-center w-full hover:bg-lightest focus:outline-none rounded-lg"
          >
            <img
              src="img/profile.jpg"
              class="w-10 h-10 rounded-full border border-lighter"
            />
            <div class="ml-4 text-left">
              <p class="text-sm font-bold leading-tight">Daffa Zaky</p>
              <p class="text-sm leading-tight">@daffaz</p>
            </div>
            <i class="fas fa-check ml-auto text-blue"></i>
          </button>
          <button
            @click="dropDown = !dropDown"
            class="w-full text-left hover:bg-lightest border-t border-lighter focus:outline-none p-3 text-sm"
          >
            Add an existing account
          </button>
          <button
            @click="dropDown = !dropDown"
            class="w-full text-left hover:bg-lightest border-t border-lighter focus:outline-none p-3 text-sm"
          >
            Log out @daffaz
          </button>
        </div>
        <!-- END OF DROPDOWN MODAL -->
      </div>
      <!-- END OF BUTTON TWEET SECTION -->
    </div>
    <!-- TWEETS -->
    <div class="w-1/2 h-full overflow-y-auto">
      <div
        class="px-5 py-3 border-b border-lighter flex items-center justify-between"
      >
        <h1 class="text-xl font-bold">Home</h1>
        <i class="far fa-star text-xl text-blue"></i>
      </div>
      <div class="px-5 py-3 border-b-8 border-lighter flex">
        <div>
          <img
            src="img/profile.jpg"
            class="w-12 h-12 rounded-full border border-lighter"
          />
        </div>
        <form action="" class="w-full px-4 relative">
          <textarea
            placeholder="What's up"
            class="w-full focus:outline-none"
          ></textarea>
          <div class="flex items-center">
            <i class="text-lg text-blue mr-4 far fa-image"></i>
            <i class="text-lg text-blue mr-4 fas fa-film"></i>
            <i class="text-lg text-blue mr-4 far fa-chart-bar"></i>
            <i class="text-lg text-blue mr-4 far fa-smile"></i>
          </div>
          <button class="h-10 px-4 text-white font-semibold bg-blue hover:bg-darkblue focus:outline-none rounded-full absolute right-0 bottom-0">Tweet</button>
        </form>
      </div>
    </div>
    <!-- TRENDING -->
    <div
      class="md:block hidden w-1/3 h-full border-l py-2 px-6 overflow-y-auto relative"
    >
      <!-- TRENDING -->
      <input
        class="rounded-full w-full p-2 pl-12 bg-lighter text-sm focus:outline-none text-gray-600"
        placeholder="Search Twitter"
        type="text"
      />
      <i
        class="fas fa-search absolute left-0 top-0 mt-4 ml-12 text-sm text-light"
      ></i>
      <!-- TRENDS -->
      <div class="mt-3 w-full rounded-lg border bg-lightest">
        <div class="flex items-center p-3 justify-between">
          <p class="text-lg font-bold">Trends for you</p>
          <i class="fas fa-cog text-blue text-lg"></i>
        </div>
        <button
          v-for="trend in trending"
          :key="trend.id"
          class="w-full flex justify-between hover:bg-lighter p-3 border-t border-lighter"
        >
          <div>
            <p class="text-sm text-left leading-tight text-dark">
              {{ trend.top }}
            </p>
            <p class="font-bold text-left leading-tight my-1">
              {{ trend.title }}
            </p>
            <p class="text-left leading-tight text-dark">{{ trend.bottom }}</p>
          </div>
          <i class="fas fa-angle-down text-lg"></i>
        </button>
        <button
          class="text-blue p-3 text-left w-full hover:bg-lighter border-t border-lighter"
        >
          <a href="#">Show more</a>
        </button>
      </div>
      <!-- SUGGESTION -->
      <div class="mt-5 w-full rounded-lg border bg-lightest">
        <div class="p-3">
          <p class="text-lg font-bold">Who to follow</p>
        </div>
        <button
          v-for="friend in friends"
          :key="friend.id"
          class="w-full flex hover:bg-lighter p-3 border-t border-lighter"
        >
          <img
            :src="'img/' + friend.src"
            class="w-12 h-12 rounded-full border border-lighter"
          />
          <div class="hidden lg:block ml-4 text-left">
            <p class="text-sm font-bold leading-tight">
              {{ friend.name }}
            </p>
            <p class="text-sm leading-tight">{{ friend.handle }}</p>
          </div>
          <button
            class="ml-auto border text-sm py-1 px-4 rounded-full border-blue text-blue"
          >
            Follow
          </button>
        </button>
        <!-- SHOW MORE TEXT -->
        <button
          class="text-blue p-3 text-left w-full hover:bg-lighter border-t border-lighter"
        >
          <a href="#">Show more</a>
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
      dropDown: false,
      trending: [
        {
          top: "Trending in TX",
          title: "Gigi",
          bottom: "Trending with: Rip Gigi",
        },
        { top: "Music", title: "We Won", bottom: "135K Tweets" },
        { top: "Pop", title: "Blue Ivy", bottom: "40k tweets" },
        { top: "Trending in US", title: "Denim Day", bottom: "40k tweets" },
        { top: "Trending", title: "When Beyonce", bottom: "25.4k tweets" },
      ],
      friends: [
        { src: "elon.jpg", name: "Elon Musk", handle: "@teslaBoy" },
        { src: "monk.jpg", name: "Adrian Monk", handle: "@detective:)" },
        { src: "kevin.jpg", name: "Kevin Hart", handle: "@miniRock" },
      ],
    };
  },
};
</script>

<style>
</style>
