<template>
  <div class="container">
      <div v-for="article in info.results" v-bind:key="article.url" id="articles" class="card my-3 ">
        <div class="row g-0">
          <div class="col-md-4">
            <img :src="imageIfExists(article)" class="img-fluid rounded-start" alt="image">
          </div>
          <div class="col-md-8">
            <div class="card-body">
              <!-- start title-->
              <h5 class="card-title">
                {{ article.title }}
              </h5>
              <!-- end title-->

              <!-- start category-->

              <span
                  v-if="article.category !== null"
                  class="badge rounded-pill bg-primary"
              >
                  {{ article.category.title }}
                  </span>
              <!-- end category-->

              <!-- start tags-->
              <span v-for="tag in article.tags" v-bind:key="tag" class="badge rounded-pill bg-secondary">
                {{ tag }}
              </span>
              <!-- end tags-->

              <div class="d-flex align-items-center justify-content-between" id="card_bottom">
                <!-- start created time-->
                <div>
                  <div>This Article is posted at: {{ formatted_time(article.created) }}</div>
                </div>
                <!-- end created time-->
                <router-link
                  :to="{ name: 'ArticleDetail', params: { id: article.id }}"
                  class="btn btn-light"
                >
                  Learn More
                </router-link>
              </div>

            </div>
          </div>
        </div>
      </div>
  </div>


  <div id="paginator">
        <span v-if="is_page_exists('previous')">
            <router-link :to="get_path('previous')">
                Prev
            </router-link>
        </span>
    <span class="current-page">
            {{ get_page_param('current') }}
        </span>
    <span v-if="is_page_exists('next')">
            <router-link :to="get_path('next')">
                Next
            </router-link>
        </span>
  </div>

</template>

<script>
// import axios from 'axios';

import {ref} from 'vue'
import {useRoute} from 'vue-router'
import getArticleData from '@/composables/getArticleData.js'
import pagination from '@/composables/pagination.js'
import articleGrid from '@/composables/articleGrid.js'
import formattedTime from '@/composables/formattedTime.js'

export default {
  name: 'ArticleList',

  setup() {
    const info = ref('');
    const route = useRoute();

    const kwargs = ref({page: 0, searchText: ''});
    getArticleData(info, route, kwargs);

    const {
      is_page_exists,
      get_page_param,
      get_path
    } = pagination(info, route);

    const {
      imageIfExists,
      gridStyle
    } = articleGrid();

    const formatted_time = formattedTime;

    return {
      info,
      is_page_exists,
      get_page_param,
      get_path,
      imageIfExists,
      gridStyle,
      formatted_time,
    }
  },
}

</script>

<style scoped>

#paginator {
  text-align: center;
  padding-top: 50px;
}

.current-page {
  font-size: x-large;
  font-weight: bold;
  padding-left: 10px;
  padding-right: 10px;
}

/*define the size of img in card*/
.img-fluid {
  width: 100%;
  height: 15vw;
  object-fit: cover;
}

/*start hover effect*/
.card{
  border-radius: 4px;
  background: #fff;
  box-shadow: 0 6px 10px rgba(0,0,0,.08), 0 0 6px rgba(0,0,0,.05);
  transition: .3s transform cubic-bezier(.155,1.105,.295,1.12),.3s box-shadow,.3s -webkit-transform cubic-bezier(.155,1.105,.295,1.12);
  cursor: pointer;
}

.card:hover{
  transform: scale(1.05);
  box-shadow: 0 10px 20px rgba(0,0,0,.12), 0 4px 8px rgba(0,0,0,.06);
}
/*end hover effect*/
</style>
