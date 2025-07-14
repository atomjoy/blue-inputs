<script setup>
import IconInfo from './icons/IconInfoThin.vue';

const props = defineProps({
	message: { type: String, default: 'Alert message!' },
	type: { type: String, default: 'info' },
});

const type = 'form-alert-' + props.type;
</script>

<template>
	<div class="form-alert" :class="type">
		<div class="form-alert-left">
			<IconInfo class="form-alert-icon" />
		</div>
		<div class="form-alert-message">
			<slot>{{ props.message }}</slot>
		</div>
	</div>
</template>

<style>
@import url('./css/inputs.css');
</style>
