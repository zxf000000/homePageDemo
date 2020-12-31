<template>
  <v-container class="d-flex flex-column container">
    <div class="d-flex buttons">
      <v-btn v-on:click="tapLeft" :disabled="showA">Enterprise</v-btn>
      <v-btn v-on:click="tapRight" :disabled="!showA">Individual</v-btn>
    </div>
    <div class="page-box">
      <div class="page-container" :class="{'slide-in': showA}">
        <div class="big-box-a big-box"></div>
        <div class="small-box-a small-box"></div>
      </div>
      <div class="page-container" :class="{'slide-in': !showA}">
        <div class="big-box-b big-box"></div>
        <div class="small-box-b small-box"></div>
      </div>
    </div>
    <div style="height: 1000px"></div>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',
    methods: {
      tapLeft: function () {
        this.showA = true
      },
      tapRight: function () {
        this.showA = false
      }
    },
    mounted() {
      let thresholds = []
      for (let i = 0; i < 100; i++) {
        thresholds.push(i * 0.01)
      }
      let options = {
        rootMargin: '0px',
        threshold: thresholds
      }
      let observer = new IntersectionObserver((entries) => {
        let entry = entries[0]
        console.log(entry)

          console.log(entry.intersectionRatio)
          let minTop = 400;
          let maxTop = 700;
          let currentTop = (maxTop - minTop) * (1 - entry.intersectionRatio) + minTop
          let targets = document.getElementsByClassName('small-box')
          console.log(currentTop)
          for (var i = 0; i < targets.length; i++) {
            targets[i].setAttribute('style', 'top:' + currentTop + 'px !important');
          }


      console.log(window.innerHeight)
      }, options)
      observer.observe(document.querySelector('.page-container'))
    },
    data: () => ({
      showA: false
    }),
  }
</script>

<style scoped lang="sass">
  $page-width: 800px
  $page-height: 1000px
  $transition: all 0.5s linear
  .container
    margin-top: 1000px

  .buttons
    height: 100px
    background: aquamarine

  .page-container
    position: absolute
    width: $page-width
    height: $page-height
    margin-top: 30px
    transition: $transition
    transform: translateX(10%)
    opacity: 0
    background: gray

  .slide-in
    transform: translateX(0)
    opacity: 1

  .big-box
    width: 800px
    height: 500px

  .big-box-a
    background: blue

  .big-box-b
    background: red

  .small-box
    width: 250px
    height: 200px
    position: absolute
    left: 200px
    top: 600px

  .small-box-a
    background: yellow

  .small-box-b
    background: green

</style>
