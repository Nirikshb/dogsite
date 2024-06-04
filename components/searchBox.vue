<template>
    <b-container>

      <h1 class="text-center">Hey Welcome to doggy site</h1>

      <b-form-input 
            v-model="searchDog" 
            type="text" 
            placeholder="Enter Dog Name" 
            @change="dogChange">
      </b-form-input>

      <span 
            v-if="warningShot">
            {{ warningShot }}
      </span>
    </b-container>
  </template>
  
  <script>
  export default {
    props: {
      // This prop receives a string value from the parent component,  indicate search mode
      searching: {
        type: String,
        default: ''
      },
      // This prop receives a string value from the parent component,  display a warning message
      warningShot: {
        type: String,
        default: ''
      },
    },
    data() {
      return {
        // This variable stores the user's input for searching dog names
        searchDog: '',
        // Commented out for now, potential variable to control loading state
        // loadAll: false
      }
    },
    methods: {
      dogChange() {
        // This function emits the 'searching' event with the current searchDog value
        // This allows the parent component to react to the search term change
        this.$emit('searching', this.searchDog)
        console.log(this.searchDog, "in searchBox Emit"); // Logs the search term for debugging purposes
      }
    }
  }
  </script>
  