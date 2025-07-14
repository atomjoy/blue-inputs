<script setup>
// Document click close all selects
document.addEventListener('click', function () {
	let all = document.querySelectorAll('.select-opened');
	all.forEach((i) => {
		i.classList.remove('select-opened');
	});
});
</script>
<template></template>
