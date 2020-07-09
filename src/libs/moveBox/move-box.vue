<template>
  <div
   class="move-box"
   :style="`left:${leftPos}px;top:${topPos}px`"
   @mouseenter="bindMouseEvent"
   @mouseleave="unbindMouseEvent"
  >
    <div class="bar"
      @mousedown="onMouseDown"
      @mouseup="onMouseUp"
    >
      <div class="close btn"></div>
      <div class="min btn"></div>
      <div class="max btn"></div>
    </div>
    
    <dialog-content ref="body"></dialog-content>
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
      },
      visible: false,
      disabled: false
    }
  },

  computed: {
    classSize() {
      // if(this.size == small)
      return this.size;
    }
  },

  mounted() {
    // window.onmousemove = e => this.onMouseMove(e);
    // window.onmouseup = e => this.onMouseUp(e);
  },

  methods: {
    bindMouseEvent() {
      console.log('in');
      window.addEventListener('mousemove', e => {
        this.onMouseMove(e)
      })
    },
    unbindMouseEvent() {
      console.log('leave');
      window.removeEventListener('mousemove', () => {});
    },
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
    onMouseUp() {
      console.log('mouse up')
      this.moveable = false
    },
    open() {
      this.visible = true;
    },
    handleAction(button) {
      this.$emit('action', button);
    },
    close() {
      this.visible = false;
      setTimeout(() => {
        this.$emit('close');
      }, 100);
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
  // background-color: #ababab;
  border-radius: 5px;
  border: 1px solid #d2d2d2;
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.25);
  overflow: hidden;

  

  .bar {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: flex-start;
    width: 100%;
    height: 22px;
    // background-color: red;
    background-image: linear-gradient(to top, #d4d2d4, #e8e6e8);
    border-bottom: 1px solid #b3b1b3;
    cursor: move;

    .btn {
      width: 12px;
      height: 12px;
      margin-left: 8px;
      border-radius: 50%;
      border-width: 1px;
      border-style: solid;
    }

    .close {
      background-color: #ff605b;
      border-color: #ef4643;
    }

    .min {
      background-color: #ffbb49;
      border-color: #ea9f3e;
    }

    .max {
      background-color: #00c753;
      border-color: #12aa41;
    }
  }
}

.close {
  width: 50px;
  height: 20px;
  color: #000;
}
</style>
