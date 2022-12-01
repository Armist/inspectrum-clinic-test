<template>
  <div class="employees">
    <EmployeesHeader :company-name="company.name"/>
    <EmployeesButtons/>
    <TheInput v-model="searchValue"/>
    <div class="table">
      <p class="table__count">
        Показаны записи
        <span>{{ getAllEmployeesCount() === 0 ? '0' : '1' }}-{{ getAllEmployeesCount() }}</span>
        из
        <span>{{ getAllEmployeesCount() }}</span>.
      </p>
      <div class="table__row table__header">
        <div class="table__cell">
          <VCheckbox v-model="selectAll" :item="company.employees"/>
        </div>
        <div class="table__cell">
          <div class="header__text-large">ФИО</div>
          <div class="header__text-small">Выбрать все</div>
        </div>
        <div class="table__cell">Должность</div>
        <div class="table__cell">Статус МО</div>
        <div class="table__cell">Дата записи</div>
        <div class="table__cell">Дата прохождения</div>
        <div class="table__cell"></div>
      </div>
      <ul>
        <li v-for="(department, index) in company.departments" :key="index"
            class="table__department">
          <div class="table__department-body">
            <span class="table__department-name">{{ department.name }}</span>
            <span class="table__department-count">{{
                departmentEmployeesCount(department.id)
              }}</span>
            <div class="table__department-buttons button-group">
              <button>
                <EditIcon/>
              </button>
              <button>
                <DeleteIcon/>
              </button>
              <button :class="`table__department-button ${department.isShown ? 'clicked' : ''}`"
                      @click="department.isShown = !department.isShown">
                <DownArrowIcon/>
              </button>
            </div>
          </div>
          <ul :class="`table__department-employees ${department.isShown ? 'shown' : ''}`">
            <li class="employee table__row"
                v-for="(employee, indexEmp) in getEmployeesOfDepartment(department.id)"
                :key="indexEmp">
              <div class="table__cell employee__check">
                <VCheckbox v-model="selected" :item="employee"/>
              </div>
              <span class="table__cell employee__name">
                <span class="info">ФИО</span>
                {{ employee.fullName }}
              </span>
              <span class="table__cell employee__post">
                <span class="info">Должность</span>
                {{ employee.post }}
              </span>
              <span class="table__cell employee__status">
                <span class="info">Статус МО</span>
                {{ employee.status }}
              </span>
              <span class="table__cell employee__record">
                <span class="info">Дата записи</span>
                {{ formatDate(employee.recordingDate) }}
              </span>
              <span class="table__cell employee__passage">
                <span class="info">Дата прохождения</span>
                {{ formatDate(employee.passageDate) }}
              </span>
              <div class="table__cell employee__buttons">
                <div class="button-group">
                  <button>
                    <SwapIcon/>
                  </button>
                  <button @click="deleteEmployee(employee.id)">
                    <DeleteIcon/>
                  </button>
                  <button>
                    <RightArrowIcon/>
                  </button>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import TheInput from '@/components/TheInput.vue';
import VCheckbox from '@/components/VCheckbox.vue';
import EditIcon from '@/components/icons/EditIcon.vue';
import DeleteIcon from '@/components/icons/DeleteIcon.vue';
import DownArrowIcon from '@/components/icons/DownArrowIcon.vue';
import SwapIcon from '@/components/icons/SwapIcon.vue';
import RightArrowIcon from '@/components/icons/RightArrowIcon.vue';
import EmployeesHeader from '@/components/Employees/EmployeesHeader.vue';
import EmployeesButtons from '@/components/Employees/EmployeesButtons.vue';

export default {
  name: 'TheContent',
  components: {
    EmployeesButtons,
    EmployeesHeader,
    RightArrowIcon,
    SwapIcon,
    DownArrowIcon,
    DeleteIcon,
    EditIcon,
    VCheckbox,
    TheInput,
  },
  data() {
    return {
      searchValue: '',
      selected: [],
      allSelected: false,
      company: {
        name: 'ООО «Модуль»',
        departments: [
          {
            id: 1,
            name: 'Отдел продаж',
            isShown: false,
          },
          {
            id: 2,
            name: 'Склад',
            isShown: false,
          },
        ],
        employees: [
          {
            id: 1,
            fullName: 'Стрелков Алексей Мэлсович',
            post: 'Менеджер',
            status: 'Проходит',
            recordingDate: new Date(2022, 9, 5),
            passageDate: new Date(2022, 9, 5),
            department: 1,
            selected: true,
          },
          {
            id: 2,
            fullName: 'Горбунов Велор Наумович',
            post: 'Менеджер',
            status: 'Проходит',
            recordingDate: new Date(2022, 9, 5),
            passageDate: new Date(2022, 9, 5),
            department: 1,
            selected: false,
          }, {
            id: 3,
            fullName: 'Рыбаков Яков Святославович',
            post: 'Менеджер',
            status: 'Проходит',
            recordingDate: new Date(2022, 9, 5),
            passageDate: new Date(2022, 9, 5),
            department: 1,
            selected: false,
          },
          {
            id: 4,
            fullName: 'Жданов Давид Лаврентьевич',
            post: 'Кладовщик',
            status: 'Проходит',
            recordingDate: new Date(2022, 9, 5),
            passageDate: new Date(2022, 9, 5),
            department: 2,
            selected: false,
          },
          {
            id: 5,
            fullName: 'Дмитриев Панкратий Владленович',
            post: 'Главный кладовщик',
            status: 'Проходит',
            recordingDate: new Date(2022, 9, 5),
            passageDate: new Date(2022, 9, 5),
            department: 2,
            selected: false,
          },
          {
            id: 6,
            fullName: 'Сорокин Мечеслав Вячеславович',
            post: 'Водитель',
            status: 'Проходит',
            recordingDate: new Date(2022, 9, 5),
            passageDate: new Date(2022, 9, 5),
            department: 2,
            selected: false,
          },
          {
            id: 7,
            fullName: 'Леонтьев Влас Игнатьевич',
            post: 'Водитель',
            status: 'Проходит',
            recordingDate: new Date(2022, 9, 5),
            passageDate: new Date(2022, 9, 5),
            department: 2,
            selected: false,
          },
          {
            id: 8,
            fullName: 'Рыбаков Нелли Дмитрьевич',
            post: 'Кладовщик',
            status: 'Проходит',
            recordingDate: new Date(2022, 9, 5),
            passageDate: new Date(2022, 9, 5),
            department: 2,
            selected: false,
          },
          {
            id: 9,
            fullName: 'Семёнов Петр Михайлович',
            post: 'Кладовщик',
            status: 'Проходит',
            recordingDate: new Date(2022, 9, 5),
            passageDate: new Date(2022, 9, 5),
            department: 2,
            selected: false,
          },
        ],
      },
    };
  },
  methods: {
    update(value) {
      this.searchValue = value;
    },
    departmentEmployeesCount(departmentId) {
      let count = 0;
      this.getEmployeesOfDepartment(departmentId)
        .forEach((employee) => {
          if (employee.department === departmentId) count += 1;
        });
      return count;
    },
    getAllEmployeesCount() {
      let count = 0;
      this.company.departments.forEach((department) => {
        this.getEmployeesOfDepartment(department.id)
          .forEach((employee) => {
            if (employee.department === department.id) count += 1;
          });
      });
      return count;
    },
    getEmployeesOfDepartment(departmentId) {
      const employees = [];
      this.company.employees.forEach((employee) => {
        if (employee.department === departmentId) employees.push(employee);
      });
      if (this.searchValue !== '') {
        return employees.filter((item) => item.fullName.toLowerCase()
          .includes(this.searchValue.toLowerCase()));
      }
      return employees;
    },
    formatDate(date) {
      const day = `0${date.getUTCDate()}`.slice(-2);
      const month = `0${date.getUTCMonth() + 1}`.slice(-2);
      const year = date.getUTCFullYear();
      return `${day}.${month}.${year}`;
    },
    deleteEmployee(employeeId) {
      const employeeToDelete = this.company.employees.find(
        (employee) => employee.id === employeeId,
      );
      const findIn = (data) => data.findIndex((employee) => employeeToDelete === employee);
      this.company.employees.splice(findIn(this.company.employees), 1);
      this.selected.splice(findIn(this.selected), 1);
    },
  },
  computed: {
    selectAll: {
      get() {
        const employeesToSelect = [];
        this.company.departments.forEach((department) => {
          employeesToSelect.push(this.getEmployeesOfDepartment(department.id));
        });
        return employeesToSelect
          ? this.selected.length === this.company.employees.length
          : false;
      },
      set(value) {
        const checked = [];
        if (value) {
          this.company.departments.forEach((department) => {
            this.getEmployeesOfDepartment(department.id)
              .forEach((employee) => {
                checked.push(employee);
              });
          });
        }
        this.selected = checked;
      },
    },
  },
};
</script>

<style lang="scss" scoped>
.employees {
  width: 100%;
  height: 100%;
}

.table {
  .table__count {
    width: 100%;
    padding-left: var(--left-padding-m);
    font-size: var(--large-text);
    line-height: var(--text-lh-s);
    border-bottom: 1px solid var(--gray);

    span {
      color: #000;
      font-size: inherit;
      line-height: var(--large-text-lh);
      font-weight: var(--xl);
    }

    @media screen and (max-width: 1280px) {
      padding-left: 0;
    }
  }

  &__row {
    max-width: 100%;
    display: grid;
    grid-template-columns:
      minmax(16px, 16px)
      minmax(138px, 236px)
      minmax(64px, 176px)
      minmax(57px, 111px)
      minmax(63px, 119px)
      minmax(63px, 329px)
      minmax(64px, 64px);
    padding: 11px 24px 8px 18px;
    border-bottom: 1px solid var(--gray);
    border-top: 1px solid var(--gray);
    grid-gap: 16px;
  }

  &__header {
    border-top: 0;
    padding: 27px 24px 8px 18px;
    color: var(--red);
    font-size: var(--small-text);
    line-height: var(--small-text-lh);
    font-weight: var(--s);

    .header__text-small {
      display: none;
    }

    @media screen and (max-width: 768px) {
      grid-template-columns: minmax(16px, 16px) 1fr;

      .table__cell:not(:first-child, :nth-child(2)) {
        display: none;
      }

      .header__text-large {
        display: none;
      }
      .header__text-small {
        display: block;
      }
    }
  }

  &__cell {
    display: flex;
    align-items: center;
    justify-content: flex-start;
  }

  &__department {
    &-body {
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: flex-start;
      padding: 20px 24px 5px 18px;
      border-bottom: 1px solid var(--gray);

      @media screen and (max-width: 1280px) {
        padding: 20px 18px 5px 18px;
      }
    }

    &-name,
    &-count {
      font-weight: var(--m);
      font-size: var(--large-text);
      line-height: var(--large-text-lh);
    }

    &-name {
      color: var(--black);
      margin-right: 8px;
    }

    &-count {
      color: var(--red);
    }

    &-buttons {
      .table__department-button {
        svg {
          transition: var(--transition);

          &:hover {
            color: var(--blue-darken);
          }
        }
      }

      .clicked {
        svg {
          transform: rotate(180deg);
        }
      }
    }

    &-employees {
      opacity: 0;
      max-height: 0;
      height: 100%;

      .employee {
        opacity: 0;
        transition: var(--transition);
        max-height: 0;
        display: none;
        height: 100%;
        padding: 12px 24px 7px 18px;
        border-top: 0;
        grid-template-areas: 'check name post status record passage buttons';

        .info {
          display: none;
          color: var(--red);
        }

        &__check {
          grid-area: check;
        }

        &__name {
          grid-area: name;
        }

        &__post {
          grid-area: post;
        }

        &__status {
          grid-area: status;
          color: var(--yellow);
        }

        &__record {
          grid-area: record;
        }

        &__passage {
          grid-area: passage;
        }

        &__buttons {
          grid-area: buttons;
        }

        &:last-child {
          border-bottom: 0;
        }

        @media screen and (max-width: 1280px) {
          padding: 20px 18px 5px 18px;
        }

        @media screen and (max-width: 768px) {
          grid-template-columns: minmax(16px, 55px) 1fr;
          grid-template-areas:
            'check name'
            '. post'
            '. status'
            '. record'
            'buttons passage';
          padding: 20px 18px;
          .button-group {
            justify-content: flex-start;
          }

          .info {
            display: block;
            min-width: 100px;
          }

          &__check {
            grid-area: check;
            width: 16px;
          }

          .table__cell {
            display: flex;
            align-items: center;
            justify-content: space-between;

            &:first-child {
              max-width: 16px;
            }
          }
        }

        @media screen and (max-width: 428px) {
          .employee__check {
            padding-top: 6px;
            align-items: flex-start;
          }
          .table__cell {
            span {
              text-align: left;
              height: 100%;
              vertical-align: top;
            }

            text-align: right;
          }
        }
      }

      &.shown {
        max-height: fit-content;
        opacity: 1;

        li {
          display: grid;
          opacity: 1;
          max-height: fit-content;
          height: 100%;
        }
      }
    }
  }
}

.button-group {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  flex: 1 1 0;

  button {
    height: 12px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    justify-self: flex-end;

    svg {
      color: var(--red);
      transition: var(--transition);
    }

    &:last-child {
      svg {
        color: var(--blue);
      }
    }

    &:nth-child(1) {
      margin-right: 10px;
    }

    &:nth-child(2) {
      margin-right: 12px;
    }
  }
}

.input {
  margin-left: var(--left-padding-m);
  margin-bottom: 30px;

  @media screen and (max-width: 1280px) {
    margin-left: 0;
  }
}
</style>
