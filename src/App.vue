<template>
    <div class="viewer" v-bind:class="{'zoomed-in':zoomScale>1}">
        <pinch-zoom wheel="true" v-on:pinch-zoom="handleZoom" backgroundColor="rgba(0,0,0,0)">
            <img ref="img" class="img"
                 :style="{'border-radius':revScale+'px',}"
                 :zoom=zoomScale
                 src="https://images.unsplash.com/photo-1544606402-e522c304b027?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1564&q=80">
        </pinch-zoom>
        ZoomScale : {{zoomScale}}
    </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

import PinchZoom from './components/PinchZoom.vue'; 

@Component({
    components: {
        'pinch-zoom': PinchZoom
    },
})
export default class myLib extends Vue {
  zoomScale:number=1
  revScale:number=0
  handleZoom(e:any){
    this.zoomScale = e.scale
    this.revScale = 24.0 / e.scale
  }
}
</script>

<style scoped lang="sass">
.img
  border-radius: 24px
.viewer
  margin: 10px
  &.zoomed-in
    margin: 0px
</style>