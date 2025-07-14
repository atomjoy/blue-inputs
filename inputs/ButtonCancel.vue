<script setup>
const props = defineProps({
	text: { type: String, default: 'Cancel' },
	type: { type: String, default: 'button' },
	class: { type: [String, Array, Object] },
});
</script>
<template>
	<input class="form-input-button-cancel form-input-button-margin" :type="props.type" :value="props.text" :class="props.class" />
</template>
<style>
@import url('./css/inputs.css');
</style>
