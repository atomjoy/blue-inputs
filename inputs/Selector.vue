<script setup>
const emits = defineEmits(['change']);
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'selector' },
	options: { type: Array, default: [] },
	class: { type: [String, Array, Object] },
});

function update(id) {
	model.value = id;
	emits('change', id);
}
</script>
<template>
	<div class="form-input-wrapper">
		<div class="form-selector" :class="props.class">
			<div class="form-selector-item" v-for="i in props.options" @click="update(i)" :class="{ 'form-selector-item-selected': model.toLowerCase() == i.toLowerCase() }">{{ i }}</div>
		</div>
		<input v-model="model" type="hidden" :name="props.name" @change="emits('change', $event.target.value)" />
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
