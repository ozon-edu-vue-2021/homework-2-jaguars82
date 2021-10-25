<template>
  <div
    class="focusable"
    @focus="selectItem"
    @blur="deselectItem"
    @keydown.down.prevent="goToNext"
    @keydown.up.prevent="goToPrev"
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
            :class="{ 'icon': true, 'icon_active': isFocused }"
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
        <div
          v-if="isFocused"
          class="path"
        >
          <span>Путь к выделенной ссылке: {{ itemData.path }}</span>
        </div>
      </template>

    </tree-item>
  </div>
</template>

<script>
import TreeItemMixin from './TreeItemMixin.vue'

export default {
  name: 'Link',
  mixins: [TreeItemMixin],
  computed: {
    iconpath () {
      return this.isFocused
        ? 'M18,10.82a1,1,0,0,0-1,1V19a1,1,0,0,1-1,1H5a1,1,0,0,1-1-1V8A1,1,0,0,1,5,7h7.18a1,1,0,0,0,0-2H5A3,3,0,0,0,2,8V19a3,3,0,0,0,3,3H16a3,3,0,0,0,3-3V11.82A1,1,0,0,0,18,10.82Zm3.92-8.2a1,1,0,0,0-.54-.54A1,1,0,0,0,21,2H15a1,1,0,0,0,0,2h3.59L8.29,14.29a1,1,0,0,0,0,1.42,1,1,0,0,0,1.42,0L20,5.41V9a1,1,0,0,0,2,0V3A1,1,0,0,0,21.92,2.62Z'
        : 'M12.11,15.39,8.23,19.27a2.52,2.52,0,0,1-3.5,0,2.47,2.47,0,0,1,0-3.5l3.88-3.88a1,1,0,1,0-1.42-1.42L3.31,14.36a4.48,4.48,0,0,0,6.33,6.33l3.89-3.88a1,1,0,0,0-1.42-1.42ZM20.69,3.31a4.49,4.49,0,0,0-6.33,0L10.47,7.19a1,1,0,1,0,1.42,1.42l3.88-3.88a2.52,2.52,0,0,1,3.5,0,2.47,2.47,0,0,1,0,3.5l-3.88,3.88a1,1,0,0,0,0,1.42,1,1,0,0,0,1.42,0l3.88-3.89A4.49,4.49,0,0,0,20.69,3.31ZM8.83,15.17a1,1,0,0,0,.71.29,1,1,0,0,0,.71-.29l4.92-4.92a1,1,0,1,0-1.42-1.42L8.83,13.75A1,1,0,0,0,8.83,15.17Z';
    }
  }
}
</script>

<style scoped>
  .icon {
    fill: #0095B6;
  }

  .icon_active {
    fill: #1560BD;
  }
</style>