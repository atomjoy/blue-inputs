<script setup>
const emits = defineEmits(['change']);
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'selector_onoff' },
	off: { type: String, default: 'Off' },
	on: { type: String, default: 'On' },
	class: { type: [String, Array, Object] },
});

function toggle() {
	model.value = !model.value;
	emits('change', !model.value);
}
</script>
<template>
	<div class="form-input-wrapper">
		<div class="form-selector" :class="props.class">
			<div class="form-selector-item form-selector-item-onoff" @click="toggle" :class="{ 'form-selector-item-selected form-selector-item-selected-onoff': !model }">{{ props.off }}</div>
			<div class="form-selector-item form-selector-item-onoff" @click="toggle" :class="{ 'form-selector-item-selected form-selector-item-selected-onoff': model }">{{ props.on }}</div>
		</div>
		<input v-model="model" type="hidden" :name="props.name" @change="emits('change', $event.target.value)" />
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
