<script setup>
import { onMounted, ref, watch } from 'vue';
import Select from '@/components/utils/inputs/SelectObject.vue';
import Number from '@/components/utils/inputs/Number.vue';

const emits = defineEmits(['change']);
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'date' },
	class: { type: [String, Array, Object] },
});

let year = ref(2025);
let month = ref({ id: '00', name: '00' });
let month_options = ref([]);
let day = ref({ id: '00', name: '00' });
let day_options = ref([]);

onMounted(() => {
	for (let i = 0; i < 32; i++) {
		if (`${i}`.length == 1) {
			i = '0' + i;
		}
		if (i < 13) {
			month_options.value.push({ id: i, name: i });
		}
		day_options.value.push({ id: i, name: i });
	}

	splitModel();
});

watch(
	() => model.value,
	() => {
		splitModel();
	}
);

function updateYear(e) {
	year.value = e;
	updateDate();
}

function updateMonth(e) {
	month.value = e;
	updateDate();
}

function updateDay(e) {
	day.value = e;
	updateDate();
}

function updateDate() {
	let cur_date = year.value + '-' + month.value.id + '-' + day.value.id;
	model.value = cur_date;
	emits('change', cur_date);
}

function splitModel() {
	let a = model.value.split('-');
	let y = a[0] < 1 ? 1 : a[0];
	let m = a[1] > 12 ? 12 : a[1];
	let d = a[2] > 31 ? 31 : a[2];
	year.value = y;
	month.value = { id: m, name: m };
	day.value = { id: d, name: d };
	updateDate();
}
</script>
<template>
	<div class="form-input-wrapper">
		<div class="form-input-date">
			<Number v-model="year" name="year" placeholder="Year" @change="updateYear($event)" />
			<Select v-model="month" :options="month_options" name="month" placeholder="Month" :search="false" @change="updateMonth($event)" />
			<Select v-model="day" :options="day_options" name="day" placeholder="Day" :search="false" @change="updateDay($event)" />
		</div>

		<input type="hidden" :name="props.name" :value="model" />
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
