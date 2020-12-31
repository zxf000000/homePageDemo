<template>
  <v-container class="d-flex flex-column container">
    <div style="height: 500px"></div>
    <div class="d-flex buttons">
      <v-btn v-on:click="tapLeft" :disabled="showA">Enterprise</v-btn>
      <v-btn v-on:click="tapRight" :disabled="!showA">Individual</v-btn>
    </div>
    <div class="page-box">
      <div class="page-container" :class="{'slide-in': showA}">
        <div class="big-box-a big-box"></div>
        <div class="small-box-a small-box" :class="{'small-slide-out': !showA}"></div>
      </div>
      <div class="page-container" :class="{'slide-in': !showA}">
        <div class="big-box-b big-box"></div>
        <div class="small-box-b small-box" :class="{'small-slide-out': showA}"></div>
      </div>
    </div>
    <div style="height: 2000px"></div>
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
      console.log('enter')
      window.addEventListener('scroll', function () {
        let startOffet = 0
        let endOffset = 1200
        let windowOffset = window.pageYOffset
        let progress = 0
        if (windowOffset > endOffset) {
          progress = 1
        } else if (windowOffset < startOffet) {
          progress = 0
        } else {
          progress = (windowOffset - startOffet)/1200
        }
        let smallStartOffset = 700
        let smallBoxEndOffset = 0
        let currentOffset = smallStartOffset - progress * (smallStartOffset - smallBoxEndOffset)
        let targets = document.getElementsByClassName('small-box')
        for (var i = 0; i < targets.length; i++) {
          targets[i].setAttribute('style', 'top:' + currentOffset + 'px !important');
        }
      })
    },
    data: () => ({
      showA: false
    }),
  }
</script>

<style scoped lang="sass">
  $page-width: 800px
  $page-height: 500px
  $transition: all 0.2s linear

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
    transition: transform 0.2s linear

  .small-box-a
    background: yellow

  .small-box-b
    background: green

  .small-slide-out
    transform: translate(40%, -40%)

</style>
