<script setup>
import { ref } from 'vue';
import IconCheckmark from './icons/IconCheckmark.vue';
import IconArrowDown from './icons/IconArrowDown.vue';
import IconArrowUp from './icons/IconArrowUp.vue';

const emits = defineEmits(['change']);
const model = defineModel({ required: true, type: Array });
const props = defineProps({
	name: { type: String, default: 'multiple_object[]' },
	options: { type: Array, default: [] },
	class: { type: [String, Array, Object] },
	search: { type: Boolean, default: true },
	placeholder: { type: String, default: 'Choose' },
	search_error: { type: String, default: 'No options found' },
	info_text: { type: String, default: 'Selected:' },
});

let filtered_options = ref(props.options);
let search_check = ref(false);
let search = ref('');

function toggle(i, e) {
	closeAll();
	e.currentTarget.classList.toggle('select-opened');
}

function toggleElement(arr, val) {
	return arr.map((i) => i.id).includes(val.id) ? arr.filter((el) => el.id != val.id) : [...arr, val];
}

function update(option) {
	search.value = '';
	filtered_options.value = props.options;
	let selected = toggleElement(model.value, option);
	model.value = selected;
	emits('change', selected);
}

function filterOptions(e) {
	filtered_options.value = props.options.filter((o) => {
		if (o.name != null) {
			return o.name.toLowerCase().startsWith(e.target.value.toLowerCase());
		}
		return false;
	});
	search_check.value = filtered_options.value.length == 0 ? true : false;
}

function count(m) {
	let count = 0;
	m.forEach((i) => {
		count++;
	});
	return count;
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
				<div class="form-select-selected">{{ props.info_text }} {{ count(model) ?? props.placeholder }}</div>
			</div>

			<div class="form-input-icon">
				<IconArrowDown class="form-select-arror-down" />
				<IconArrowUp class="form-select-arror-up" @click.stop="closeAll()" />
			</div>

			<div class="form-select-options">
				<input v-model="search" type="text" placeholder="Search" class="form-select-options-search" @click.stop="" @keyup="filterOptions" v-if="props.search" />

				<div class="form-select-options-wrapper">
					<div class="form-select-option" @click.stop="update(option)" v-for="option in filtered_options">
						<div class="form-select-option-icon">
							<IconCheckmark v-if="model.map((i) => i.id).includes(option.id)" />
						</div>
						{{ option.name ?? props.placeholder }}
					</div>

					<div v-if="search_check" class="form-select-option-error">{{ props.search_error }}</div>
				</div>
			</div>

			<select multiple v-model="model" :name="props.name" style="display: inline">
				<option v-for="o in props.options" :value="o" :selected="model.map((i) => i.id).includes(o.id)">{{ o.name + ' ' + o.id }}</option>
			</select>
		</div>
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
