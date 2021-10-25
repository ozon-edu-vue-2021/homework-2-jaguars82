<template>
  <div>
    <directory-item
      :itemData="{ name: content.name, path: path }"
      @toggle="childIsVisible = !childIsVisible"
    />

    <div v-if="childIsVisible">
      <div
        v-for="(item, i) in content.contents"
        :key="`${item.name}-${i}`"
        :style="{ paddingLeft: `${indentSize}px` }"
      >
        
        <file-item
          v-if="item.type === 'file'"
          :itemData="{ name: item.name, path: `${path}${content.name}\\${item.name}` }"
        />
        <link-item
          v-if="item.type === 'link'"
          :itemData="{ name: item.name, path: `${path}${content.name}\\${item.name}` }"
        />

        <branch
          v-if="item.type === 'directory'"
          :path="`${path}${content.name}\\`"
          :content="item"
        />

      </div>
    </div>
  </div>
</template>

<script>
import DirectoryItem from './tree_items/Directory.vue'
import FileItem from './tree_items/File.vue'
import LinkItem from './tree_items/Link.vue'

export default {
  name: 'Branch',
  props: {
    path: {
      type: String,
      default: '\\'
    },
    content: {
      type: Object,
      default: () => {}
    },
  },
  components: {
    DirectoryItem,
    FileItem,
    LinkItem
  },
  data() {
    return {
      indentSize: 25,
      childIsVisible: false,
    }
  },
  methods: {
    updateTabIndexes () {
      const focusableEls = document.querySelectorAll('.focusable');
      focusableEls.forEach((elem, i) => {
        elem.setAttribute('tabindex', i)
      })
    }
  },
  updated () {
    this.updateTabIndexes();
  }
}
</script>