<template>
  <div id="app">
    <div class="container">
      <div class="flex wrapper">
        <my-input
          v-bind="{ prefix, inputString, regRule }"
          @sendStr="getStr"
          @focusInput="focus"
          @blurInput="blur"
        ></my-input>
      </div>
    </div>
  </div>
</template>

<script>
import MyInput from '@/components/MyInput.vue';
export default {
  name: 'App',
  components: {
    MyInput,
  },
  data: () => ({
    inputString: '',
    prefix: '$',
    regRule: /^\d+$/,
  }),
  methods: {
    getStr(e) {
      this.inputString = e;
    },
    focus() {
      console.log('focused');
    },
    blur() {
      console.log('blured');
    },
  },
};
</script>

<style lang="sass">
.wrapper
  justify-content: center
  align-items: center
</style>
