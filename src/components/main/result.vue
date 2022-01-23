<template>
  <div v-if="countryRes[0]">
    <div class="container">
      <div class="row my-5">
        <div class="col-lg-8 col-md-12">
          <div class="infos">
            <ul class="mb-2">
              <li class="c-name">
                {{ countryRes[0].name.common }} ({{
                  countryRes[0].name.official
                }})
              </li>
            </ul>
            <table class="table text-center table-bordered mb-2 table-responsive-sm">
              <thead>
                <tr>
                  <th scope="col">Capital</th>
                  <th scope="col">Region</th>
                  <th scope="col">Area</th>
                  <th scope="col">Population</th>
                  <th scope="col">Fifa</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td v-if="countryRes[0].capital[0]">{{ countryRes[0].capital[0] }}</td>
                  <td v-else>-</td>
                  <td v-if="countryRes[0].region">{{ countryRes[0].region }}</td>
                  <td v-else>-</td>

                  <td v-if="countryRes[0].area">{{ countryRes[0].area.toLocaleString() }} km²</td>
                  <td v-else>-</td>
                  <td v-if="countryRes[0].population">{{ countryRes[0].population.toLocaleString() }}</td>
                  <td v-else>-</td>
                  <td v-if="countryRes[0].fifa">{{ countryRes[0].fifa }}</td>
                  <td v-else>-</td>
                </tr>
              </tbody>
            </table>
            <div class="row mt-5">
              
              <div class="col-lg-3 col-md-4 col-sm-6">
                <h5>Borders</h5>
                <ul v-if="countryRes[0].borders">
                  <li
                    v-for="border in countryRes[0].borders"
                    class="c-bord"
                    :key="border"
                  >
                    {{ border }}
                  </li>
                </ul>
                <ul v-else>
                  <li>None</li>
                </ul>
                <hr>
              </div>
              <div class="col-lg-3  col-md-4  col-sm-6">
                <h5>Languages</h5>
                <ul v-if="countryRes[0].languages">
                  <li
                    v-for="language in countryRes[0].languages"
                    class="c-bord"
                    :key="language"
                  >
                    {{ language }}
                  </li>
                </ul>
                <ul v-else>
                  <li>None</li>
                </ul>
                <hr>

              </div>
              <div class="col-lg-3  col-md-4  col-sm-6">
                <h5>Currencies</h5>
                <ul v-if="countryRes[0].currencies">
                  <li
                    v-for="curr in countryRes[0].currencies"
                    class="c-bord"
                    :key="curr"
                  >
                    {{ curr.name }}
                  </li>
                </ul>
                <ul v-else>
                  <li>None</li>
                </ul>
                <hr>

              </div>
              <div class="col-lg-3   col-md-4  col-sm-6">
                <h5>Timezones</h5>
                <ul>
                  <li
                    v-for="tz in countryRes[0].timezones"
                    class="c-bord"
                    :key="tz"
                  >
                    {{ tz }}
                  </li>
                </ul>
                <hr>

              </div>
              
              <div class="col-lg-3   col-md-4  col-sm-6">
                <h5>Independent</h5>
                <ul v-if="countryRes[0].independent">
                  <li class="c-bord">
                    {{ countryRes[0].independent }}
                  </li>
                </ul>
                <ul v-else>
                  <li>None</li>
                </ul>
                <hr>

              </div>
              <div class="col-lg-3   col-md-4  col-sm-6">
                <h5>Land Locked</h5>
                <ul>
                  <li class="c-bord">
                    {{ countryRes[0].landlocked }}
                  </li>
                </ul>
                <hr>

              </div>
              <div class="col-lg-3   col-md-4  col-sm-6">
                <h5>Latitude</h5>
                <ul>
                  <li class="c-bord">
                    {{ countryRes[0].latlng[0] }}
                  </li>
                </ul>
                <hr>

              </div>
              <div class="col-lg-3   col-md-4  col-sm-6">
                <h5>Longitude</h5>
                <ul>
                  <li class="c-bord">
                    {{ countryRes[0].latlng[1] }}
                  </li>
                </ul>
                <hr>

              </div>
              
              <div class="col-lg-3   col-md-4  col-sm-6">
                <h5>Start Of Week</h5>
                <ul>
                  <li class="c-bord">
                    {{ countryRes[0].startOfWeek.toUpperCase() }}
                  </li>
                </ul>
                <hr>

              </div>
              <div class="col-lg-3   col-md-4  col-sm-6">
                <h5>Top Level Domain</h5>
               
                 <ul v-if="countryRes[0].tld">
                  <li
                    v-for="d in countryRes[0].tld"
                    class="c-bord"
                    :key="d"
                  >
                    {{ d }}
                  </li>
                </ul>
                <ul v-else>
                  <li>None</li>
                </ul>
                <hr>

              </div>
              <div class="col-lg-3   col-md-4  col-sm-6">
                <h5>Calling Code</h5>
                <ul>
                  <li class="c-bord" v-if="countryRes[0].idd.root && countryRes[0].idd.suffixes[0]">
                    {{ countryRes[0].idd.root }}{{ countryRes[0].idd.suffixes[0] }}
                  </li>
                   <li v-else-if="countryRes[0].idd.root">
                     {{ countryRes[0].idd.root }}
                  </li>
                  <li v-else>None</li>
                </ul>
                <hr>

              </div>
              <div class="col-lg-3   col-md-4  col-sm-6">
                <h5>Postal Code</h5>
                <ul>
                  <li class="c-bord" v-if="countryRes[0].postalCode">
                    {{ countryRes[0].postalCode.format }}
                  </li>
                  <li v-else>None</li>
                </ul>
                <hr>

              </div>
              
            </div>
          </div>
        </div>
        <div class="col-lg-4 col-md-6 col-sm-9">
          <div class="imgs d-flex flex-column">
            <h5 class="mb-2">Flag</h5>
            <img
              v-if="countryRes[0].flags.png"
              :src="countryRes[0].flags.png"
              class="flag rounded mb-4"
              alt="flag"
            />
            <h5 class="mb-2">Map</h5>
            <a :href="countryRes[0].maps.googleMaps">{{
              countryRes[0].maps.googleMaps
            }}</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { watch, ref } from "vue";
import { country } from "@/country.js";
export default {
  setup() {
    const countryRes = ref([]);
  // watch change country Clicked
    watch(country, (curr) => {
      countryRes.value = curr;
      console.log(countryRes.value);
    });
    // console.log(countryRes.value);
    //
     
    //
    return {
      countryRes,
    };
  },
};
</script>

<style scoped>
.flag {
  height: 200px;
}
.c-name {
  font-weight: 600;
  color: var(--primary-color);
  font-size: 1.5rem;
}
h5 {
  color: var(--primary-color);
}
hr{
  width:100%;
}
</style>