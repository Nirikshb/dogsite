<template>
  <b-container>
    <hr />
    <div class="containData">
      
      <div v-for="dog in dogData" :key="dog.id">
        <div class="dataCenter">
          <img
            width="251"
            height="251"
            src="perfect2.jpg"
            onmouseover="this.src='newdog.jpg'"
            onmouseout="this.src='perfect2.jpg'"
          />
        
          <div class="data">
            <div>
              <b>Dog ID : </b> {{ dog.id }}
            </div>
            <div>
              <b>Name : </b> {{ dog.name }}</div>
            <div>
              <b>Breed Group :</b> {{ dog.breed_group }}</div>
            <div>
              <b>Height : </b> {{ dog.height.metric }}</div>
            <div>
              <b>Weight : </b> {{ dog.weight.metric }}</div>
            <div>
              <b>Life Span :</b> {{ dog.life_span }}</div>
          </div>

          <hr />
        </div>
      </div>
    </div>
    <div v-if="warningShot">
      {{ warningShot }}
    </div>
    
    <button 
        v-if="!warningShot && canFetchMore" 
        class="button" 
        @click="moreDogs">
        Show more 
        ({{ dogDataLength }} dogs)
    </button>
  </b-container>
</template>

<script>
export default {
  props: {
    dogData: {
      type: Array,
      default: Array,
    },
    warningShot: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      canFetchMore: true,
    };
  },
  computed: {
    dogDataLength() {
      return this.dogData ? this.dogData.length : 0;
    },
  },
  methods: {
    moreDogs() {
      this.$emit("fetchMore");
    },
  },
};
</script>

<style>
body {
  font-family: "Poppins";
  background-color: rgb(255, 255, 255);
}

h1 {
  font-family: "Sedan SC";
}

.dataCenter {
  margin-left: 0.5rem !important;
  margin-right: 0.5rem !important;
  margin-bottom: 10px;
  border: 1px solid transparent;
}

.containData {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.dataCenter:hover {
  border: 1px solid #b1b1b1;
}

.data {
  max-width: 210px;
}

button {
  margin-bottom: 10px;
}

img {
  height: auto;
}

.button {
  width: 100%;
  padding: 0.5rem 1rem;
  border: 1px solid #007bff;
  background-color: transparent;
  color: #007bff;
  text-align: center;
  cursor: pointer;
  font-size: 1.1rem;
  font-weight: 400;
  border-radius: 0.25rem;
  transition: background-color 0.15s ease-in-out, border-color 0.15s ease-in-out,
    color 0.15s ease-in-out;
}

.button:hover {
  background-color: #007bff;
  color: #fff;
}

.button:active {
  background-color: #0056b3;
  border-color: #0056b3;
}

@media screen and (max-width: 600px) {
  .containData {
    align-items: center;
    justify-content: center;
  }
}
</style>
