<script setup>
import { onMounted, ref, watch } from 'vue';
import Select from '@/components/utils/inputs/select/SelectObject.vue';

const emits = defineEmits(['change']);
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'time' },
	class: { type: [String, Array, Object] },
});

let hour = ref({ id: '00', name: '00' });
let hour_options = ref([]);

let minute = ref({ id: '00', name: '00' });
let minute_options = ref([]);

let second = ref({ id: '00', name: '00' });
let second_options = ref([]);

onMounted(() => {
	for (let i = 0; i < 60; i++) {
		if (`${i}`.length == 1) {
			i = '0' + i;
		}
		if (i < 24) {
			hour_options.value.push({ id: i, name: i });
		}
		minute_options.value.push({ id: i, name: i });
		second_options.value.push({ id: i, name: i });
	}

	splitModel();
});

watch(
	() => model.value,
	() => {
		splitModel();
	}
);

function updateHour(e) {
	hour.value = e;
	update();
}

function updateMinute(e) {
	minute.value = e;
	update();
}

function updateSecond(e) {
	second.value = e;
	update();
}

function update() {
	let cur_time = hour.value.id + ':' + minute.value.id + ':' + second.value.id;
	model.value = cur_time;
	emits('change', cur_time);
}

function splitModel() {
	let a = model.value.split(':');
	let h = a[0] > 23 ? 23 : a[0];
	let m = a[1] > 59 ? 59 : a[1];
	let s = a[2] > 59 ? 59 : a[2];
	hour.value = { id: h, name: h };
	minute.value = { id: m, name: m };
	second.value = { id: s, name: s };
	update();
}
</script>
<template>
	<div class="form-input-wrapper">
		<div class="form-input-time">
			<Select v-model="hour" :options="hour_options" name="hour" placeholder="Hour" :search="false" @change="updateHour($event)" />
			<Select v-model="minute" :options="minute_options" name="minute" placeholder="Minute" :search="false" @change="updateMinute($event)" />
			<Select v-model="second" :options="second_options" name="second" placeholder="Second" :search="false" @change="updateSecond($event)" />
		</div>

		<input type="hidden" :name="props.name" :value="model" />
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
