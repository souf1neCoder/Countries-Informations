<template>
  <div class="content-side">
    <div class="box_search">
      <input
        type="search"
        v-model="search"
        class="form-control"
        placeholder="Search Country..."
      />
    </div>
    <div class="list_countries">
      <ul>
        <li
        
          v-for="c in searchCountries"
          class="link text-center"
          :class="c.name.common === 'Morocco' ? 'active' : ''"
          :key="c.name.common"
          @click="getCountry(c.name.common,$event)"
        >
          {{ c.name.common }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
//
import http from "@/http-common.js";
import { ref, computed } from "vue";
import { country } from "@/country.js";
//
export default {
  setup() {
    //countries that not responded to request 
    const toRemove = ['Antarctica','Aruba','Bouvet Island','China','Macau','Dominica','Heard Island and McDonald Islands','Kosovo','United States Minor Outlying Islands','Western Sahara'];
    //searchCountries
    let searchCountries;
    //search Input
    let search = ref("");
    // countries
    let countries = ref([]);
    // get countries
    async function getCountries() {
      const res = await http.get("/all").catch(function (error) {
        if (error.res) {
          // Request made ande server respodes
          console.log(error.res.data);
          console.log(error.res.status);
          console.log(error.res.headers);
          return;
        } else if (error.request) {
          // Request was made but no response
          console.log(error.request);
          return;
        } else {
          // Something happened in setting up the request that triggered an error
          console.log("Error", error.message);
          return;
        }
      });
      countries.value = res.data;
      //remove countries that not responded to request
       countries.value = countries.value.filter(function(c){
         return !toRemove.includes(c.name.common);
       })
      // console.log(countries.value);
    }

    //get one Country Clicked
    async function getCountry(name,event) {
      const res = await http.get(`/name/${name}`);
      country.value = res.data;
      // console.log(country.value[0]);
      removeActivesLinks();
      event.target.classList.add('active');
      const side = document.querySelector(".side");
      const bar = document.querySelector(".open_search");
      const main = document.querySelector(".main");
      side.classList.toggle("active");
      bar.classList.toggle("active");
      main.classList.toggle("active");
      document.title = name;
    }
    //get morocco country
     //get one Country Clicked
    async function getCountryMorocco(){
      const res = await http.get(`/name/morocco`);
      country.value = res.data;
      // console.log(country.value[0]);
    }
    // Call get Countries
    getCountries();
    getCountryMorocco();
    //Filter Countries By Search Box And Sort
    searchCountries = computed(() => {
      return countries.value.filter((c) => {
        return c.name.common.toLowerCase().match(search.value.toLowerCase());
      }).sort((a,b)=>(a.name.common > b.name.common) ? 1 : -1);
    });
    //remove Active Classes from Li
    function removeActivesLinks(){
        const links = document.querySelector(".list_countries ul");
      
      [...links.children].forEach((link) => {
        link.classList.remove("active");
      });
    }
    //
  
    // console.log(searchCountries);
    // Return Object
    return {
      searchCountries,
      countries,
      search,
      getCountry,
      country,
    };
  },
};
</script>

<style>
.content-side {
  padding: 10px;
}
.box_search {
  margin-bottom: 0.8rem;
}
.link {
  padding: 3px;
  width: 100%;
  color: var(--dark-color);
  transition: 0.3s ease-in-out all;
  cursor: pointer;
  border-bottom:1px solid #ccc;
}
.list_countries ul:first-child{
  border-top:1px solid #ccc;

}

.link:hover,
.link.active {
  background-color: var(--primary-color);
  color:#fff;
}
</style>