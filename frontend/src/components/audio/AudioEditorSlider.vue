<template>
  <div v-if="vertical" class="flex-center column gap-2">
    <q-slider
      :model-value="modelValue"
      :min="min"
      :max="max"
      label
      switch-label-side
      vertical
      v-bind="$attrs"
      @update:model-value="$emit('update:model-value', $event)"
    />
    <div v-if="label" class="text-caption">{{ label }}</div>
  </div>

  <div v-else class="flex items-center gap-4">
    <div v-if="label" class="flex-center-end" style="width: 120px">
      {{ label }}
    </div>
    <q-item class="row gap-3 items-center" style="width: 200px">
      <q-item-section>
        <q-slider
          :model-value="modelValue"
          :min="min"
          :max="max"
          label
          switch-label-side
          v-bind="$attrs"
          @update:model-value="$emit('update:model-value', $event)"
        />
      </q-item-section>
      <q-item-section v-if="$slots.append" class="no-padding q-ml-sm" side>
        <slot name="append" />
      </q-item-section>
    </q-item>

    <BaseButton icon="restart_alt" tooltip="Reset field" @click="reset" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'AudioEditorSlider',

  props: {
    modelValue: {
      type: Number,
      default: 50,
    },
    max: {
      type: Number,
      default: 100,
    },
    min: {
      type: Number,
      default: 0,
    },
    label: {
      type: [Number, String],
      default: null,
    },

    vertical: Boolean,
  },

  emits: ['update:model-value'],

  setup(props, { emit }) {
    const defaultValue = ref(props.modelValue);
    function reset() {
      emit('update:model-value', defaultValue.value);
    }

    return {
      reset,
    };
  },
});
</script>
