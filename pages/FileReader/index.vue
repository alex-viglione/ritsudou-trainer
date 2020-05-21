<template>
	<div>
		<label class="text-reader">
			<input
				type="file"
				@change="loadTextFromFile"
			>
		</label>

		<!-- <p v-for="element in data">{{element.name}} is {{element.status}}</p> -->
		<div>
			<div
				v-for="element in data"
				:key="element.id"
				v-show="element.id === counter"
			>
				<p>Name: {{element.name}} {{element.id}}</p>
				<p>Status: {{element.status}}</p>
			</div>
			<div v-show="counter > data.length">End of the line</div>
			<p>{{data.length}} {{counter}}</p>
			<button @click="counter--">Previous page</button>
			<button @click="counter++">Next page</button>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			data: [],
			counter: 1
		}
	},
	methods: {
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