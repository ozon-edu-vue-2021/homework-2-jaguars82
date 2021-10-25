<template>
  <div
    class="focusable"
    @click="toggleDirectory"
    @focus="isFocused = true"
    @blur="isFocused = false"
    @keydown.down.prevent="goToNext"
    @keydown.up.prevent="goToPrev"
    @keydown.enter.prevent="toggleDirectory"
    tabindex="0"
  >
    <tree-item>

      <template v-slot:icon>
        <svg
          :width="iconSize"
          :height="iconSize"
          :viewBox="`0 0 ${ iconSize / 2 } ${ iconSize / 2 }`"
        >
          <path
            :class="{ 'icon': true, 'icon_active': isOpened}"
            :d="iconpath"
          />
        </svg>
      </template>

      <template v-slot:content>
        <div :class="{ 'item-name': true, 'item-name_active': isFocused }">
          {{ itemData.name }}
        </div>
      </template>

      <template v-slot:path>
        <div v-if="isFocused" class="path">
          <span>Выделенная папка расположена в {{ itemData.path }}</span>
        </div>
      </template>

    </tree-item>
  </div>
</template>

<script>
import TreeItemMixin from './TreeItemMixin.vue'

export default {
  name: 'Directory',
  mixins: [TreeItemMixin],
  computed: {
    iconpath () {
      return this.isOpened
        ? 'M14,12.5H10a1,1,0,0,0,0,2h4a1,1,0,0,0,0-2Zm5-7H12.72l-.32-1a3,3,0,0,0-2.84-2H5a3,3,0,0,0-3,3v13a3,3,0,0,0,3,3H19a3,3,0,0,0,3-3V8.5A3,3,0,0,0,19,5.5Zm1,13a1,1,0,0,1-1,1H5a1,1,0,0,1-1-1V5.5a1,1,0,0,1,1-1H9.56a1,1,0,0,1,.95.68l.54,1.64A1,1,0,0,0,12,7.5h7a1,1,0,0,1,1,1Z'
        : 'M14,12.5H13v-1a1,1,0,0,0-2,0v1H10a1,1,0,0,0,0,2h1v1a1,1,0,0,0,2,0v-1h1a1,1,0,0,0,0-2Zm5-7H12.72l-.32-1a3,3,0,0,0-2.84-2H5a3,3,0,0,0-3,3v13a3,3,0,0,0,3,3H19a3,3,0,0,0,3-3V8.5A3,3,0,0,0,19,5.5Zm1,13a1,1,0,0,1-1,1H5a1,1,0,0,1-1-1V5.5a1,1,0,0,1,1-1H9.56a1,1,0,0,1,.95.68l.54,1.64A1,1,0,0,0,12,7.5h7a1,1,0,0,1,1,1Z';
    }
  },
  methods: {
    toggleDirectory () {
      this.isOpened = !this.isOpened;
      this.$emit('toggle');
    },
  }
}
</script>

<style scoped>
.icon {
  fill: orange;
}

.icon_active {
  fill: orangered;
}
</style>