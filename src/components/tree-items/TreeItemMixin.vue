<script>
import TreeItem from './TreeItem.vue'

export default {
  props: { 
    itemData: {
      type: Object,
      default: () => {}
    },
    isOpened: {
      type: Boolean,
      default: false
    }
  },
  components: { TreeItem },
  data () {
    return {
      isFocused: false,
      iconSize: 50
    }
  },
  methods: {
    selectItem () {
      this.isFocused = true;
    },
    deselectItem () {
      this.isFocused = false;
    },
    goToNext(event) {
      const currIndex = parseInt(event.target.getAttribute('tabindex'));
      const nextElem = document.querySelector(`.focusable[tabindex="${currIndex + 1}"]`);
      nextElem ? nextElem.focus() : console.log('Элемент для перехода отсутствует или находится в свёрнутой папке');
    },
    goToPrev(event) {
      const currIndex = parseInt(event.target.getAttribute('tabindex'));
      const prevElem = document.querySelector(`.focusable[tabindex="${currIndex - 1}"]`);
      prevElem ? prevElem.focus() : console.log('Вы на верхнем уровне, переход невозможен');
    }
  }
}
</script>