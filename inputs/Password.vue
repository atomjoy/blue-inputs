<script setup>
import IconCopy from './icons/IconCopy.vue';
import IconClose from './icons/IconClose.vue';
import IconCheck from './icons/IconCheck.vue';
import IconEyeOpen from './icons/IconEyeOpen.vue';
import IconEyeClosed from './icons/IconEyeClosed.vue';
import { ref, onMounted } from 'vue';

const emits = defineEmits(['change', 'invalid', 'valid']);
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'text' },
	class: { type: [String, Array, Object] },
	placeholder: { type: String },
	minChars: { type: Number, default: 12 },
	focus: { type: Boolean, default: false },
	show: { type: Boolean, default: false },
	copy: { type: Boolean, default: false },
});

let input = ref(null);
let show = ref(false);
let open = ref(false);
let check1 = ref(false);
let check2 = ref(false);
let check3 = ref(false);
let check4 = ref(false);
let check5 = ref(false);
let power = ref(0);

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

function onFocus(e) {
	open.value = true;
	validatePass(e);
}

function validatePass(event) {
	let str = event?.target?.value ?? '';

	if (str.replace(' ', '').length >= props.minChars) {
		check1.value = true;
	} else {
		check1.value = false;
	}

	if (Boolean(str.match(/[A-Z]/))) {
		check2.value = true;
	} else {
		check2.value = false;
	}

	if (Boolean(str.match(/[a-z]/))) {
		check3.value = true;
	} else {
		check3.value = false;
	}

	if (Boolean(str.match(/[0-9]/))) {
		check4.value = true;
	} else {
		check4.value = false;
	}

	if (Boolean(str.match(/[^A-Za-z0-9 ]/))) {
		check5.value = true;
	} else {
		check5.value = false;
	}

	if (check1.value && check2.value && check3.value && check4.value && check5.value) {
		emits('valid', str);
	} else {
		emits('invalid', str);
	}

	power.value = Number(check1.value) + Number(check2.value) + Number(check3.value) + Number(check4.value) + Number(check5.value) ?? 0;
}

function passPower() {
	if (power.value == 1) {
		return 'Very Weak';
	}
	if (power.value == 2) {
		return 'Weak';
	}
	if (power.value == 3) {
		return 'Average';
	}
	if (power.value == 4) {
		return 'Strong';
	}
	if (power.value == 5) {
		return 'Secure';
	}
	return 'Empty';
}
</script>
<template>
	<div class="form-input-wrapper">
		<input ref="input" v-model="model" class="form-input form-password" type="password" :name="props.name" :class="props.class" :placeholder="props.placeholder" @keyup="validatePass" @focus="onFocus" @blur="open = false" @change="emits('change', $event)" />
		<IconCopy v-if="props.copy" class="form-input-copy" @click="copyClipboard" title="Copy" />
		<div class="form-input-icon" @click="toggle">
			<IconEyeClosed v-if="!show" />
			<IconEyeOpen v-if="show" />
		</div>

		<div class="form-password-validator" v-if="open">
			<div class="flex"><IconClose v-if="!check1" /><IconCheck v-if="check1" class="green" />Minimum number of characters: {{ props.minChars }}</div>
			<div class="flex"><IconClose v-if="!check2" /><IconCheck v-if="check2" class="green" />Contains a capital letter</div>
			<div class="flex"><IconClose v-if="!check3" /><IconCheck v-if="check3" class="green" />Contains a lowercase letter</div>
			<div class="flex"><IconClose v-if="!check4" /><IconCheck v-if="check4" class="green" />Contains a number</div>
			<div class="flex"><IconClose v-if="!check5" /><IconCheck v-if="check5" class="green" />Contains a special character</div>
			<div class="flex password-power" :class="['password-power-' + power]">{{ passPower() }}</div>
		</div>
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
