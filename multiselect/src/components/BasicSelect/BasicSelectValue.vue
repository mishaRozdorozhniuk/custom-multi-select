<template>
  <div>
    <div class="select-container">
      <label class="select-label" for="selectIdArray">{{ label }} with array option</label>
      <select
          :value="selectedOption"
          @change="handleChange"
          class="custom-select"
          :disabled="disabled">
        <option :value="null" hidden disabled>{{ placeholder }}</option>
        <option v-for="option in arrayOfObjectOptions"
                :key="option.id"
                :value="option.id">
          {{ option.name }}
        </option>
      </select>
    </div>

    <div class="select-container">
      <label class="select-label" for="selectIdPrimitive">{{ label }} with primitive options</label>

      <select
          :value="selectedPrimitiveOption"
          @change="handleChangePrimitive"
          class="custom-select"
          :disabled="disabled">
        <option :value="null" hidden disabled>{{ placeholder }}</option>
        <option v-for="option in arrayOfPrimitiveOptions"
                :key="option">
          {{ option }}
        </option>
      </select>
    </div>
  </div>
</template>

<script>
import {ref} from 'vue';

export default {
  props: {
    disabled: {
      type: Boolean,
      default: false
    },
    placeholder: {
      type: String,
      required: true
    },
    label: {
      type: String,
      required: false
    },
  },
  setup() {
    const arrayOfObjectOptions = ref([
      { id: "1", name: "Label 1" },
      { id: "2", name: "Label 2" }
    ]);
    const arrayOfPrimitiveOptions = ref([1, "2", 3]);

    const selectedOption = ref(null);
    const selectedPrimitiveOption = ref(null);
    const handleChange = (event) => {
      selectedOption.value = event.target.value;
    };
    const handleChangePrimitive = (event) => {
      selectedPrimitiveOption.value = event.target.value;
    };

    return {
      arrayOfObjectOptions,
      selectedOption,
      arrayOfPrimitiveOptions,
      selectedPrimitiveOption,
      handleChange,
      handleChangePrimitive,
    };
  }
};
</script>

<style scoped>
.custom-select {
  width: 600px;
  padding: 15px;
  border-radius: 8px;
  border: 1px solid #ccc;
  transition: border-color 0.3s ease;
}

.custom-select:focus {
  border: 2px solid rgb(140,87,255);
}

.select-container {
  background-color: #fff;
  margin-top: 30px;
  border-radius: 5px;
  padding: 30px 30px 30px 15px;
  box-shadow: 0 10px 15px 4px rgba(0,0,0,0.1);
  display: flex;
  flex-direction: column;
}

.select-label {
  margin-bottom: 20px;
  font-weight: 600;
}
</style>
