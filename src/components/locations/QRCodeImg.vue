<template>
  <div>
    <canvas ref="canvas"></canvas>
  </div>
</template>

<script lang="ts">
import {Component, Prop, Vue} from 'vue-property-decorator';
import {QRCodeToDataURLOptions, toCanvas} from 'qrcode';

@Component
  export default class QRCodeImg extends Vue {
    public $refs!: {
      canvas: HTMLFormElement
    };

    @Prop()
    private url!: string;

    public mounted() {
      const opts = {
        scale: 10
      } as QRCodeToDataURLOptions;
      toCanvas(this.$refs.canvas, `url:${this.url}`, opts, (error) => {
        if (error) { console.error(error); }
        console.log('success!');
      });
    }

  }
</script>

<style scoped>
  canvas {
    width: 150px;
  }
</style>
