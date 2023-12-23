<template>
    <div :class="showOptions ? 'select select_oppened' : 'select'" ref="select" @click="toggleDropdown">
      <div class="select__img-container">
        <img class="select__img"  :src="selectedOption ? selectedOption.imgSrc ? selectedOption.imgSrc : this.avatarIcon : selectData.avatar"/>
      </div>
      <div class="select__inner">
        <span class="select__paceholder">
          {{ selectData.placeholder }}
        </span>
        <span class="select__paceholder_selected">
          {{ selectedOption ? selectedOption.text : 'Нет пользователя' }}
        </span>
        <div class="select__options" v-show="showOptions">
          <div
            v-for="option in selectData.options" 
            :key="option.value" 
            class="select__option"
            @click="selectOption(option)"
          >
            <div class="select__option-img-container">
              <img class="select__option-img" :src="option.imgSrc ? option.imgSrc : this.avatarIcon" alt="лого">
            </div>
            
            <span class="select__option-text"> 
              {{ option.text }}
            </span>
          </div>
          
        </div>
      </div>
      <img class="select__add-icon" :src="plusIcon" @click="handleAddClick"/>
    </div>
</template>
  
  
<script>
import plusIcon from '@/assets/icons/plus.svg'
import avatarIcon from '@/assets/icons/avatar.svg'
export default {
    props: {
      onClick: {
        type: Function,
        default: () => {}
      },
      selectData: {
        type: Object,
      }
    },
    data() {
        return {
            showOptions: false,
            selectedOption: null,
            plusIcon: plusIcon,
            avatarIcon: avatarIcon,
        }
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
      },
      handleAddClick(event) {
        event.stopPropagation();
        if (this.selectData.event) {
          this.$emit(this.selectData.event);
        }
      }
    },
    mounted() {
        window.addEventListener('click', this.handleClickOutside);
    },
    beforeUnmount() {
        window.removeEventListener('click', this.handleClickOutside);
    }
}
</script>

<style scoped lang="scss">
@import '../assets/scss/variables.scss';

.select {
    color: $manatee;
    font-size: $font-size-small;
    line-height: 1;
    
    position: relative;
    display: flex;
    align-items: center;

    border: 1px solid $white-smoke;
    border-radius: $border-radius-tiny;

    height: $inputHeight;
    min-width: $inputMinWidth;

    cursor: pointer;

    text-align: left;

    box-sizing: border-box;

    -webkit-user-select: none;
    -ms-user-select: none;
    user-select: none;

    &__inner {
        display: flex;
        flex-direction: column;
        gap: 3px;
    }
    &_oppened {
        border-bottom-color: transparent;
        border-radius: $border-radius-tiny $border-radius-tiny 0 0 ;
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
        
        border: 1px solid $white-smoke;
        border-bottom: none;
        border-radius: 0 0 $border-radius-tiny $border-radius-tiny;

        background-color: $white;
        z-index: 4;
    }

    &__option {
        display: flex;
        gap: 10px;

        padding: 13px 10px;
        height: $inputHeight;

        border-bottom: 1px solid $white-smoke;

        text-align: left;

        box-sizing: border-box;

        &:hover {
            color: $text-color;
            background-color: $white-smoke;
        }
    }
    &__option-img-container {
      border-radius: 50%;
      width: 13px;
      height: 13px;
      overflow: hidden;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    &__option-img {
      max-width: 20px;
      max-height: 20px;
      height: auto;
      width: auto;

    }
    &__img-container {
      border-radius: 50%;
      width: 13px;
      height: 13px;
      overflow: hidden;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 10px;
    }
    &__img {
        max-width: 20px;
        max-height: 20px;
        height: auto;
        width: auto;

    }
    &__add-icon {
      width: 10px;
      height: 10px;
      margin-left: auto;
      padding: 10px;
    }

}
</style>