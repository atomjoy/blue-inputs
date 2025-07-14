<script setup>
import { onMounted, ref } from 'vue';
import InputDate from '@/components/utils/inputs/Date.vue';
import InputTime from '@/components/utils/inputs/Time.vue';

const emits = defineEmits(['change']);
const model = defineModel({ required: true });
const props = defineProps({
	name: { type: String, default: 'date_time' },
	class: { type: [String, Array, Object] },
});

const dt_date = ref(null);
const dt_time = ref(null);

onMounted(() => {
	let a = model.value.split(' ');
	dt_date.value = a[0];
	dt_time.value = a[1];
	update();

	for (let i = 0; i < 32; i++) {
		if (`$i`.length == 1) {
			i = '0' + i;
		}
		if (i < 13) {
			month_options.value.push(i);
		}
		day_options.value.push(i);
	}
});

function updateDate(e) {
	dt_date.value = e;
	update();
}

function updateTime(e) {
	dt_time.value = e;
	update();
}

function update() {
	let cur_date = dt_date.value + ' ' + dt_time.value;
	model.value = cur_date;
	emits('change', cur_date);
}
</script>
<template>
	<div class="form-input-wrapper">
		<div class="form-input-date">
			<InputDate v-model="dt_date" name="" @change="updateDate($event)" />
		</div>
		<div class="form-input-time">
			<InputTime v-model="dt_time" name="" @change="updateTime($event)" />
		</div>

		<input type="hidden" :name="props.name" :value="model" />
	</div>
</template>
<style>
@import url('./css/inputs.css');
</style>
