<template>
  <div>
    <el-container>
      <el-main v-loading.fullscreen.lock="isLoading">
        <!-- 検索フォーム -->
        <search />
        <!-- 検索結果一覧 -->
        <search-result />
      </el-main>
    </el-container>
  </div>
</template>

<script lang="babel">
import {mapState} from 'vuex'
import SearchResult from '~/components/searchResult.vue'
import Search from '~/components/search.vue'

export default {
  layout: 'navbar',
  components: {
    Search,
    SearchResult
  },
  computed: mapState(['isLoading']),
  fetch ({store}) {
    store.dispatch('getItems',{
      keyword: 'nuxt.js'
    })
  }
}
</script>

<style>
.el-main {
  background-color: #fff;
}
</style>
