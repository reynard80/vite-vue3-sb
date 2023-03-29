<template>
  <button type="button" :class="classes" @click="onClick" :style="style">{{ label }} </button>
</template>

<script lang="ts" setup>
import './button.css';
import { computed } from 'vue';

const props = withDefaults(defineProps<{
  /**
   * The label of the button
   */
  label: string,
  /**
   * primary or secondary button
   */
  primary?: boolean,
  /**
   * size of the button
   */
  size?: 'small' | 'medium' | 'large',
  /**
   * background color of the button
   */
  backgroundColor?: string,
}>(), { primary: false });

const emit = defineEmits<{
  (e: 'input', value: boolean): void;
  (e: 'update:active-tab', value: number): void;
  (e: 'update:active-step', value: number): void;
  (e: 'submit'): void;
  (e: 'close'): void;
}>();

const classes = computed(() => ({
  'storybook-button': true,
  'storybook-button--primary': props.primary,
  'storybook-button--secondary': !props.primary,
  [`storybook-button--${props.size || 'medium'}`]: true,
}));

const style = computed(() => ({
  backgroundColor: props.backgroundColor
}));

const onClick = () => {
  emit('input', true)
  emit('update:active-step', 22)
  emit('close')
};
</script>
