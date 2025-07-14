<script setup>
import { onMounted, ref, watch } from 'vue';
import Select from '@/components/utils/inputs/Select.vue';

const emits = defineEmits(['change']);
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'time' },
	class: { type: [String, Array, Object] },
});

let hour = ref(null);
let hour_options = ref([]);
let minute = ref(null);
let minute_options = ref([]);
let second = ref(null);
let second_options = ref([]);

onMounted(() => {
	for (let i = 0; i < 60; i++) {
		if (`${i}`.length == 1) {
			i = '0' + i;
		}
		if (i < 24) {
			hour_options.value.push(i);
		}
		minute_options.value.push(i);
		second_options.value.push(i);
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
	let cur_time = hour.value + ':' + minute.value + ':' + second.value;
	model.value = cur_time;
	emits('change', cur_time);
}

function splitModel() {
	let a = model.value.split(':');
	let h = a[0] > 23 ? 23 : a[0];
	let m = a[1] > 59 ? 59 : a[1];
	let s = a[2] > 59 ? 59 : a[2];
	hour.value = h;
	minute.value = m;
	second.value = s;
	update();
}
</script>
<template>
	<div class="form-input-wrapper">
		<div class="form-input-time">
			<Select v-model="hour" :options="hour_options" name="" placeholder="Hour" :search="false" @change="updateHour($event)" />
			<span>:</span>
			<Select v-model="minute" :options="minute_options" name="" placeholder="Minute" :search="false" @change="updateMinute($event)" />
			<span>:</span>
			<Select v-model="second" :options="second_options" name="" placeholder="Second" :search="false" @change="updateSecond($event)" />
		</div>

		<input type="hidden" :name="props.name" :value="model" v-if="props.name" />
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
