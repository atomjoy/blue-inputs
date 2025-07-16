<script setup>
import { ref } from 'vue';
import IconCheckmark from './icons/IconCheckmark.vue';
import IconArrowDown from './icons/IconArrowDown.vue';
import IconArrowUp from './icons/IconArrowUp.vue';
import country from './json/country.json';

const emits = defineEmits(['change']);
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'prefix' },
	class: { type: [String, Array, Object] },
	placeholder: { type: String, default: 'Choose' },
	search_error: { type: String, default: 'No options found' },
});

let filtered_options = ref(country);
let search_check = ref(false);
let search = ref('');

function toggle(i, e) {
	closeAll();
	e.currentTarget.classList.toggle('select-opened');
}

function update(option) {
	search.value = '';
	filtered_options.value = country;
	model.value = option.code;
	emits('change', option.code);
	closeAll();
}

function code(code) {
	let item = country.filter((o) => {
		return o.code.toLowerCase() == code.toLowerCase();
	});
	return item[0].prefix ?? '00';
}

function filterOptions(e) {
	filtered_options.value = country.filter((o) => {
		return o.name.toLowerCase().startsWith(e.target.value.toLowerCase());
	});
	search_check.value = filtered_options.value.length == 0 ? true : false;
}

function closeAll() {
	let all = document.querySelectorAll('.select-opened');
	all.forEach((i) => {
		i.classList.remove('select-opened');
	});
}
</script>
<template>
	<div class="form-input-wrapper">
		<div class="form-input-event" @click.stop="toggle('div', $event)">
			<div class="form-select" :class="props.class">
				<div class="form-select-selected">
					<img class="form-select-option-flag-selected" :src="'/flags/' + model + '.webp'" onerror="this.remove()" />
					{{ '+' + code(model) ?? props.placeholder }}
				</div>
			</div>

			<div class="form-input-icon">
				<IconArrowDown class="form-select-arror-down" />
				<IconArrowUp class="form-select-arror-up" @click.stop="closeAll()" />
			</div>

			<div class="form-select-options">
				<input type="text" v-model="search" placeholder="Search" class="form-select-options-search" @click.stop="" @keyup="filterOptions" />

				<div class="form-select-options-wrapper">
					<div class="form-select-option" @click.stop="update(option)" v-for="option in filtered_options">
						<div class="form-select-option-icon">
							<!-- <i v-if="model == option.code">✔️</i> -->
							<IconCheckmark v-if="model == option.code" />
						</div>
						<img class="form-select-option-flag" :src="'/flags/' + option.code.toLowerCase() + '.webp'" />
						{{ '+' + option.prefix + ' ' + option.name ?? props.placeholder }}
					</div>

					<div v-if="search_check" class="form-select-option-error">{{ props.search_error }}</div>
				</div>
			</div>

			<input type="hidden" :name="props.name" :value="model" v-if="props.name" />
		</div>
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
