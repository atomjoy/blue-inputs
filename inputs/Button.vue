<script setup>
const props = defineProps({
	text: { type: String, default: 'Submit' },
	type: { type: String, default: 'submit' },
	class: { type: [String, Array, Object] },
});
</script>
<template>
	<input class="form-input-button" :type="props.type" :value="props.text" :class="props.class" />
</template>
<style>
@import url('./css/inputs.css');
</style>
