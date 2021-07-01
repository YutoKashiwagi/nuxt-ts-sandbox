<template>
  <div>
    <p>hello</p>
    <p>{{ hoge }}</p>
    <div>
      <button @click="test">
        test
      </button>
    </div>
    <div>
      <p>articles</p>
      {{ articles }}
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { ThisTypedComponentOptionsWithRecordProps } from 'vue/types/options'

type Data = {
  hoge: string
  articles: any[]
}

type Methods = {
  test: () => Promise<void>
}

type Computed = {}

type Props = {}

const options: ThisTypedComponentOptionsWithRecordProps<
  Vue,
  Data,
  Methods,
  Computed,
  Props
> = {
  data () {
    return {
      hoge: 'hogehogehoge',
      articles: []
    }
  },
  methods: {
    async test () {
      try {
        const data = await this.$axios.get<any[]>('https://qiita.com/api/v2/items?page=1&per_page=20')
        console.log(data)
        this.articles = data.data
      } catch (error) {
        console.log(error)
      }
    }
  }
}

export default Vue.extend(options)
</script>
