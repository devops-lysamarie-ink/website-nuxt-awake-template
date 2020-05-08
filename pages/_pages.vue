<template>
  <div id="post-page" class="page-wrapper post-page">

    <main-section :one-column-constrained="true">
      <template v-slot:default>
        <div class="post-wrapper">
          <markdown :markdown="$store.state.content" />
        </div>
      </template>
    </main-section>
  </div>
</template>
<script>
import { mapState } from 'vuex'
import { setPageData, getFormattedDate } from '../helper'
// import 'highlight.js/styles/github.css'
import Markdown from '~/components/Markdown'
export default {
  components: {
    Markdown
  },
  computed: {
    ...mapState([
      'title',
      'subtitle',
      'content',
      'featuredImage',
      'seoDescription',
      'seoMetaImage',
      'slug'
    ]),
    url() {
      return `${process.env.URL}/${this.$route.fullPath}`
    }
  },
  fetch({ store, params }) {
    setPageData(store, { resource: 'pages', slug: params.pages })
  }
}
</script>
<style scoped lang="scss">
.edit-post {
  margin-bottom: 20px;
}
</style>
