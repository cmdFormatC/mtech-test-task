<template>
  <div v-if="isVisible" class="modal" @click.self="closeModal">
    <form class="modal__container" @submit.prevent="submit">
      <h3>{{ modalData.title }}</h3>
      <div class="modal__inputs">
        <template v-for="inputElemet in modalData.inputs" :key="modalData.inputs.indexOf(inputElemet)">
          <SelectEmployeeComponent
            v-if="inputElemet.inputStyle === 'select-employ'"
            :selectData="inputElemet"
            @openModal="handleModalOpen"
            @selectOption="handleSelectOption"
          />
          <SelectComponent 
            v-if="inputElemet.inputStyle === 'select'"
            @selectOption="handleSelectOption"
            :selectData="inputElemet" 
          />
          <text-input-component
            v-if="inputElemet.inputStyle === 'text' || inputElemet.inputStyle === 'number'"
            :textData="inputElemet"
            @inputChange="handleUpdateInputValue"
          />
        </template>
      </div>
      <div class="modal__footer">
        <button type="reset" class="modal__cancel-button" @click="closeModal">Отмена</button>
        <button type="submit" class="modal__create-button">Создать</button>
      </div>
    </form>
  </div>
</template>
  
<script>
import SelectComponent from './SelectComponent.vue';
import SelectEmployeeComponent from './SelectEmployeeComponent.vue'
import TextInputComponent from './TextInputComponent.vue';
export default {
  props: {
    isVisible: {
      type: Boolean,
      required: true
    },
    modalData: {
      type: Object
    },

  },
  components: {
    SelectComponent,
    SelectEmployeeComponent,
    TextInputComponent,
  },
  data() {
    return {
      formData: {},
    }
  },
  methods: {
    closeModal() {
      this.$emit('close', false);
    },
    handleModalOpen() {
      console.log('Кнопка нажата');
    },
    submit(event) {
        event.stopPropagation()
        console.log(this.formData);
        this.formData = {};
        this.closeModal();
    },
    handleSelectOption(payload) {
        this.formData[payload.name] = payload.option.value;
    },
    handleUpdateInputValue(payload) {
        this.formData[payload.name] = payload.inputValue;
    }
  }
};
</script>

<style lang="scss">
@import '../assets/scss/variables.scss';

.modal {
  display: flex;
  justify-content: center;
  align-items: center;

  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;

  background-color: rgba(0, 0, 0, 0.5);

  z-index: 5;

  &__container {
    display: flex;

    flex-direction: column;

    background: $white;

    width: 600px;
    padding: 40px;

    border-radius: $border-radius-medium;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.25);
    z-index: 6;

  }
  &__inputs {
    display: flex;

    flex-direction: column;
    flex-wrap: wrap;


    max-height: 300px;

    gap: 10px;

    margin: 20px 0 20px 0;
  }

  &__footer {
    display: flex;
    gap: 10px;
    margin-left: auto;
  }

  &__cancel-button {
    color: $manatee;
    font-size: $font-size-middle;
    line-height: 1;
    text-transform: uppercase;
    font-weight: 600;

    cursor: pointer;

    background: transparent;

    border: none;

    &:hover {
      color: $text-color;
    }
  }

  &__create-button {
    color: $white;
    font-size: $font-size-middle;
    line-height: 1;
    text-transform: uppercase;
    font-weight: 600;

    background-color: $lavender;

    border: none;
    padding: 7.5px 5px;
    border-radius: $border-radius-small;

    cursor: pointer;

    &:hover {
      background-color: $middle-purple;
    }
  }
}

</style>
  