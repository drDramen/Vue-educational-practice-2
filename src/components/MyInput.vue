<template>
  <div>
    <label>
      <input
        type="text"
        :class="noValid"
        :value="unprefixedStr"
        @input="isValid"
        @focus="$emit('focusInput')"
        @blur="$emit('blurInput')"
      />
      <span class="prefix">{{ prefix }}</span>
    </label>
    <span class="error" v-if="noValid['no-valid']">Только цифры</span>
  </div>
</template>

<script>
export default {
  name: 'MyInput',
  data: () => ({
    noValid: { 'no-valid': false },
  }),
  props: {
    prefix: String,
    inputString: String,
    regRule: RegExp,
  },
  methods: {
    sendStr(e) {
      this.$emit('sendStr', `${this.prefix}${e.target.value}`);
    },
    isValid(e) {
      let valid = this.regRule.test(e.target.value);
      this.noValid['no-valid'] = valid || !e.target.value ? false : true;
      this.sendStr(e);
    },
  },
  computed: {
    unprefixedStr() {
      return this.inputString.replace(this.prefix, '');
    },
  },
};
</script>

<style lang="sass" scoped>
label
  position: relative
  display: block
  input
    padding: 10px 15px 10px 30px
    width: 250px
    font-size: 3rem
    font-weight: bold
    border-radius: 5px
    border: none
    background: #e0e0e0
    box-shadow: inset -5px 5px 10px rgb(190, 190, 190), inset 5px -5px 10px rgb(255, 255, 255)
    outline: none
    &.no-valid
      border: 1px solid rgb(233, 30, 99)
    &:focus
      border: 1px solid rgb(57, 99, 135)
      & + .prefix
        color: #4CAF50
      &.no-valid
        border: 1px solid rgb(233, 30, 99)
  .prefix
    position: absolute
    top: 50%
    left: 10px
    transform: translateY(-50%)
    font-size: 3rem
    color: #b9b9b9

.error
  display: block
  color: rgb(233, 30, 99)
  font-size: 1.4rem
  text-align: center
</style>
