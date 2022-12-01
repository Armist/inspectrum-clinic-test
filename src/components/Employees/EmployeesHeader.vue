<template>
  <header class="employees__header">
    <h1 class="employees__header-title">Сотрудники</h1>
    <div class="employees__header-company">
      <div class="company__avatar">
        <span>{{ firstLetterOfCompany }}</span>
      </div>
      <span class="company__name">
        {{ companyName }}
      </span>
    </div>
  </header>
</template>

<script>

export default {
  name: 'EmployeesHeader',
  props: {
    companyName: {
      type: String,
      required: true,
    },
  },
  computed: {
    firstLetterOfCompany() {
      return this.companyName[0];
    },
  },
};
</script>

<style lang="scss" scoped>
.employees__header {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  padding-left: var(--left-padding-m);
  padding-right: 54px;

  margin-bottom: 30px;

  &-title {
    font-size: var(--title);
    line-height: var(--title-lh);
    font-weight: var(--m);
  }

  @media screen and (max-width: 1280px) {
    padding-left: 0;
    padding-right: 27px;
  }

  @media screen and (max-width: 428px) {
    padding-right: 0;
  }
}

.employees__header-company {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;

  .company__avatar {
    margin-right: var(--icon-margin);

    border-radius: var(--full-rad);
    background-color: var(--red);

    width: 24px;
    height: 24px;

    display: flex;
    align-items: center;
    justify-content: center;

    span {
      color: var(--white);
      font-size: var(--btn);
      line-height: var(--btn-lh);
      font-weight: var(--xl);
    }
  }

  .company__name {
    line-height: var(--text-lh-m);
    font-weight: var(--m);
  }
}
</style>
