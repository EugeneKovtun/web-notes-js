<template>
	<div class="note-editor">
		<textarea
		 placeholder="Enter your note here ..."
		 rows="5"
		 v-model="noteText"></textarea>
		<div class='flex'>
			<button
				class="clear-button"
				@click="clearFilter()"
			>
				SHOW ALL
			</button>
			<div class='flex'>
				<span>COLOR: &nbsp;</span>
				<kendo-colorpicker v-model="color" v-on:change="onColorSelect">ColorPicker</kendo-colorpicker>
			</div>
      <button
        class="add-button"
        @click="addNote()"
        :disabled="noteText.length===0"
      >
        Add
      </button>
		</div>
	</div>
</template>

<script>
	import axios from 'axios';

	export default {
		data() {
			return {
				noteText: '',
				color: 'FF0000'
			};
		},

		methods: {
			onColorSelect({ value }) {
				this.color = value
			},
			addNote() {
				const note = {
					text: this.noteText,
					bgColor: this.color
				};

				this.$store
					.dispatch('addNote',	note)
					.then(() => this.noteText = '')
			},
			clearFilter() {
				this.$router.push('/')
			}
		}
	};
</script>

<style>
.note-editor {
	width: 100%;
	max-width: 600px;
	padding: 16px;
	margin: 16px auto;
	background-color: white;
	box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
	border-radius: 2px;
	display: flex;
	flex-direction: column;
}

textarea {
	width: 100%;
	resize: none;
	margin: 5px;
	font-size: 14px;
	border: none;
	font-weight: 300;
}

textarea:focus {
	outline: 0;
}

.flex {
	display: flex;
	justify-content: space-between;
	align-items: center;
}

.clear-button {
	width: 120px;
	background-color: rgb(255, 0, 0);
	color: rgb(255, 255, 255);
	border-radius: 8px;
	border: 1px solid rgb(200, 200, 200);
	font-size: 14px;
	padding: 8px 8px;
	text-transform: uppercase;
	text-decoration: none;
	cursor: pointer;
  text-shadow: 0px 1px 0px #2f6627;
}

.clear-button:hover {
	background-color: #518e9c;
}

.add-button {
	align-self: flex-end;
	width: 100px;
	background-color: #44c767;
	border-radius: 8px;
	border: 2px solid #18ab29;
	cursor: pointer;
	color: #ffffff;
	font-size: 14px;
	padding: 8px 8px;
	text-transform: uppercase;
	text-decoration: none;
	text-shadow: 0px 1px 0px #2f6627;
}

.add-button:hover {
	background-color: #5cbf2a;
}

.add-button:active {
	position: relative;
	top: 1px;
}

.add-button:focus,
.clear-button:focus {
	outline: 0;
}

.k-colorpicker {
	width: 58px;
}
</style>

