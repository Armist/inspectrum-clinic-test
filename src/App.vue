<template>
  <div id="app">
    <TheHeader/>
    <main class="main">
      <TheEmployees/>
    </main>
  </div>
</template>

<script>
import TheHeader from '@/components/TheHeader.vue';
import TheEmployees from '@/components/Employees/TheEmployees.vue';

export default {
  name: 'App',
  components: {
    TheEmployees,
    TheHeader,
  },
};
</script>

<style lang="scss">
@import './styles/main.scss';

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100%;
  margin: 0 auto;
  max-width: 1440px;
  position: relative;
  display: flex;
  flex-direction: row;
  justify-content: space-between;

  @media screen and (max-width: 768px) {
    flex-direction: column;
  }
}

.main {
  height: 100%;
  flex: 1 1 0;
  overflow-y: scroll;
  scrollbar-width: none;

  &::-webkit-scrollbar {
    width: 0;
    height: 0;
  }

  padding: 47px 130px 47px 43px;

  @media screen and (max-width: 1280px) {
    padding: 47px 43px;
  }

  @media screen and (max-width: 768px) {
    padding: 20px;
  }

  @media screen and (max-width: 428px) {
    padding: 20px 12px;
  }
}
</style>
