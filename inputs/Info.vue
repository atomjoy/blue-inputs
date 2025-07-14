<script setup>
import { ref } from 'vue';
import IconInfo from './icons/IconInfoThin.vue';

const props = defineProps({
	message: { type: String, default: '' },
});

const show = ref(false);
</script>

<template>
	<div class="form-label-info">
		<IconInfo v-if="props.message" class="form-label-info-icon" @click.stop="show = !show" />
		<div class="form-info-popup" v-if="show" @click.stop="show = !show">
			<slot>{{ props.message }}</slot>
			<div class="form-info-popup-triangle"></div>
		</div>
	</div>
</template>

<style>
@import url('./css/inputs.css');
</style>
