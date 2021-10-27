<template>
  <div
    class="focusable"
    @focus="selectItem"
    @blur="deselectItem"
    @keydown.down.prevent="goToNext"
    @keydown.up.prevent="goToPrev"
    tabindex="0"
  >
    <TreeItem>

      <template v-slot:icon>
        <svg
          :width="iconSize"
          :height="iconSize"
          :viewBox="`0 0 ${ iconSize / 2 } ${ iconSize / 2 }`"
        >
          <path
            :class="['icon', { 'icon_active': isFocused }]"
            :d="iconpath"
          />
        </svg>
      </template>

      <template v-slot:content>
        <div :class="['item-name', { 'item-name_active': isFocused }]">
          {{ itemData.name }}
        </div>
      </template>

      <template v-slot:path>
        <div
          v-if="isFocused"
          class="path"
        >
          <span>Путь к выделенному файлу: {{ itemData.path }}</span>
        </div>
      </template>

    </TreeItem>
  </div>
</template>

<script>
import TreeItemMixin from './TreeItemMixin.vue'

export default {
  name: 'File',
  mixins: [TreeItemMixin],
  computed: {
    iconpath () {
      return this.isFocused
        ? 'M20,8.94a1.31,1.31,0,0,0-.06-.27l0-.09a1.07,1.07,0,0,0-.19-.28h0l-6-6h0a1.07,1.07,0,0,0-.28-.19.32.32,0,0,0-.09,0A.88.88,0,0,0,13.05,2H7A3,3,0,0,0,4,5V19a3,3,0,0,0,3,3H17a3,3,0,0,0,3-3V9S20,9,20,8.94ZM14,5.41,16.59,8H15a1,1,0,0,1-1-1ZM18,19a1,1,0,0,1-1,1H7a1,1,0,0,1-1-1V5A1,1,0,0,1,7,4h5V7a3,3,0,0,0,3,3h3Zm-3.71-6.71L11,15.59l-1.29-1.3a1,1,0,0,0-1.42,1.42l2,2a1,1,0,0,0,1.42,0l4-4a1,1,0,0,0-1.42-1.42Z'
        : 'M20,8.94a1.31,1.31,0,0,0-.06-.27l0-.09a1.07,1.07,0,0,0-.19-.28h0l-6-6h0a1.07,1.07,0,0,0-.28-.19l-.09,0L13.06,2H7A3,3,0,0,0,4,5V19a3,3,0,0,0,3,3H17a3,3,0,0,0,3-3V9S20,9,20,8.94ZM14,5.41,16.59,8H14ZM18,19a1,1,0,0,1-1,1H7a1,1,0,0,1-1-1V5A1,1,0,0,1,7,4h5V9a1,1,0,0,0,1,1h5Z';
    }
  }
}
</script>

<style scoped>
  .icon {
    fill: grey;
  }

  .icon_active {
    fill: darkslategray;
  }
</style>