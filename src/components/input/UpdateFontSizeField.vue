<template>
  <div class="flex items-center">
    <InputField
      class="mr-[18px] w-[42px]"
      :modelValue="size"
      @update:modelValue="updateSize"
      :clearable="false"
      :maxLength="2"
      :mask="'[0-9]'"
      :placeholder="size"
    >
      <template #postfix>px</template>
    </InputField>
    <SlideBar
      class="flex-1"
      v-model="size"
      :min="MIN_FONT_SIZE"
      :max="MAX_FONT_SIZE"
    />
  </div>
</template>

<script lang="ts" setup>
import { MAX_FONT_SIZE, MIN_FONT_SIZE } from 'src/constants';
import { useFontStore } from 'src/store/font';
import InputField from './InputField.vue';
import SlideBar from './SlideBar.vue';

const store = useFontStore();
const { size } = storeToRefs(store);

const updateSize = (newSize: string) => {
  const parsedSize = parseInt(newSize || '0');
  const isInvalidSize =
    parsedSize < MIN_FONT_SIZE || MAX_FONT_SIZE < parsedSize;

  if (isInvalidSize) {
    return;
  }

  size.value = newSize;
};
</script>
