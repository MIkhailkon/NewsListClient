<template>
  <div class="main">
    <div class="news-list" v-for="oneNews in paginatedData" :key="oneNews.id">
      <news-card>
        <template v-slot:text>
          {{ oneNews.text }}
        </template>
        <template v-slot:author>
          {{ oneNews.author }}
        </template>

        <template v-slot:tag>
          <div class="tag" v-for="tag in oneNews.tags" :key="tag.id">
            #{{ tag.name }}
          </div>
        </template>
        <template v-slot:created>
          {{ oneNews.created_at }}
        </template>
      </news-card>
    </div>
    <div class="buttons">
      <button @click="prevPage" :disabled="pageNumber===0">
        Previous
      </button>
      <button @click="nextPage" :disabled="pageNumber >= pageCount -1">
        Next
      </button>
    </div>
  </div>
</template>

<script>
import NewsCard from './NewsCard'
import axios from 'axios'

export default {
  name: 'NewsList.vue',
  components: {NewsCard},
  data () {
    return {
      pageNumber: 0,
      size: 10,
      listData: []
    }
  },
  computed: {
    pageCount () {
      const l = this.listData.length
      const s = this.size
      return Math.ceil(l / s)
    },
    paginatedData () {
      const start = this.pageNumber * this.size
      const end = start + this.size
      return this.listData.slice(start, end)
    }
  },
  methods: {
    getData: async function () {
      const news = await axios.get('http://127.0.0.1:8000/api/news')
      return news.data
    },
    nextPage: function () {
      this.pageNumber++
    },
    prevPage: function () {
      this.pageNumber--
    }
  },
  async mounted () {
    this.listData = await this.getData()
  }
}
</script>

<style scoped>
.main {
  width: 100%;
  margin-right: auto;
  margin-left: auto;
  padding-top: 3rem;
  padding-bottom: 3rem;
}

@media (min-width: 992px) {
  .main {
    max-width: 820px;
  }
}
@media (min-width: 992px) {
  .main {
    max-width: 960px;
  }
}
@media (min-width: 768px) {
  .main {
    max-width: 720px;
  }
}
@media (min-width: 576px) {
  .main {
    max-width: 540px;
  }
}

button {
  padding: 5px 10px;
  margin: 5px;
  background-color: unset;
  border: solid 2px #333;
}

.tag {
  margin-right: 10px;
}

.news-list {
  background-color: #f8f9fa;
  padding: 1.5rem;
  margin-bottom: 2em;
}

@media (min-width: 425px) {
  .news-list {
    padding: 1.5em 3em;
  }

  .buttons {
    display: flex;
    justify-content: center;
  }
}
</style>
