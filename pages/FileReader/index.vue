<template>
	<div class="testpage">
		<div class="inputs">
			<input
				type="text"
				v-model="name"
			>
			<input
				type="number"
				v-model="age"
			>
			<button @click="savePerson">Save person</button>
			<p>{{toFile}}</p>
			<vue-blob-json-csv
				tag-name="button"
				class="button--grey"
				file-type="json"
				file-name="user_data"
				title="Download JSON"
				:data="toFile"
			/>
		</div>
		<br>
		<hr><br>
		<label class="text-reader">
			<input
				type="file"
				@change="loadTextFromFile"
			>
		</label>

		<div>
			<div
				v-for="element in data"
				:key="element.id"
				v-show="element.id === counter"
			>
				<p>Name: {{element.name}} | ID: {{element.id}}</p>
				<p>Age: {{element.age}}</p>
			</div>
			<div v-show="data.length > 0 && counter > data.length">End of the line</div>
			<!-- <p>{{data.length}} {{counter}}</p> -->
			<button @click="decreaseCounter">Previous page</button>
			<button @click="increaseCounter">Next page</button>
		</div>
	</div>
</template>

<script>
import Vue from 'vue';
import VueBlobJsonCsv from 'vue-blob-json-csv';

Vue.use(VueBlobJsonCsv);
export default {
	data() {
		return {
			data: [],
			counter: 1,
			toFile: [],
			name: '',
			age: 0,
			id: 1
		}
	},
	methods: {
		savePerson() {
			let newPerson = {};

			newPerson.name = this.name;
			newPerson.age = this.age;
			newPerson.id = this.id;
			this.toFile.push(newPerson);

			this.name = '';
			this.age = 0;
			this.id++;
		},
		increaseCounter() {
			if (this.counter + 1 > this.data.length) {
				return;
			} else {
				this.counter++;
			}
		},
		decreaseCounter() {
			if (this.counter === 1) {
				return;
			} else {
				this.counter--;
			}
		},
		loadTextFromFile(ev) {
			const file = ev.target.files[0];
			const reader = new FileReader();

			reader.onload = e => {
				const submittedFile = e.target.result;
				const parsed = JSON.parse(submittedFile);
				parsed.forEach(el => this.data.push(el))
			};
			reader.readAsText(file);
		}
	}
};
</script>

<style scoped>
.testpage {
	background-color: #333;
	height: 100vh;
	color: #ccc;
}
</style>