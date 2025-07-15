<script setup>
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'Button' },
	value: { type: String, default: '' },
});
</script>
<template>
	<div class="form-selector-item form-selector-slot-button" :class="{ 'form-selector-item-selected': model == props.value }">
		<slot>{{ props.name }}</slot>
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
