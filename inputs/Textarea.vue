<script setup>
import { ref, onMounted } from 'vue';

const emits = defineEmits(['change']);
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'text' },
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

function update(e) {
	model.value = e.target.value;
	emits('change', e.target.value);
}
</script>
<template>
	<div class="form-input-wrapper">
		<textarea ref="input" v-model="model" class="form-textarea" :type="props.type" :name="props.name" :class="props.class" :placeholder="props.placeholder" @input="emits('change', update)" />
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
