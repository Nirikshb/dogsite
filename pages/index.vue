<template>
  <div>

    <searchBox
      :search-dog="searchDog"
      :warning-shot="warningShot"
      @searching="handleSearching"
    />

    <dogBox 
    :dog-data="dogData" 
    :warning-shot="warningShot" 
    @fetchMore="fetchMore" />

  </div>
</template>

<script>
import searchBox from "~/components/searchBox.vue";
import dogBox from "~/components/dogBox.vue";

export default {
  components: {
    searchBox,
    dogBox,
  },

  data() {
    return {
      dogData: null,
      searchDog: "",
      warningShot: "",
      limit: 12,
      page: 1,
    };
  },

  mounted() {
    this.fetchDogs();
  },

  methods: {
    async fetchDogs() {
      try {
        const response = await this.$axios.get(
          `https://api.thedogapi.com/v1/breeds?limit=12&page=${this.page}`
        );
        // Check if dogData property is not yet initialized
        if (!this.dogData) {
          // Initialize an empty array for dog data
          this.dogData = [];
          console.log(this.dogData, "empty check");
        }

        // Check if the response data has no elements (empty array)
        if (response.data.length === 0) {
          // Set a warning message indicating no more data to fetch
          this.warningShot = "No more data to fetch.";
          console.log("warningshot error", this.warningShot);

        } else {
          // If response data has content, using spread operater we add more
          this.dogData.push(...response.data);
          console.log("data push from api", this.dogData);

        }
      } catch (error) {
        console.log("main error", error);
        
      }
    },
    handleSearching(dogData) {
      // on initialization setting page 1
      // fetching the data, setting our search for the data from the api
      this.page = 1;
      this.fetchDogs();
      this.searchDog = dogData;
    },
    fetchMore() {
      // increment pages as data is being fetched
      this.page++;
      this.fetchDogs();
    },
  },
};
</script>
