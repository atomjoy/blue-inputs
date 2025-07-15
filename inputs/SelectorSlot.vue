<script setup>
const emits = defineEmits(['change']);
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'selector_slot' },
	class: { type: [String, Array, Object] },
});

function onClick(id) {
	model.value = id;
	emits('change', id);
}
</script>
<template>
	<div class="form-input-wrapper">
		<div class="form-selector" :class="props.class">
			<slot name="default" :onClick="onClick"></slot>
		</div>
		<input v-model="model" type="hidden" :name="props.name" @change="emits('change', $event.target.value)" />
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
