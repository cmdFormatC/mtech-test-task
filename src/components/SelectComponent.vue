<template>
    <div :class="showOptions ? 'select select_oppened' : 'select'" ref="select" @click="toggleDropdown">
      <span :class="selectedOption ? 'select__paceholder select__paceholder_selected' : 'select__paceholder'">
        {{ selectedOption ? selectedOption.text : selectData.placeholder }}
      </span>
      <div class="select__options" v-show="showOptions">
        <span class="select__option" 
             v-for="option in selectData.options" 
             :key="option.value" 
             @click="selectOption(option)">
          {{ option.text }}
        </span>
      </div>
    </div>
</template>
  
  
<script>
export default {
  props: {
    selectData: Object,
    value: Object
  },
  data() {
    return {
      selectedOption: null,
      showOptions: false,
    };
  },
  methods: {
    toggleDropdown() {
      this.showOptions = !this.showOptions;
    },
    selectOption(option) {
      this.selectedOption = option;
      this.$emit('selectOption', {name: this.selectData.name, option})
    },
    handleClickOutside(event) {
      if (this.showOptions && !this.$refs.select.contains(event.target)) {
        this.showOptions = false;
      }
    }
  },
  mounted() {
    window.addEventListener('click', this.handleClickOutside);
  },
  beforeUnmount() {
    window.removeEventListener('click', this.handleClickOutside);
  }
};
</script>

<style scoped lang="scss">
@import '../assets/scss/variables.scss';

.select {
    color: $manatee;
    font-size: $font-size-small;
    position: relative;
    line-height: 1;
    border: 1px solid $lavender;
    border-radius: $border-radius-medium;

    padding: 13px 10px;

    height: $inputHeight;
    min-width: $inputMinWidth;

    cursor: pointer;

    text-align: left;

    box-sizing: border-box;

    -webkit-user-select: none;
    -ms-user-select: none;
    user-select: none;

    &::after {
        content: '';
        display: block;
        position: absolute;

        top: 50%;
        transform: translateY(-50%);
        right: 10px;

        background-image: url('../assets/icons/dropdown.svg');
        width: 7.5px;
        height: 7.5px;

        z-index: 1;

        transition: transform 0.2s ease;
    }

    &_oppened {
        border-bottom: none;

        border-radius: $border-radius-medium $border-radius-medium 0 0 ;

        &::after {
          transform: translateY(-50%) rotate(180deg);
          transform-origin: center;
        }
    }

    &__paceholder {
        &_selected {
            color: $text-color;
        }
    }

    &__options {
        position: absolute;
        top: 39px;
        left: -1px;

        width: 100%;

        border: 1px solid $lavender;
        border-bottom: none;
        border-radius: 0 0 $border-radius-medium $border-radius-medium;

        background-color: $white;
        z-index: 4;
    }

    &__option {
        display: block;

        padding: 13px 10px;
        height: $inputHeight;

        border-bottom: 1px solid $lavender;

        text-align: left;

        box-sizing: border-box;

        &:hover {
            color: $text-color;
            background-color: $lavender;
        }
    }

}
</style>