<script setup>
import IconCopy from './icons/IconCopy.vue';
import IconEyeOpen from './icons/IconEyeOpen.vue';
import IconEyeClosed from './icons/IconEyeClosed.vue';
import { ref, onMounted } from 'vue';

const emits = defineEmits(['change', 'invalid', 'valid']);
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'text' },
	class: { type: [String, Array, Object] },
	placeholder: { type: String },
	focus: { type: Boolean, default: false },
	show: { type: Boolean, default: false },
	copy: { type: Boolean, default: true },
});

let input = ref(null);
let show = ref(false);

onMounted(() => {
	if (props.focus) {
		input.value.focus();
	}
	show.value = props.show;
});

function toggle() {
	show.value = !show.value;
	if (input.value.type != 'password') {
		input.value.type = 'password';
	} else {
		input.value.type = 'text';
	}
}

function copyClipboard() {
	navigator.clipboard.writeText(input.value.value);
}
</script>
<template>
	<div class="form-input-wrapper">
		<input ref="input" v-model="model" class="form-input form-password" type="password" :name="props.name" :class="props.class" :placeholder="props.placeholder" @change="emits('change', $event.target.value)" />
		<span title="Copy">
			<IconCopy v-if="props.copy" class="form-input-copy" @click="copyClipboard" />
		</span>
		<div class="form-input-icon" @click="toggle">
			<IconEyeClosed v-if="!show" />
			<IconEyeOpen v-if="show" />
		</div>
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
