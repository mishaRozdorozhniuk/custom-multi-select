<template>
  <div class="select">
    <label>{{ label }}</label>
    <div class="select-input"
         tabindex="0"
         :class="[disabled ? 'select-disabled' : '', isMenuOpen ? 'menu-opened' : '']"
         @click.stop="handleMenuOpen">
      <span v-if="!multiple && !tags">
        {{selectValue}}
        <span v-show="!selectValue && !selectedOptions.length" class="placeholder">{{placeholder}}</span>
      </span>
      <div v-else class="select-multiple-wrapper">
        <div :class="tags && 'select-tags'"
             @click.stop
             @mouseenter="tags && handleShowCross(option)"
             @mouseleave="tags && handleShowCross(null)"
             v-for="option in selectedOptions"
             :key="isArrayOfObjects(option, valueProp)">
          <span class="selected-option">
            {{option}}
          </span>
          <span v-if="tags"
                class="tags-cross"
                @click="removeSelectedOption(option)" :class="getCrossVisible(option)" />
        </div>
        <span v-show="!selectValue && !selectedOptions.length" class="placeholder">{{placeholder}}</span>
      </div>
    </div>
    <div class="select__menu" :class="isMenuOpen ? `select__menu-hidden` : `select__menu-show  ${selectStyles}`">
      <ul>
        <li v-for="option in optionsCopy"
            :key="isArrayOfObjects(option, valueProp)"
            @click="(!multiple && !tags) && handleChange(option)"
            class="select-item">
          <label v-show="multiple || tags" class="custom-checkbox">
            <input type="checkbox" @change="handleMultipleOptionChange(option)" :checked="isChecked(option)">
            <span class="checkmark"></span>
          </label>
          <span :class="{ 'selected-text': isChecked(option) }">{{ isArrayOfObjects(option, labelProp )}}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import {ref, toRaw} from "vue";

export default {
  props: {
    selectStyles: {
      type: String,
      default: '',
      required: false
    },
    isObject: {
      type: Boolean,
      default: false,
      required: false
    },
    default: {
      type: Array,
      default: [],
      required: true
    },
    valueProp: {
      type: String,
      required: false,
      default: "id"
    },
    labelProp: {
      type: String,
      required: false,
      default: "label"
    },
    multiple: {
      type: Boolean,
      required: false,
      default: false
    },
    tags: {
      type: Boolean,
      required: false,
      default: false
    },
    hideSelected: {
      type: Boolean,
      required: false,
      default: false
    },
    placeholder: {
      type: String,
      required: true,
      default: null
    },
    label: {
      type: String,
      required: false,
      default: null
    },
    disabled: {
      type: Boolean,
      required: false,
      default: false
    },
    search: {
      type: Boolean,
      required: false,
      default: false
    }
  },
  setup(props, context) {
    const optionsCopy = ref(JSON.parse(JSON.stringify(props.default)))
    const isMenuOpen = ref(true)
    const selectedOptions = ref([]);
    const selectValue = ref('')
    const hoveredOption = ref(null)
    const handleMenuOpen = () => {
      isMenuOpen.value = !isMenuOpen.value;
    };

    const isArrayOfObjects = ((option, valueProp = props.valueProp) => {
      if(props.isObject && typeof option === 'object' && option !== null) {
        return option[valueProp]
      } else {
        return option
      }
    })
    const handleMultipleOptionChange = (option) => {
      const oldValue = selectedOptions.value[selectedOptions.value.length  - 1];
      const newOption = isArrayOfObjects(option, props.labelProp)

      context.emit('changed', { oldValue, newValue: toRaw(option) });

      if (!selectedOptions.value.includes(newOption)) {
        selectedOptions.value.push(newOption);
        context.emit('selected', toRaw(option))
      } else {
        selectedOptions.value = selectedOptions.value.filter(el => el !== newOption);
        context.emit('deselected', toRaw(option))
      }

      if(props.hideSelected) {
        optionsCopy.value = optionsCopy.value.filter(el => isArrayOfObjects(el, props.labelProp) !== newOption)
      }
    };
    const handleChange = (option) => {
      const oldValue = selectValue.value;
      const newOption = isArrayOfObjects(option, props.labelProp);
      selectValue.value = newOption;

      context.emit('changed', { oldValue, newValue: toRaw(option) });

      if (!props.multiple) {
        handleMenuOpen();
      }
    }
    const getCrossVisible = (option) => {
      const crossVisible = option?.[props.valueProp] ?? option
      return crossVisible === hoveredOption.value ? 'tags-cross-visible' : ''
    }
    const handleShowCross = (option) => {
      hoveredOption.value = option?.[props.valueProp] ?? option
    }
    const removeSelectedOption = (option) => {
      const newOption = isArrayOfObjects(option, props.labelProp)
      selectedOptions.value = selectedOptions.value.filter(el => isArrayOfObjects(el, props.labelProp) !== newOption)

      if(props.hideSelected) {
        const foundedOption = props.default.find(el => isArrayOfObjects(el, props.labelProp) === option)

        context.emit('deselected', toRaw(foundedOption))
        optionsCopy.value.push(foundedOption)
        optionsCopy.value.sort((a, b) => {
          return isArrayOfObjects(a, props.valueProp) - isArrayOfObjects(b, props.valueProp);
        });
      }
    }
    const isChecked = (option) => {
      const newOption = isArrayOfObjects(option, props.labelProp)
      return selectedOptions.value.some(el => isArrayOfObjects(el, props.labelProp) === newOption)
    }

    return {
      optionsCopy,
      isMenuOpen,
      handleMenuOpen,
      handleMultipleOptionChange,
      handleChange,
      selectValue,
      isArrayOfObjects,
      selectedOptions,
      handleShowCross,
      getCrossVisible,
      removeSelectedOption,
      isChecked,
    }
  }
}
</script>

<style scoped>
@import "MySelect.css";
</style>
