<template>
  <div class="search-nav-bar">
    <van-icon
      size="16"
      name="arrow-left"
      style="padding: 12px 0 12px 12px"
      @click="$router.back()"
    />
    <van-search
      v-model="keyword"
      shape="round"
      style="width: 100%"
      :placeholder="defaultSearch"
      show-action
      clearable
      autofocus
      @focus="onFocus"
      @search="onSearch"
      @cancel="onCancel"
    >
      <template #action>
        <div @click="onSearch">搜索</div>
      </template>
    </van-search>
  </div>
</template>

<script>
import variables from '@/styles/variables.scss'

export default {
  props: {
    value: {
      type: String,
      default: ''
    },
    defaultSearch: {
      type: String,
      default: ''
    }
  },
  computed: {
    variables() {
      return variables
    },
    keyword: {
      get() {
        return this.value
      },
      set(val) {
        this.$emit('input', val)
      }
    }
  },
  // watch: {
  //   defaultSearch(val1, val2) {
  //   }
  // },
  methods: {
    onFocus() {
      this.$emit('handleFocus')
    },
    onSearch() {
      const key = this.keyword.trim() || this.defaultSearch.trim()
      if (!key) {
        this.$toast('请输入要搜索内容')
        return
      }
      this.$store.dispatch('search/setKey', key)
      this.$emit('handleSearch', key)
    },
    onCancel() {
      this.value = ''
      this.$router.back()
    }
  }
}
</script>

<style lang="scss" scoped>
.search-nav-bar {
  display: flex;
  align-items: center;
}
</style>
