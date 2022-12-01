<template>
  <header class="header">
    <button class="logo">
      <LogoIcon/>
    </button>
  </header>
</template>

<script>
import LogoIcon from '@/components/icons/LogoIcon.vue';

export default {
  name: 'TheHeader',
  components: { LogoIcon },
};
</script>

<style lang="scss" scoped>
.logo {
  border: 0;
  cursor: pointer;
  background-color: inherit;
  display: block;
  width: 48px;
  height: 48px;
  transition: var(--transition);

  svg {
    transition: var(--transition);
  }

  @media screen and (max-width: 768px) {
    width: 36px;
    height: 36px;
  }
}

.header {
  background-color: #fff;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  height: 100%;
  width: calc(var(--sidebar--offset) * 2 + 48px);
  padding: 48px 19px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
  border: 1px solid var(--gray);
  margin-top: -1px;
  border-bottom: 0;

  transition: var(--transition);

  @media screen and (max-width: 768px) {
    width: 100%;
    border: 0;
    border-bottom: 1px solid var(--gray);
    height: auto;
    padding: 19px 20px;
    flex-direction: row;
    align-items: center;
    justify-content: flex-start;
    border-left: 0;
  }

  @media screen and (max-width: 428px) {
    padding: 12px 12px;
  }
}

</style>
