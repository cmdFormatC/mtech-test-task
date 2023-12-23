<template>
    <div class="text">
        <input 
            :placeholder="textData.placeholder" 
            :id="inputId" class="text__input" 
            :type="textData.inputStyle" 
            @change="handleInputChange" 
            v-model="inputValue"
            @input="validateInput"
        >
        <label class="text__lable"  
            :for="inputId">{{ textData.label ? textData.label : ''}}
        </label>
        <button 
            v-if="inputValue" 
            @click="handleInputClear" 
            class="text__clear" type="button">
        </button>
    </div>
</template>

<script>
export default {
    props: ['textData'],
    data() {
        return {
            inputId: `textInput-${Date.now()}-${Math.random().toString(36).substr(2, 9)}`,
            inputValue: '',
        }
    },
    methods: {
        handleInputChange() {
            this.$emit('inputChange', { name: this.textData.name, inputValue: this.inputValue });
        },
        validateInput() {
            if (this.textData.inputStyle === 'number') {
                if (this.inputValue > 100) {
                    this.inputValue = 100; 
                } else if (this.inputValue < 0) {
                    this.inputValue = 0;
                }
            }
        },
        handleInputClear() {
            this.inputValue = '';
        }
    }
}
</script>

<style lang="scss">
@import '../assets/scss/variables.scss';

.text {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    position: relative;


    &__input {
        color: $text-color;
        font-size: $font-size-small;
        line-height: 1;

        display: block;
        
        height: $inputHeight;
        width: 100%;
        min-width: $inputMinWidth;

        border: 1px solid $lavender;
        border-radius: $border-radius-medium;

        margin: 0;
        padding: 13px 10px;

        box-sizing: border-box;
        
        &::placeholder, &::-moz-placeholder, &:-ms-input-placeholder {
            color: $manatee;
        }

        &:focus {
            outline: none;
        }
    }
    &__clear {
        position: absolute;

        top: 12.5px;
        right: 12.5px;

        height: 12.5px;
        width: 12.5px;

        padding: 0;

        border: none;

        background: transparent;

        cursor: pointer;

        background-image: url('../assets/icons/cancel.svg');
    }
    &__lable {
        color: $manatee;
        font-size: $font-size-tiny;
        line-height: 1;

        margin: 5px 0 0 10px;

        &:empty {
            display: none;
        }
    }
}
input[type="number"]::-webkit-inner-spin-button, 
input[type="number"]::-webkit-outer-spin-button { 
  -webkit-appearance: none;
  margin: 0; 
}

input[type="number"] {
  -moz-appearance: textfield;
}

input[type="number"]::-ms-clear,
input[type="number"]::-ms-reveal {
  display: none;
}

</style>