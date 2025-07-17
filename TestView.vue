<script setup>
import SelectMultiple from '@/components/utils/inputs/SelectMultiple.vue';
import SelectMultipleObject from '@/components/utils/inputs/SelectMultipleObject.vue';
import Select from '@/components/utils/inputs/Select.vue';
import SelectObject from '@/components/utils/inputs/SelectObject.vue';
import SelectPrefix from '@/components/utils/inputs/Prefix.vue';
import SelectPrefixCode from '@/components/utils/inputs/PrefixCode.vue';
import SelectPrefixObject from '@/components/utils/inputs/PrefixObject.vue';
import SelectCountry from '@/components/utils/inputs/Country.vue';
import SelectCountryObject from '@/components/utils/inputs/CountryObject.vue';
import Wrapper from '@/components/utils/inputs/Wrapper.vue';
import Tags from '@/components/utils/inputs/Tags.vue';
import Alert from '@/components/utils/inputs/Alert.vue';
import Label from '@/components/utils/inputs/Label.vue';
import Textarea from '@/components/utils/inputs/Textarea.vue';
import Input from '@/components/utils/inputs/Input.vue';
import InputButton from '@/components/utils/inputs/Button.vue';
import InputButtonCancel from '@/components/utils/inputs/ButtonCancel.vue';
import InputNumber from '@/components/utils/inputs/Number.vue';
import InputPassword from '@/components/utils/inputs/Password.vue';
import InputSecret from '@/components/utils/inputs/Secret.vue';
import DateTime from '@/components/utils/inputs/DateTime.vue';
import InputDate from '@/components/utils/inputs/Date.vue';
import InputTime from '@/components/utils/inputs/Time.vue';
import CheckboxOnOff from '@/components/utils/inputs/CheckboxOnOff.vue';
import Checkbox from '@/components/utils/inputs/Checkbox.vue';
import Radiobox from '@/components/utils/inputs/Radiobox.vue';
import AvatarInput from '@/components/utils/inputs/Avatar.vue';
import EventCloseSelects from '@/components/utils/inputs/EventCloseSelects.vue';
import Selector from '@/components/utils/inputs/Selector.vue';
import SelectorMini from '@/components/utils/inputs/SelectorMini.vue';
import SelectorOnOff from '@/components/utils/inputs/SelectorOnOff.vue';
import SelectorSlot from '@/components/utils/inputs/SelectorSlot.vue';
import SelectorSlotButton from '@/components/utils/inputs/SelectorSlotButton.vue';
import Price from '@/components/utils/inputs/Price.vue';
import Info from '@/components/utils/inputs/Info.vue';
import IconShieldCheck from '@/components/utils/inputs/icons/IconShieldCheck.vue';
import IconShieldCross from '@/components/utils/inputs/icons/IconShieldCross.vue';
import IconShieldWarning from '@/components/utils/inputs/icons/IconShieldWarning.vue';
import { ref } from 'vue';

let email = ref('email@example.com');
let ip = ref('127.0.0.9');
let pass = ref('Password123#');
let apikey = ref('ab384bc2eb83r7439f24f293482');
let year = ref(2025);
let created_datetime = ref('2020-12-19 23:25:15');
let created_date = ref('2025-08-25');
let created_time = ref('22:55:44');
let country = ref('PL');
let prefix = ref(48);
let price = ref(548.76);
let payment = ref(['card', 'cash']);
let settings = ref(['sms']);
let tags = ref(['sms']);
let remember_me = ref(true);
let enable = ref(true);
let fruits = ref('Melon');
let about = ref('');
let selector = ref('dns');
let selector_slot = ref('accept');
let selector_options = ref(['policy', 'dns', 'nat']);
let selector_mini = ref('senior');
let selector_mini_options = ref(['regular', 'senior', 'expert', 'master']);
let policy = ref('accept');
let lights = ref(true);
let categories = ref(['php', 'html']);
let categories_options = ref(['laravel', 'php', 'html']);

let country_obj = ref({
	name: 'Afghanistan',
	prefix: '93',
	emoji: '🇦🇫',
	code: 'AF',
});

let prefix_code = ref('PL');

let prefix_obj = ref({
	name: 'Afghanistan',
	prefix: '93',
	emoji: '🇦🇫',
	code: 'AF',
});

let lang = ref('css');
let lang_options = ref([null, 'css', 'csharp', 'html', 'js', 'php', 'go', 'vue', 'c++']);

let lang_object = ref({ id: 'php', name: 'php' });
let lang_object_options = ref([
	{ id: null, name: 'Select' },
	{ id: 'csharp', name: 'csharp' },
	{ id: 'css', name: 'css' },
	{ id: 'go', name: 'go' },
	{ id: 'html', name: 'html' },
	{ id: 'java', name: 'java' },
	{ id: 'php', name: 'php' },
	{ id: 'vue', name: 'vue' },
]);

let categories_object = ref([2, 3]);
let categories_object_options = ref([
	{ id: 1, name: 'csharp' },
	{ id: 2, name: 'css' },
	{ id: 3, name: 'go' },
	{ id: 4, name: 'html' },
	{ id: 5, name: 'java' },
	{ id: 6, name: 'php' },
	{ id: 7, name: 'vue' },
]);

function onSubmit(e) {
	console.log('Submit', new FormData(e.target));
}
</script>

<template>
	<EventCloseSelects />

	<form action="/test" method="post" enctype="multipart/form-data" @submit.stop.prevent="onSubmit" style="margin: 50px auto; padding: 20px; width: 90%; height: auto; max-width: 600px; padding-bottom: 200px">
		<Label text="Avatar image" />
		<AvatarInput />

		<Label text="Categories">({{ categories }})</Label>
		<SelectMultiple v-model="categories" name="categories[]" :options="categories_options" @change="console.log($event)" />

		<Label text="Categories">({{ categories_object }})</Label>
		<SelectMultipleObject v-model="categories_object" name="categories_object[]" :options="categories_object_options" @change="console.log($event)" />

		<Label text="Email address">({{ email }})</Label>
		<Input v-model="email" name="email" type="email" placeholder="Enter email address" @change="console.log($event)" />

		<Label text="Ip address">({{ ip }})</Label>
		<Input v-model="ip" name="ip" class="form-input-background-dark" placeholder="Enter email address" @change="console.log($event)" />

		<Label text="Price">({{ price }})</Label>
		<Price v-model="price" name="price" @change="console.log($event)" />

		<Label text="Network">({{ selector }})</Label>
		<Selector v-model="selector" :options="selector_options" name="selector" @change="console.log($event)" />

		<Label text="Level">({{ selector_mini }})</Label>
		<SelectorMini v-model="selector_mini" :options="selector_mini_options" name="selector_mini" @change="console.log($event)" />

		<Label text="Lights">({{ lights }})</Label>
		<SelectorOnOff v-model="lights" name="lights" @change="console.log($event)" />

		<Label text="Selector Slot">({{ selector_slot }})</Label>
		<SelectorSlot v-model="selector_slot" name="selector_slot" @change="console.log($event)">
			<template v-slot:default="{ onClick }">
				<SelectorSlotButton v-model="selector_slot" value="accept" @click="onClick('accept')">✔️ Accept</SelectorSlotButton>
				<SelectorSlotButton v-model="selector_slot" value="reject" @click="onClick('reject')">🚩 Reject</SelectorSlotButton>
				<SelectorSlotButton v-model="selector_slot" value="drop" @click="onClick('drop')">❌ Drop</SelectorSlotButton>
			</template>
		</SelectorSlot>

		<Label text="Policy Slot">({{ policy }})</Label>
		<SelectorSlot v-model="policy" name="selector_policy" @change="console.log($event)">
			<template v-slot:default="{ onClick }">
				<SelectorSlotButton v-model="policy" value="accept" @click="onClick('accept')"><IconShieldCheck /> Accept</SelectorSlotButton>
				<SelectorSlotButton v-model="policy" value="reject" @click="onClick('reject')"><IconShieldWarning /> Reject</SelectorSlotButton>
				<SelectorSlotButton v-model="policy" value="drop" @click="onClick('drop')"><IconShieldCross /> Drop</SelectorSlotButton>
			</template>
		</SelectorSlot>

		<Label text="Tags">({{ tags }})</Label>
		<Tags v-model="tags" name="tags" @change="console.log($event)" />

		<Label text="Language">({{ lang }})</Label>
		<Select v-model="lang" name="lang" :options="lang_options" @change="console.log($event)" />

		<Label text="Language object">({{ lang_object }})</Label>
		<SelectObject v-model="lang_object" name="lang" :options="lang_object_options" @change="console.log($event)" />

		<Label text="Country">({{ country }})</Label>
		<SelectCountry v-model="country" name="country" @change="console.log($event)" />

		<Label text="Country object">({{ country_obj }})</Label>
		<SelectCountryObject v-model="country_obj" name="country_obj" @change="console.log($event)" />

		<Label text="Prefix">({{ prefix }})</Label>
		<SelectPrefix v-model="prefix" name="prefix" @change="console.log($event)" />

		<Label text="Prefix code">({{ prefix_code }})</Label>
		<SelectPrefixCode v-model="prefix_code" name="prefix_code" @change="console.log($event)" />

		<Label text="Prefix object">({{ prefix_obj }})</Label>
		<SelectPrefixObject v-model="prefix_obj" name="prefix_obj" @change="console.log($event)" />

		<Label text="Date">({{ created_date }})</Label>
		<InputDate v-model="created_date" name="created_date" @change="console.log($event)" />

		<Label text="Time">({{ created_time }})</Label>
		<InputTime v-model="created_time" name="created_time" @change="console.log($event)" />

		<Label text="Date Time">({{ created_datetime }})</Label>
		<DateTime v-model="created_datetime" name="created_datetime" @change="console.log($event)" />

		<Label for="number" text="Year">({{ year }})</Label>
		<InputNumber v-model="year" name="year" placeholder="Year" @change="console.log($event)" />

		<Label text="Password">({{ pass }})</Label>
		<InputPassword v-model="pass" name="password" placeholder="Enter password" @change="console.log($event)" />

		<Label text="Api Key">({{ apikey }})</Label>
		<InputSecret v-model="apikey" name="apikey" placeholder="Api key" @change="console.log($event)" />

		<Label text="Remeber me">({{ remember_me }})</Label>
		<div class="form-input-wrapper">
			<Checkbox value="1" v-model="remember_me" name="remember_me" @change="console.log($event)">Remember me</Checkbox>
		</div>

		<Label text="Remeber me">({{ enable }})</Label>
		<Wrapper>
			<CheckboxOnOff value="1" v-model="enable" name="enable" @change="console.log($event)" />
		</Wrapper>

		<Label text="Settings">({{ settings }})</Label>
		<Wrapper>
			<CheckboxOnOff value="email" v-model="settings" name="settings[]" label="Email newsletter" @change="console.log($event)" />
			<CheckboxOnOff value="sms" v-model="settings" name="settings[]" label="Sms newsletter" @change="console.log($event)" />
		</Wrapper>

		<Label text="Payments">({{ payment }})</Label>
		<Wrapper>
			<Checkbox value="cash" v-model="payment" name="payment[]" label="Cash" @change="console.log($event)" />
			<Checkbox value="card" v-model="payment" name="payment[]" label="Card" @change="console.log($event)" />
			<Checkbox value="blik" v-model="payment" name="payment[]" label="Blik" @change="console.log($event)" />
		</Wrapper>

		<Label text="Fruits" info="Select only fruits below!">({{ fruits }})</Label>
		<Wrapper>
			<Radiobox value="Banan" v-model="fruits" name="fruits" label="Banan" @change="console.log($event)" />
			<Radiobox value="Cherry" v-model="fruits" name="fruits" label="Cherry" @change="console.log($event)" />
			<Radiobox value="Melon" v-model="fruits" name="fruits" label="Melon" @change="console.log($event)" />
		</Wrapper>

		<Label text="About">({{ about }})</Label>
		<Textarea v-model="about" name="about" placeholder="Write something about yourself." @change="console.log($event)" />

		<InputButton type="submit" value="Submit" />
		<InputButtonCancel value="Cancel" @click="console.log('Cancel')" />

		<Label text="Alert: Info, Error, Warming"></Label>
		<Alert type="info"> <strong>Info</strong> ipsum dolor sit amet consectetur, adipisicing elit. Autem blanditiis suscipit excepturi, amet assumenda alias et quisquam rerum veritatis repellendus aliquam tenetur aut, magni tempore! Doloremque nihil tenetur illum in. </Alert>
		<Alert type="success"><strong>Success</strong> ipsum dolor sit amet consectetur, adipisicing elit. Autem blanditiis suscipit excepturi, amet assumenda alias et quisquam rerum veritatis repellendus aliquam tenetur aut, magni tempore! Doloremque nihil tenetur illum in.</Alert>
		<Alert type="error"><strong>Error</strong> ipsum dolor sit amet consectetur, adipisicing elit. Autem blanditiis suscipit excepturi, amet assumenda alias et quisquam rerum veritatis repellendus aliquam tenetur aut, magni tempore! Doloremque nihil tenetur illum in.</Alert>
		<Alert type="warning"><strong>Warning</strong> ipsum dolor sit amet consectetur, adipisicing elit. Autem blanditiis suscipit excepturi, amet assumenda alias et quisquam rerum veritatis repellendus aliquam tenetur aut, magni tempore! Doloremque nihil tenetur illum in.</Alert>
	</form>
</template>
