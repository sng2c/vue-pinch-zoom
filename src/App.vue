<template>
  <div class="main" v-bind:class="{'zoomed-in':zoomScale>1}">
    <div class="head">ZoomScale : {{ zoomScale }}</div>
    <div class="body">
      <div class="viewer">
        <pinch-zoom ref=pin
                    wheel="false"
                    backgroundColor="rgba(0,0,0,0)"
                    v-on:pinch-zoom="handleZoom">
          <img ref="img" class="img"
               :style="{'border-radius':(12/zoomScale)+'px',}"
               src="/imgs/sample_1280x1920.png">
        </pinch-zoom>

      </div>
    </div>
  </div>
</template>

<script lang="ts">
import {Component, Vue} from 'vue-property-decorator';

import PinchZoom from './components/PinchZoom.vue';

@Component({
  components: {
    'pinch-zoom': PinchZoom
  },
})
export default class myLib extends Vue {
  zoomScale: number = 1

  handleZoom(e: any) {
    console.log(e)
    this.zoomScale = e.scale
    let img = this.$refs.img as HTMLImageElement
    let pin = (this.$refs.pin as Vue).$el
    let scale = 0
    if ( img.width/img.height < 1 ){
      scale = pin.clientWidth/img.width
    } else {
      scale = pin.clientHeight/img.height
    }
    img.width = img.width*scale
    img.height = img.height*scale
  }
}
</script>

<style scoped lang="sass">
div

.main
  position: fixed
  display: flex
  flex-direction: column
  background-color: crimson
  height: 100%
  width: 100%

.head
  min-height: 100px
  background-color: blue
  flex-grow: 0
  padding: 5px

.foot
  min-height: 100px
  flex-grow: 0
  background-color: blue
  padding: 5px

.body
  flex-grow: 1
  background-color: yellow
  padding: 5px
  overflow: hidden

.viewer
  position: relative
  padding: 10px
  padding-bottom: 20px
  background-color: chartreuse
  height: 100%
  box-sizing: border-box

.main.zoomed-in
  .viewer, .body
    padding: 0px

.pinch-zoom-wrapper
  width: 100%
  height: 100%
  flex-grow: 1

.img
  border-radius: 24px

</style>