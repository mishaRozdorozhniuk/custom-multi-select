<template>
  <div class="selects-wrapper">
    <h1>Custom Selects</h1>
    <div class="selects-inner">
      <MySelect
          :default="arrayOfObjectOptions"
          :is-object="true"
          :multiple="false"
          :tags="false"
          :hideSelected="false"
          :disabled="false"
          label="Custom select"
          placeholder="Choose value..."
          label-prop="name"
          value-prop="id"
          select-styles="select-menu-max-height"
          @changed="handleSelectChange"
          @selected="handleSelect"
          @deselected="handleDeselect"
      />
    </div>
  </div>
</template>

<script>
import MySelect from "@/components/MySelect/MySelect.vue";
import {ref} from "vue";

export default {
  components: {
    MySelect,
  },
  setup() {
    const arrayOfObjectOptions = ref([
      {id: "1", name: "Label 1"},
      {id: "2", name: "Label 2"},
      {id: "3", name: "Label 3"},
      {id: "4", name: "Label 4"},
      {id: "5", name: "Label 5"},
      {id: "6", name: "Label 6"},
      {id: "7", name: "Label 7"},
      {id: "8", name: "Label 8"},
      {id: "9", name: "Label 9"},
      {id: "10", name: "Label 10"},
    ]);

    const arrayOfPrimitive = ref([
        '1', '2', '3', '4', '5'
    ])

    const handleSelectChange = (option) => {
      console.log(option)
    }

    const handleSelect = (option) => {
      console.log(option)
    }

    const handleDeselect = (option) => {
      console.log(option)
    }

    return {
      arrayOfObjectOptions,
      arrayOfPrimitive,
      handleSelect,
      handleSelectChange,
      handleDeselect
    }
  }
};
</script>

<style scoped>
.selects-inner {
  display: flex;
  gap: 20px;
}

.selects-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>