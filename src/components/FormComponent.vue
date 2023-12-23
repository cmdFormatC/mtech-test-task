<template>
    <form class="form" @submit="submit">
      <div class="form__header">
          <h3 class="form__title">{{ componentProps.title }}</h3>
      </div>
      <div class="form__container">
        <h4 class="form__subtitle">{{ componentProps.subtitle }}</h4>
        <div :class="componentProps.inputBlocks.indexOf(inputBlock) === 0 ? 'form__input-block form__input-block_first' : 'form__input-block'"
          v-for="inputBlock in componentProps.inputBlocks" :key="componentProps.inputBlocks.indexOf(inputBlock)">
            <template v-for="inputElemet in inputBlock.inputs" :key="inputBlock.inputs.indexOf(inputElemet)">
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
      </div>
      <button type="submit" class="form__submit-button">создать</button>
    </form>
    <modal-window v-if="this.showModal" :modalData=componentProps.modalData :isVisible="showModal" @close="showModal = false" />
</template>
  
<script>
import SelectComponent from './SelectComponent.vue';
import SelectEmployeeComponent from '@/components/SelectEmployeeComponent.vue'
import TextInputComponent from './TextInputComponent.vue';
import ModalWindow from '@/components/ModalWindow.vue'

export default {
    props: ['componentProps'],
    components: {
        SelectComponent,
        SelectEmployeeComponent,
        TextInputComponent,
        ModalWindow,
    },
    data() {
        return {
            showInputs: true,
            inputVlaue: null,
            showModal: false,
            formData: {},
        }
    },
    methods: {
        submit(event) {
            event.preventDefault();
            console.log(this.formData);
            this.formData = {};
        },
        handleModalOpen() {
            this.showModal = true;
        },
        handleSelectOption(payload) {
            this.formData[payload.name] = payload.option.value;
        },
        handleUpdateInputValue(payload) {
            this.formData[payload.name] = payload.inputValue;
        }
    },
    computed: {
        isValid() {
            return 123
        }
    }
}
</script>

<style scoped lang="scss">
    @import '../assets/scss/variables.scss';
    .form {
        display: flex;
        flex-direction: column;
        padding-top: 50px;

        width: 600px;

        &__header {
            padding: 5px 10px;
            margin-right: auto;
            
            border-bottom: 1px solid $middle-purple;
        }

        &__title {
            font-size: $font-size-middle;
            color: $text-color;
            font-weight: 500;
            line-height: 1;

            text-transform: uppercase;

            margin: 0;
        }
        &__subtitle {
            font-size: $font-size-middle;
            color: $text-color;
            font-weight: 600;
            line-height: 1;

            text-align: left;

            margin: 40px 0 25px 0;
        }
        &__container {
            padding-left: 20px;
        }
        &__input-block {
            display: flex;
            flex-direction: column;

            gap: 20px;

            margin-bottom: 20px;

            &_first {
                padding: 0 40px 40px 0;
                border-bottom: 1px solid $lavender;
            }
        }

        &__submit-button{
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

            margin-left: auto;

            &:hover {
                background-color: $middle-purple;
            }
        }
    }
</style>