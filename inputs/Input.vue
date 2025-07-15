<script setup>
import { ref, onMounted } from 'vue';

const emits = defineEmits(['change']);
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'text' },
	type: { type: String, default: 'text' },
	class: { type: [String, Array, Object] },
	placeholder: { type: String },
	focus: false,
});

let input = ref(null);

onMounted(() => {
	if (props.focus) {
		input.value.focus();
	}
});
</script>
<template>
	<div class="form-input-wrapper">
		<input ref="input" v-model="model" class="form-input" :type="props.type" :name="props.name" :class="props.class" :placeholder="props.placeholder" @change="emits('change', $event.target.value)" />
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
