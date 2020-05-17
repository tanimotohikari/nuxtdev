<template>
  <el-form
    ref="searchForm"
    :inline="true"
    :model="searchForm"
    :rules="rules"
    @submit.native.prevent
  >
    <el-form-item prop="keyword">
      <el-input
        v-model="searchForm.keyword"
        placeholder="search keyword"
        prefix-icon="el-icon-search"
        @keyup.enter.native="search('search')"
      />
    </el-form-item>
    <el-form-item>
      <el-button @click="search('search')">search</el-button>
    </el-form-item>
  </el-form>
</template>
<script>
export default {
  data() {
    return {
      // 検索フォーム
      searchForm: {
        keyword: ''
      },
      // バリデーション
      rules: {
        keyword: [
          { required: true, massage: 'Plase input the key', trigger: 'blur' },
          // 未入力はエラー
          // 空白のみはエラー
          { whitespase: true, massage: 'Plase input the key', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    // searchボタンをおしたら呼び出されるメドッド
    search(form) {
      this.$refs[form].validate((valid) => {
        if (!valid) {
          return false
        }
        this.sendRequest()
      })
    },
    // storeのactionに用意した getItemsを呼び出す
    sendRequest() {
      this.$store.dispatch('getItems', {
        keyword: this.search.keyword
      })
    }
  }
}
</script>

<style>
.el-form {
  margin-top: 1em;
  margin-left: 1em;
}
</style>
