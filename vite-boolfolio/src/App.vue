<script >
  import MainHeader from './components/MainHeader.vue';
  import MainMain from './components/MainMain.vue';
  import MainFooter from './components/MainFooter.vue';

  export default {
    name:"",
    components:{
       MainHeader,
       MainMain,
       MainFooter
    }
}
</script>

<template>
  <MainHeader/>
  <MainMain/>
  <MainFooter/>
</template>

<style lang="scss">
header {
  line-height: 1.5;
} 

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
