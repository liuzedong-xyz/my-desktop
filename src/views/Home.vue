<template>
  <div class="container">
    <div class="window">
      <!-- <move-box>
        <p>This is a qqq</p>
      </move-box> -->
      <button class="btn" @click="showBox"></button>
    </div>
    <div class="bottom-bar"></div>
  </div>
</template>

<script>
// import moveBox from '@/components/moveBox';

export default {
  name: 'Home',
  methods: {
    async showBox() {
      const res = await this.$box('test');
      console.log(res);
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: column;
  height: 100vh;

  .bottom-bar {
    width: 100%;
    height: 60px;
    background-color: #ffffff;
  }

  .window {
    position: relative;
    width: 100%;
    flex-grow: 1;
    overflow: hidden;
  }
}

.btn {
  width: 100px;
  height: 100px;
}

</style>
