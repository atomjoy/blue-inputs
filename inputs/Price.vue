<script setup>
import { ref, onMounted } from 'vue';

const emits = defineEmits(['change']);
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'text' },
	type: { type: String, default: 'text' },
	class: { type: [String, Array, Object] },
	currency: { type: String, default: 'PLN' },
	placeholder: { type: String, default: '0.00' },
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
		<div class="form-price">
			<input ref="input" class="form-price-input" v-model="model" :type="props.type" :name="props.name" :class="props.class" :placeholder="props.placeholder" @change="emits('change', $event)" />
			<div class="form-input-currency">
				<slot>{{ props.currency }}</slot>
			</div>
		</div>
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
