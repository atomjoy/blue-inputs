<script setup>
import Info from './Info.vue';

const props = defineProps({
	text: { type: String, default: 'Label' },
	for: { type: String, default: '' },
	info: { type: String, default: '' },
});
</script>
<template>
	<label class="form-input-label" :for="props.name">
		<span class="form-input-label-text">{{ props.text }}</span>
		<Info :message="props.info">
			{{ props.info }}
		</Info>
		<slot></slot>
	</label>
</template>
<style>
@import url('./css/inputs.css');
</style>
