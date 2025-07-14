<script setup>
import { ref } from 'vue';

const props = defineProps({
	placeholder: { type: String, default: 'Add tag-slug-lower-case and hit enter' },
	error_length: { type: String, default: 'Max 40 characters' },
	error_tag: { type: String, default: 'Invalid tag' },
});

const model = defineModel();
const input = ref(null);
const tag = ref('');

function add() {
	if (tag.value.length > 40) {
		alert(props.error_length);
		return;
	}
	if (new RegExp('^[a-z0-9]+(?:-[a-z0-9]+)*$').test(tag.value)) {
		model.value.push(tag.value);
		tag.value = '';
	} else {
		alert(props.error_tag);
	}
}

function del(slug) {
	if (confirm('Delete?')) {
		model.value = model.value.filter((i) => i !== slug);
	}
}
</script>

<template>
	<div class="form-input-wrapper">
		<div class="form-input-tags" @click="input.focus()">
			<input ref="input" v-model="tag" type="text" name="tag" class="form-input form-input-tags-margin" @blur="input.value = ''" @keydown.enter.prevent="add" :placeholder="props.placeholder" />
			<input v-model="model" type="hidden" name="tags[]" />
			<div class="form-input-tag-list">
				<div class="form-input-tag-item" v-for="tag in model" @click="del(tag)" :title="$t('Delete')">{{ tag }}</div>
			</div>
		</div>
	</div>
</template>

<style>
.form-input-tags {
	float: left;
	width: 100%;
	box-sizing: border-box;
	border-radius: var(--border-radius);
}

.form-input-tags-margin {
	margin-bottom: 5px !important;
}

.form-input-tag-list {
	float: left;
	width: 100%;
	height: auto;
	margin-bottom: 20px;
	overflow: hidden;
}

.form-input-tag-input {
	float: left;
	width: 100%;
	margin-top: 5px;
	margin-right: 5px;
	margin-bottom: 5px;
	padding: 15px 20px;
	line-height: 1.5;
	font-size: 16px;
	cursor: pointer;
	transition: all 0.6s;
	border-radius: var(--border-radius);
	border: 1px solid var(--input-border);
}

.form-input-tag-item {
	cursor: pointer;
	float: left;
	width: auto;
	margin-right: 5px;
	margin-top: 5px;
	margin-bottom: 5px;
	padding: 5px 10px;
	font-size: 13px;
	color: #0075ff;
	background: #0075ff11;
	border-radius: var(--border-radius);
}

.form-input-tag-item:hover {
	color: #fff;
	background: #e0414f;
}
</style>
