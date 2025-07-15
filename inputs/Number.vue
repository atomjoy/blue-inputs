<script setup>
import IconArrowDown from './icons/IconArrowDown.vue';
import IconArrowUp from './icons/IconArrowUp.vue';

import { ref, onMounted, watch } from 'vue';

const emits = defineEmits(['change']);
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'number' },
	class: { type: [String, Array, Object] },
	minus: { type: Boolean, default: false },
	focus: { type: Boolean, default: false },
});

let input = ref(null);
let nr = ref(0);

onMounted(() => {
	if (props.focus) {
		input.value.focus();
	}

	Parse();
});

watch(
	() => model.value,
	() => {
		Parse();
	}
);

function Parse() {
	if (Number.isInteger(parseInt(model.value))) {
		model.value = parseInt(model.value);
		if (props.minus != true) {
			if (model.value < 0) {
				model.value = 0;
			}
		}
	} else {
		model.value = 0;
	}
}

function Up() {
	nr = parseInt(model.value) + 1;
	model.value = nr;
	emits('change', nr);
}

function Down() {
	nr = parseInt(model.value) - 1;
	model.value = nr;
	emits('change', nr);
}
</script>
<template>
	<div class="form-input-wrapper">
		<input ref="input" v-model="model" class="form-input" type="text" :name="props.name" :class="props.class" :placeholder="props.placeholder" @change="emits('change', $event.target.value)" />
		<div class="form-input-icons">
			<IconArrowUp width="25px" height="25px" @click.stop.prevent="Up" />
			<IconArrowDown width="25px" height="25px" @click.stop.prevent="Down" />
		</div>
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
