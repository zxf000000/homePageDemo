<template>
  <div class="container">
    <div class="container__sub">
      <div class="container__sub--first"></div>
    </div>
    <div class="other">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Another',
  props: {
    msg: String
  }
}
</script>

<style scoped lang="sass">

$backgroundColor: red
$container-width: 100px
$sub-width: 90px
$first-width: 80px

%shadow
  box-shadow: 0 0 20px black

.other
  margin-top: 20px
  width: 200px
  height: 200px
  border-radius: 20px
  border: dashed 1px #fff
  background: linear-gradient(white, white) padding-box, linear-gradient(to right, blue, yellow) border-box

.container
  margin-left: 100px
  background: $backgroundColor
  width: $container-width
  height: $container-width
  border-radius: $container-width/2
  @extend %shadow
  &__sub
    background: blue
    width: $sub-width
    height: $sub-width
    border-radius: $sub-width/2
    &--first
      background: yellow
      width: $first-width
      height: $first-width
      border-radius: $first-width/2


</style>
