<template>
  <div class="selects-wrapper">
    <h1 class="custom-select-title">Custom Selects</h1>
    <div class="selects-variants">
      <MySelect
          :default="arrayOfObjectOptions"
          :is-object="true"
          :tags="true"
          label="Tags select with array"
          placeholder="Choose value..."
          label-prop="name"
          value-prop="id"
          select-styles="select-menu-max-height"
          @changed="handleSelectChange"
          @selected="handleSelect"
          @deselected="handleDeselect"
      />
      <MySelect
          :default="arrayOfObjectOptions"
          :is-object="true"
          :multiple="true"
          label="Multi select with array"
          placeholder="Choose value..."
          label-prop="name"
          value-prop="id"
          select-styles="select-menu-max-height"
          @changed="handleSelectChange"
          @selected="handleSelect"
          @deselected="handleDeselect"
      />
    </div>
    <div class="selects-variants">
      <MySelect
          :default="arrayOfPrimitive"
          :is-object="true"
          :tags="true"
          label="Tags select with primitive"
          placeholder="Choose value..."
          label-prop="name"
          value-prop="id"
          select-styles="select-menu-max-height"
          @changed="handleSelectChange"
          @selected="handleSelect"
          @deselected="handleDeselect"
      />
      <MySelect
          :default="arrayOfPrimitive"
          :is-object="true"
          :multiple="true"
          label="Multi select with primitive"
          placeholder="Choose value..."
          label-prop="name"
          value-prop="id"
          select-styles="select-menu-max-height"
          @changed="handleSelectChange"
          @selected="handleSelect"
          @deselected="handleDeselect"
      />
    </div>
    <div class="selects-variants">
      <MySelect
          :default="arrayOfObjectOptions"
          :is-object="true"
          :multiple="false"
          label="Single select with array"
          placeholder="Choose value..."
          label-prop="name"
          value-prop="id"
          select-styles="select-menu-max-height"
          @changed="handleSelectChange"
          @selected="handleSelect"
          @deselected="handleDeselect"
      />
      <MySelect
          :default="arrayOfPrimitive"
          :is-object="true"
          :multiple="false"
          label="Single select with primitive"
          placeholder="Choose value..."
          label-prop="name"
          value-prop="id"
          select-styles="select-menu-max-height"
          @changed="handleSelectChange"
          @selected="handleSelect"
          @deselected="handleDeselect"
      />
    </div>
    <div class="selects-variants">
      <MySelect
          :default="arrayOfObjectOptions"
          :is-object="true"
          :hideSelected="true"
          :multiple="true"
          label="Hide selected option"
          placeholder="Choose value..."
          label-prop="name"
          value-prop="id"
          select-styles="select-menu-max-height"
          @changed="handleSelectChange"
          @selected="handleSelect"
          @deselected="handleDeselect"
      />
      <MySelect
          :default="arrayOfObjectOptions"
          :is-object="true"
          :disabled="true"
          label="Disable select"
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
.selects-variants {
  display: grid;
  gap: 20px;
  grid-template-columns: 1fr 1fr;
  margin-bottom: 450px;
}

.selects-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.custom-select-title {
  margin-bottom: 20px;
}
</style>