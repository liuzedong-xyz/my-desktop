<template>
  <div
   class="move-box"
   :style="`left:${leftPos}px;top:${topPos}px`"
  >
    <div class="bar"
      @mousedown="onMouseDown"></div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'moveBox',
  data() {
    return {
      moveable: false,
      leftPos: 200,
      topPos: 200,
      oldPos: {
        x: 0,
        y: 0
      }
    }
  },

  mounted() {
    window.onmousemove = e => this.onMouseMove(e);
    window.onmouseup = e => this.onMouseUp(e);
  },

  methods: {
    onMouseDown(e) {
      console.log('mouse down');
      console.log(e);

      this.oldPos = {
        x: e.pageX,
        y: e.pageY
      }

      this.moveable = true;
    },
    onMouseMove(e) {
      if(!this.moveable) {
        return;
      }

      console.log('mouse move');

      this.leftPos += e.pageX - this.oldPos.x;
      this.topPos += e.pageY - this.oldPos.y;

      // this.leftPos > 0 || (this.leftPos = 0);
      if(this.leftPos < 0) {
        this.leftPos = 0;
      }

      if(this.topPos < 0) {
        this.topPos = 0;
      }

      this.oldPos = {
        x: e.pageX,
        y: e.pageY
      }
    },
    onMouseUp(e) {
      console.log('mouse up')
      this.moveable = false
    }
  }
  
}
</script>

<style lang="scss" scoped>
.move-box {
  position: absolute;
  left: 400px;
  top: 400px;
  width: 300px;
  height: 300px;
  background-color: #ababab;
  .bar {
    width: 100%;
    height: 20px;
    background-color: red;
    cursor: move;
  }
}
</style>
