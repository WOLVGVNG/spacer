<template>
  <div class="outerWrapper">
    <div class="innerWrapper">
      <div class="photo">
        <img :src="photo">
      </div>
      <div class="description">
        <h2 class="title">{{ title }}</h2>
        <p class="description">{{ description }}</p>
      </div>
      <div class="close"  @click="$emit('closeModal')" />
    </div>
    </div>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: null,
      title: null,
      description: null,
    };
  },
  mounted() {
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
    this.description = this.item.data[0].description.substring(0, 200);
  },
};

</script>

<style lang="scss" scoped>
  .outerWrapper {
    background: #f6f6f6;
    position: fixed;
    width: 100%;
    height: 100%;
    z-index: 3;
    top: 0;
    left: 0;
    padding-bottom: 20px;


    @media (min-width: 1024px) {
      max-width: 70%;
      height: 60%;
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
      margin: auto;
      padding-bottom: 0px;
      box-shadow: 0 0 135px 13px rgba(0, 0, 0, 0.75);
    }
  }

  .innerWrapper{
    display: flex;
    flex-direction: column;
    height: 100%;
    width: 100%;
    padding: 30px;
    justify-content: center;
    align-items: center;
    margin: 30px auto auto;

    @media (min-width: 1024px){
      flex-direction: row;
      padding: 50px;
      margin-top: 0;
    }
  }

  .photo {
    width: 100%;
    height: 100%;
    display: flex;

    @media (min-width: 1024px){
      margin-right: 20px;
    }

    img {
      max-width: 100%;
      height: 90%;
      margin: auto;

      @media (min-width: 1024px){
        max-width: 100%;
        height: 100%;
      }
    }
  }

  .close {
    position: absolute;
    width: 30px;
    height: 30px;
    padding: 30px;
    right: 0;
    top: 0;
    cursor: pointer;

    &::before,
    &::after
    {
      position: absolute;
      top: 30px;
      right: 20px;
      content: '';
      width: 20px;
      height: 2px;
      background: black;
      display: block;
    }

    &::before {
      transform: rotate(45deg);
    }

    &::after {
      transform: rotate(-45deg);
    }
  }


  .description {
    width: 100%;
    color: #333;
    margin: auto;
    text-align: justify;

    @media (max-width: 768px) {
      font-size: 14px;
    }
  }

  .title{
    margin-top: 20px;
    font-weight: 600;
    color: #1e3d4a;
    text-align:  center;

    @media (max-width: 768px) {
      font-size: 22px;
    }
  }

</style>
