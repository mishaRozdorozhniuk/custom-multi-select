<template>
  <div>
    <div class="select-container">
      <label class="select-label" for="selectIdArray">{{ label }} with array option</label>
      <select multiple id="selectIdArray" v-model="selectedOption" class="custom-select" :disabled="disabled">
        <option :value="null" hidden disabled>{{ placeholder }}</option>
        <option v-for="option in arrayOfObjectOptions"
                :key="option.id"
                :value="option.id">
          {{ option.name }}
        </option>
      </select>
    </div>
<!--    <div class="select-container">-->
<!--      <label class="select-label" for="selectIdPrimitive">{{ label }} with primitive options</label>-->
<!--      <select id="selectIdPrimitive" v-model="selectedOptionBinding" class="custom-select" :disabled="disabled">-->
<!--        <option :value="null" hidden disabled>{{ placeholder }}</option>-->
<!--        <option v-for="option in arrayOfPrimitiveOptions"-->
<!--                :key="option"-->
<!--                :value="option">-->
<!--          {{ option }}-->
<!--        </option>-->
<!--      </select >-->
<!--    </div>-->
  </div>
</template>

<script>
import {onUpdated, ref} from 'vue';

export default {
  props: {
    disabled: {
      type: Boolean,
      default: false
    },
    placeholder: {
      type: String,
      required: null
    },
    label: {
      type: String,
      required: null
    },
  },
  setup() {
    const arrayOfObjectOptions = ref([
      { id: "1", name: "Label 1" },
      { id: "2", name: "Label 2" },
      { id: "3", name: "Label 2"},
      { id: "4", name: "Label 2" },
      { id: "5", name: "Label 2" },
      { id: "6", name: "Label 2" },
      { id: "7", name: "Label 2" },
      { id: "8", name: "Label 2" },
      { id: "9", name: "Label 2" },
    ]);


    const arrayOfPrimitiveOptions = ref([1, "2", 3]);



    onUpdated(() => {
      console.log(selectedOption.value)
    })

    const selectedOptionBinding = ref(null);

    return {
      arrayOfObjectOptions,
      selectedOption,
      arrayOfPrimitiveOptions,
      selectedOptionBinding
    };
  },
  updated() {
    console.log(this.selectedOption.value)
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
