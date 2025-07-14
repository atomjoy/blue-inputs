<script setup>
import { computed } from 'vue';

const emits = defineEmits(['change']);
const model = defineModel({ required: true, type: [Boolean, Array] });
const props = defineProps({
	name: { type: String },
	value: { type: String, required: true },
	label: { type: String, default: '' },
});

const checked = computed(() => {
	if (model.value instanceof Array) {
		return model.value.includes(props.value);
	}
	return model.value;
});

function hash(s) {
	return s.split('').reduce(function (a, b) {
		a = (a << 5) - a + b.charCodeAt(0);
		return a & a;
	}, 0);
}
</script>

<template>
	<div class="form-checkbox-line">
		<input :id="hash(props.value)" class="form-checkbox form-checkbox-onoff" type="checkbox" v-model="model" :value="props.value" :name="props.name" :class="props.class" :placeholder="props.placeholder" @change="emits('change', $event)" />
		<div :class="{ 'form-checkmark-onoff': true, 'form-checkmark-onoff-checked': checked }">
			<div class="dot"></div>
		</div>
		<label class="form-checkbox-onoff-label" :for="hash(props.value)" v-if="props.label">{{ props.label }}<slot /></label>
	</div>
</template>

<style>
@import url('./css/inputs.css');
</style>

<!--
	// Multiple Array with strings values
	let settings = ref(['email','sms']) // Default selected in array
	<CheckboxOnOff value="email" v-model="settings" name="settings[]">Email</Label>
	<CheckboxOnOff value="sms" v-model="settings" name="settings[]">Sms</Label>

	// Single (true|false)
	let lights =lights	<CheckboxOnOff value="1" v-model="lights" name="lights">Lights</Label>
-->
