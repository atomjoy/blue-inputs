<script setup>
import { computed } from 'vue';
import IconCheckmark from './icons/IconCheckmark.vue';

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
		<input :id="hash(props.value)" class="form-checkbox" type="checkbox" v-model="model" :value="props.value" :name="props.name" :class="props.class" :placeholder="props.placeholder" @change="emits('change', model)" />
		<div class="form-checkmark">
			<div class="form-checkmark-box" v-if="!checked"></div>
			<IconCheckmark v-if="checked" />
		</div>
		<label class="form-checkbox-label" :for="hash(props.value)" v-if="props.label">{{ props.label }}<slot /></label>
	</div>
</template>

<style>
@import url('./css/inputs.css');
</style>

<!--
	// Multiple Array with strings values
	let payment = ref(['card','cash']) // Default selected in array
	<Checkbox value="cash" v-model="payment" name="pay_cash">Cash</Label>
	<Checkbox value="card" v-model="payment" name="pay_card">Card</Label>

	// Single (true|false)
	let remember_me = ref(true)
	<Checkbox value="1" v-model="remember_me" name="remember_me">Remember me</Label>
-->
