<template>
  <div class="nudify-editor">
    <div ref="imageEditor" class="editor" data-private />
  </div>
</template>

<script>
import { tutorial } from '~/modules'

export default {
  computed: {
    photo() {
      return this.$parent.photo
    },
  },

  mounted() {
    this.create()
    tutorial.editor()
  },

  methods: {
    /**
     *
     */
    async create() {
      const ImageEditor = require('tui-image-editor')
      const { blackTheme } = require('~/modules/editor.theme')

      this.photo.editor = new ImageEditor(this.$refs.imageEditor, {
        includeUI: {
          loadImage: {
            path: this.photo.file.path,
            name: this.photo.file.name,
          },
          theme: blackTheme,
          initMenu: 'draw',
          menu: ['draw', 'shape', 'flip', 'rotate', 'filter', 'mask'],
        },
        usageStatistics: false,
      })
    },
  },
}
</script>

<style lang="scss" scoped>
.nudify-editor {
  @apply h-full;
}

.editor {
  @apply w-full h-full;
}
</style>

<style lang="scss">
.tui-image-editor-control {
  @apply bg-dark-600;
}
</style>
