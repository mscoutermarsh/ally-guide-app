<template>
<div>

<div>
    <input type="text" v-model="search" placeholder="Search by name or state" v-on:keyup="CheckInputContent" style="width:30%">
    <button type="button" v-on:click='FetchSearchResults()'>Search</button>
</div>

<div id="government-contact-info" v-show="searchCompleted">
    <div v-for="result in searchResults" :key="result.Name" style="width: 30%; display: inline-block;">
        <div style="border-style: dashed;">
            <p>Name: {{result.Name}}</p>
            <p>Causes: {{result.Cause}}</p>
        </div>
    </div>
</div>

<div v-show="error" style="color: red; font-weight: bolder;">
  {{ error }}
</div>

<div v-show="searchCompleted && searchResults.length == 0 && !error" style="font-weight: bolder;">
  <h1>Sorry, no results found.</h1>
</div>

<div>
<a id = "rebuild-btn" href = "https://www.rebuildblackbusiness.com/"> Rebuild Black Owned Businesses </a>
</div>
</div>


</template>

<style>
#rebuild-btn{
    
}
.container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr;
}

button.accordion {
    background-color: #000000;
    color: #eee;
    cursor: pointer;
    padding: 18px;
    width: 100%;
    text-align: left;
    border: none;
    outline: none;
    transition: 0.4s;
}

button.accordion.active, button.accordion:hover {
    background-color: #ddd;
    color: #000000;
}

div.panel {
    padding: 0 18px;
    background-color: white;
    display: none;
}

div.panel.show {
    display: block !important;
}

div.panel {
    padding: 0 18px;
    background-color: white;
    max-height: 0;
    overflow: hidden;
    transition: 0.6s ease-in-out;
    opacity: 0;
}

div.panel.show {
    opacity: 1;
    max-height: 500px; /* Whatever you like, as long as its more than the height of the content (on all screen sizes) */
}

.blm{
cursor: pointer;
  opacity: .75;
  -webkit-transition-duration: 0.4s; /* Safari */
  transition-duration: 0.4s;

}

a.blm:hover {
  box-shadow: 0 12px 16px 0 rgba(0,0,0,0.24), 0 17px 50px 0 rgba(0,0,0,0.19);
  opacity: 1;
}

</style>

<script>

export default {
  data () {
    return{
      search:'',
      searchCompleted: false,
      searchResults: [],
      error: '',
    }
  },
  methods: {
    CheckInputContent: function () {

    },
    ToggleMessageUI: function (result) {

    },
  },
  computed: {

  },
  created() {
      this.congressMembers = [];

      this.$http.get(
          'http://localhost:5000/api/contribute/'
      ).then(response => {
        this.searchResults = response;
        console.log(this.searchResults)
      }, response => {
          // error callback
      });
  }
}

</script>
