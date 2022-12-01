<template>
  <div class="employees__buttons">
    <div class="employees__buttons-left">
      <VButton color="red">
        <AddEmployeeIcon/>
        Добавить сотрудника
      </VButton>
      <VButton color="red" outline>
        <AddDepartmentIcon/>
        Создать новый отдел
      </VButton>
    </div>
    <div class="employees__buttons-right">
      <VButton color="blue">Скачать список прошедших</VButton>
      <VButton color="blue" small>Экспорт</VButton>
      <VButton color="blue">
        <UploadIcon/>
        Загрузить списком
      </VButton>
    </div>
  </div>
</template>

<script>
import VButton from '@/components/VButton.vue';
import AddEmployeeIcon from '@/components/icons/AddEmployeeIcon.vue';
import AddDepartmentIcon from '@/components/icons/AddDepartmentIcon.vue';
import UploadIcon from '@/components/icons/UploadIcon.vue';

export default {
  name: 'EmployeesButtons',
  components: {
    UploadIcon,
    AddDepartmentIcon,
    AddEmployeeIcon,
    VButton,
  },
};
</script>

<style lang="scss" scoped>
.employees__buttons {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-left: var(--left-padding-m);
  margin-bottom: 30px;

  &-right, &-left {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: flex-start;
    gap: 15px;
  }

  @media screen and (max-width: 1280px) {
    gap: 16px 0;
    flex-wrap: wrap;
    padding-left: 0;

    &-left {
      margin-right: 16px;
    }
  }

  @media screen and (max-width: 768px) {
    &-right, &-left {
      width: 100%;
      flex-wrap: wrap;
      margin-right: 0;

      .button {
        max-width: calc(50% - 8px);
      }
    }
    &-right {
      .button:last-child {
        max-width: 100%;
      }
    }
  }

  @media screen and (max-width: 428px) {
    &-right, &-left {
      gap: 12px;

      .button {
        max-width: 100%;
      }
    }
  }
}
</style>
