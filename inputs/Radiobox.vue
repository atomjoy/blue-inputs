<script setup>
import { computed } from 'vue';
import IconRadiomark from './icons/IconRadiomark.vue';

const emits = defineEmits(['change']);
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'fruits' },
	value: { type: String, required: true },
	label: { type: String, default: '' },
});

const checked = computed(() => {
	return model.value == props.value;
});

function update(e) {
	model.value = e.target.value;
	emits('change', e.target.value);
}

function hash(s) {
	return s.split('').reduce(function (a, b) {
		a = (a << 5) - a + b.charCodeAt(0);
		return a & a;
	}, 0);
}
</script>

<template>
	<div class="form-checkbox-line">
		<input :id="hash(props.value)" class="form-checkbox" type="radio" v-model="model" :name="props.name" :value="props.value" :class="props.class" :placeholder="props.placeholder" @change="update" />
		<div class="form-checkmark form-checkmark-radio">
			<div class="form-radiobox-box" v-if="!checked"></div>
			<IconRadiomark v-if="checked" />
		</div>
		<label class="form-radiobox-label" :for="hash(props.value)" v-if="props.label">{{ props.label }}<slot /></label>
	</div>
</template>

<style>
@import url('./css/inputs.css');
</style>

<!--
  // Empty string or selected value: 'Cherry'
  let fruit = ref('')

  <Radiobox label="Melon" value="Melon" v-model="fruit" name="fruit" />
  <Radiobox label="Banan" value="Banan" v-model="fruit" name="fruit" />
  <Radiobox label="Cherry" value="Cherry" v-model="fruit" name="fruit" />
-->
