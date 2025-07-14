<script setup>
import axios from 'axios';
import Input from './Input.vue';
import Label from './Label.vue';
import IconDelete from './icons/IconDelete.vue';
import avatar_default from './profil/avatar.png';
import { ref } from 'vue';

const model = defineModel();
const props = defineProps({
	avatar: { default: avatar_default },
	label: { default: 'Select image' },
	label_file: { default: 'Select image with extension: webp, png, jpg, jpeg' },
	remove_button: { default: 'Remove Avatar' },
	remove_success: { default: 'Success' },
	remove_error: { default: 'Failed' },
	remove_avatar_url: { default: '/web/api/remove/avatar' },
});

const avatar_path = ref(null);

if (props.avatar) {
	avatar_path.value = '/storage/' + props.avatar;

	if (props.avatar.toLowerCase().startsWith('http://')) {
		avatar_path.value = props.avatar;
	}

	if (props.avatar.toLowerCase().startsWith('https://')) {
		avatar_path.value = props.avatar;
	}
} else {
	avatar_path.value = avatar_default;
}

function getImagePath(e) {
	const path = URL.createObjectURL(e.target.files[0]);
	if (path) {
		avatar_path.value = path;
	}
}

async function removeAvatar() {
	try {
		await axios.post(props.remove_avatar_url, []);
		avatar_path.value = avatar_default;
		alert(props.remove_success);
	} catch (err) {
		alert(props.remove_error);
	}
}
</script>

<template>
	<div class="form-input-wrapper">
		<div class="form-avatar-input">
			<div @click="removeAvatar" class="form-delete-avatar" :title="props.remove_button">
				<IconDelete />
			</div>
			<img :src="avatar_path" class="form-avatar-image" />
			<div class="form-avatar-input-file">
				<Label :text="props.label_file" />
				<Input v-model="model" @change="getImagePath" name="avatar" type="file" />
			</div>
		</div>
	</div>
</template>

<style>
.form-avatar-input {
	position: relative;
	float: left;
	width: 100%;
}
.form-delete-avatar {
	position: absolute;
	top: 60px;
	left: 60px;
	width: 30px;
	height: 30px;
	padding: 5px;
	border-radius: 50%;
	cursor: pointer;
	color: #fff;
	background: var(--input-accent-color);
}
.form-delete-avatar svg {
	width: 20px;
	height: 20px;
	fill: #fff;
}
.form-delete-avatar:hover {
	background: #f23;
}
.form-avatar-image {
	float: left;
	min-width: 80px;
	max-width: 80px;
	min-height: 80px;
	max-height: 80px;
	padding: 3px;
	margin-right: 20px;
	margin-top: 10px;
	border-radius: 50%;
	object-fit: cover;
	border: 2px solid var(--wow-accent);
}
.form-avatar-input-file {
	float: left;
	width: 100%;
	margin-top: 10px;
	overflow: hidden;
}
</style>
