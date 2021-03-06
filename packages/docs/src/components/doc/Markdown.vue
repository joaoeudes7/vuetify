<script>
  // Utilities
  import marked from 'marked'
  import { parseLink } from '@/util/helpers'
  // Utilities
  import {
    mapGetters,
    mapState,
  } from 'vuex'

  export default {
    props: {
      code: {
        type: [Array, String],
        default: '',
      },
      source: {
        type: String,
        default: '',
      },
      tag: {
        type: String,
        default: 'div',
      },
    },

    computed: {
      ...mapGetters('documentation', [
        'namespace',
        'page',
      ]),
      ...mapState('route', ['params']),
    },

    render (h) {
      let code = this.code || this.source

      if (!this.code) {
        if (this.$slots.default) {
          code = this.$slots.default[0].text.trim()
        }

        if (code.indexOf('.') > -1) {
          code = this.$t(code)
        } else if (
          this.namespace &&
          this.page
        ) {
          code = this.$t(
            `${this.namespace}.${this.page}.${code}`
          )
        }
      }

      // Probably wants to make a list
      const wantsList = Array.isArray(code)

      if (wantsList) {
        code = code.map(c => `- ${c}\n`).join('')
      }

      // Convert markdown links
      code = code.replace(/\[([^\]]*)\]\(([^)]*)\)/g, parseLink)

      return h(this.tag, {
        staticClass: 'markdown',
        class: {
          'mb-6': wantsList,
        },
        domProps: { innerHTML: marked(code) },
      })
    },
  }
</script>

<style lang="sass">
.markdown:last-child p,
.markdown:last-child
  margin-bottom: 0 !important

.markdown--link
  text-decoration: none

  &:hover
    opacity: 0.8

  .v-icon
    font-size: 14px
    margin-left: 4px
    vertical-align: baseline

.markdown > h4
  margin: 8px 0
</style>
