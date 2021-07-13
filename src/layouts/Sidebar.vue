<template>
  <div class="sidebar-container">
    <aside class="sidebar sidebar--desktop">
      <slot></slot>
    </aside>
    <aside v-if="toggle" class="sidebar sidebar--mobile">
      <button @click="$emit('toggle-sidebar')" class="close-btn">Close</button>
      <slot></slot>
    </aside>
  </div>
</template>

<script>
export default {
  name: 'Sidebar',
  props: ['toggle'],
  emits: ['toggle-sidebar']
}
</script>

<style scoped>
.sidebar-container {
  width: 40%;
}

.sidebar {
  background-color: #15161b;
  color: #efedf0;
  height: 100%;
  padding: 6rem 2.5rem;
}

.sidebar--desktop {
  width: 100%;
}

.sidebar--mobile {
  display: none;
}

.close-btn {
  display: none;
}

@media screen and (max-width: 1000px) {
  .sidebar-container {
    width: 100%;
  }
  .sidebar--mobile {
    display: block;
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    z-index: 100;
    overflow-y: auto;
  }
  .sidebar--desktop {
    display: none;
  }
  .close-btn {
    position: absolute;
    top: 10px;
    right: 5px;
    background-color: transparent;
    padding: 10px 20px;
    display: block;
  }
}
</style>
