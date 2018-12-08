<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
    <transition name="slide">
      <img src="../assets/logo.svg" alt="logo" class="logo" v-if="step === 1"
           @click="handleBack()" style="cursor: pointer">
    </transition>
    <transition name="fade">
      <HeroImage v-if="step === 0" />
    </transition>
    <Claim v-if="step === 0" />
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1" />
    <div class="results" v-if="results && !loading && step ===1">
      <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id"
            @click.native="handleModalOpen(item)"/>
    </div>
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"/>
    <div class="loader" v-if="step === 1 && loading"></div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  components: {
    Claim,
    SearchInput,
    HeroImage,
    Item,
    Modal,
  },
  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleBack() {
      this.step = 0;
      this.searchValue = '';
    },
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    // eslint-disable-next-line
    handleInput: debounce(function () {
      this.loading = true;
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss">
  @import '../../node_modules/bootstrap/scss/bootstrap';
  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800');

  $font-weight-light: 300;
  $font-weight-normal: 400;
  $font-weight-bold: 600;
  $font-weight-black: 800;

  *{
  box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  body{
    font-family: 'Montserrat', sans-serif;
    margin: 0;
    padding: 0;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s ease;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .slide-enter-active, .slide-leave-active {
    transition: margin-top .3s ease;
  }
  .slide-enter, .slide-leave-to {
    margin-top: -50px ;
  }

  .wrapper {
    margin: 0;
    position: relative;
    width: 100%;
    min-height: 100vh;
    padding: 30px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

    &.flexStart {
      justify-content: flex-start;
    }
  }


  .logo {
    position: absolute;
    top: 30px;
  }

  .results {
    margin-top: 50px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-column-gap: 40px;
    grid-row-gap: 40px;

    @media (min-width: 768px) {
      grid-template-columns: 1fr 1fr 1fr;
    }
  }

  .loader {
    margin-top: 100px;
    display: inline-block;
    width: 100px;
    height: 100px;

    @media (min-width:1024px) {
      margin-top: 150px;
    }
  }

  .loader:after {
    content: " ";
    display: block;
    width: 46px;
    height: 46px;
    margin-left: 25px;

    @media (min-width:1024px) {
    width: 70px;
    height: 70px;
    margin-left: 13px;
  }

    border-radius: 50%;
    border: 5px solid #1e3d4a;
    border-color: #1e3d4a transparent #1e3d4a transparent;
    animation: loading 1.2s linear infinite;
  }

  @keyframes loading {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }


  .search{
    display: none;
    flex-direction: column;
    width: 300px;
  }

  label{
    font-family: Montserrat, sans-serif;
  }

  input{
    height: 30px;
    border: 0;
    border-bottom: 1px solid;
  }
</style>
