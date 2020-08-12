<template>
  <div id="app">
    <!-- 
      Animation for one item,
      appear attribute for the initial transition,
      name is the prefix for the css classes
    -->
    <transition appear name="slide-in">
      <h1>Discover</h1>
    </transition>

    <!-- 
      Animation for a list or group of items.
      appear attribute for the initial transition
      name is the prefix for the css classes.
      You can also specify which element this component 
      should be, with the tag attribute
    -->
    <transition-group appear name="slide-in" 
                      class="grid-wrapper" tag="div">
      <Card v-for="(card, index) in cards" 
            :key="'card'+index"
            :item="card" :index="index" />
    </transition-group>
  </div>
</template>

<script>
import Card from './components/Card'

export default {
  data: () => {
    return {
      cards: [
        /*
          Images are in the assets folder,
          grid is the CSS class
        */
        { img: '/img-1.jpg', grid: 'card-2-1' },
        { img: '/img-2.jpg', grid: 'card-1-1' },
        { img: '/img-3.jpg', grid: 'card-1-1' },
        { img: '/img-4.jpg', grid: 'card-2-1' },
        { img: '/img-5.jpg', grid: 'card-1-1' },
        { img: '/img-6.jpg', grid: 'card-1-1' }
      ]
    }
  },
  components: {
    Card
  }
}
</script>

<style lang="scss">
  * {
    font-size: 1rem;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  h1 { font-size: 2rem; }

  body {
    width: 100%;
    font-family: 'Segoe UI', Tahoma;
    background-color: #efefef;
    color: #333;
  }

  #app {
    position: relative;
    padding: 10px;
    width: 100%;
    min-height: 100vh;
  }

  /*
    grid layout, dynamically with repeat, 
    as the first argument you can set the number of columns, 
    I gonna use 2 in this case.
    And as the second argument, 
    you can set the width from each column, 
    and if you want it responsive you can set here 1 fraction, 
    this means that each column has the same width, 
    based on the absolute width, in this case, 50 percent.
  */
  .grid-wrapper {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 10px;
  }

  /*
    This class would be automatically added to the element 
    before the element is inserted and removed one frame 
    after the element is inserted. 
    Basically it’s the initial state from the element.
  */
  .slide-in-enter {
    opacity: 0;
    transform: scale(.5);
  }

  /*
    This class can be used to define the duration, 
    delay and easing curve for the entering transition.
    --i is the CSS variable from the Card Component (current index)
    With this you have a staggered delay.
  */
  .slide-in-enter-active {
    transition: all .4s ease;
    transition-delay: calc( .1s * var(--i) );
  }
</style>
