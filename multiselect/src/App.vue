<template>
  <div class="selects-wrapper">
    <h1>Custom Selects</h1>
    <div class="selects-inner">
      <div>
        <BasicSelect
            :disabled="false"
            placeholder="Standard"
            label="v-model select"
            />
      </div>
      <div>
        <BasicSelectValue
            :disabled="false"
            placeholder="Standard"
            label="value select" />
      </div>
    </div>
  </div>
</template>

<script>
import BasicSelect from '@/components/BasicSelect/BasicSelect.vue';
import BasicSelectValue from "@/components/BasicSelect/BasicSelectValue.vue";

export default {
  components: {
    BasicSelect,
    BasicSelectValue,
  },
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
  justify-content: center;
}
</style>