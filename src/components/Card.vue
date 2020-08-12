<template>
  <!--
    class and style bindings with computed properties,
    for cleaner template code.
  -->
  <div class="card" :class="gridClass" :style="gridStyle"></div>
</template>

<script>
  export default {
    props: [
      'item', 'index'
    ],
    computed: {
      /*
        for the dynamic style
        --i is a CSS variable with the current index,
        for the staggered delay in the App Component
      */
      gridStyle() {
        return { 
          '--i': this.index,
          'background-image': 'url('+ require('../assets'+ this.item.img) +')' };
      },
      /*
        different Card classes, based on the value in item.grid
      */
      gridClass() {
        return { 
          'card-1-1': this.item.grid === 'card-1-1',
          'card-2-1': this.item.grid === 'card-2-1'
        };
      }
    }
  }
</script>

<style lang="scss" scoped>
  /*
    The card element with background definitions,
    Image displayed as background image
  */
  .card {
    width: 100%;
    height: 200px;
    background-position: center;
    background-size: cover;
  }

  /*
    Custom grid element classes
  */
  .card-1-1 {
    grid-column: span 1;
  }

  .card-2-1 {
    grid-column: span 2;
  }  
</style>