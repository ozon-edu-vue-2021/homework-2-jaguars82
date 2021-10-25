<template>
  <div class="wrapper">
    <slot name="icon">
    </slot>
    <div>
    <slot name="content">
    </slot>
    </div>
    <slot name="path"></slot>
  </div>
</template>

<script>
export default {
  name: 'TreeItem',
}
</script>

<style scoped>
div.wrapper {
  display: flex;
  align-items: center;
  cursor: default;
  user-select: none;
}

.item-name {
  color: #555;
  font-size: 20px;
  padding-left: 15px;
}

.item-name_active {
  font-weight: bold;
}

.path {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  font-size: 24px;
  padding: 20px 50px;
  color: #FFF;
  background-color: darkslategray;
}
</style>