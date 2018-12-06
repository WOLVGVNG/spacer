<template>
    <input
      id="search"
      name="search"
      :class="{ dark }"
      placeholder="e.g. Titan"
      :value="value"
      @input="handleChange"
    />
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>

  input {
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    width: 250px;
    z-index: 2;

    color: white;
    font-size: 18px;
    height: 30px;
    border: 0;
    font-weight: 300;
    border-bottom: 1px solid white;
    transition: box-shadow .3s ease-out;
    text-align: center;
    background: none;

    @media (min-width: 1024px) {
      font-weight: 400;
    }
  }

  input::placeholder{
    color: white;
    opacity: .4;
  }

  input:focus {
    outline: none;
    box-shadow: 0 10px 20px -8px rgba(255,255,255, .4);
  }

  .dark{
   color: #1e3d4a;
    border-bottom-color: #1e3d4a;
  }

  .dark:focus {
    outline: none;
    box-shadow: 0 10px 20px -8px rgba(#1e3d4a, .2);
  }
</style>
