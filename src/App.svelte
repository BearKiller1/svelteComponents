<script>
	import Dialog from './components/dialog/Dialog.svelte';

	let inputValue;

	let dialog = {
		save: saveDialog,
	
		props: {
			title: 'Title from the parent',
		},
	};

	function saveDialog(){
		alert(inputValue);
	}

	function fetchData(){
		console.log(dialog.values);
	}

</script>

<button on:click={dialog.open}>Open Dialog</button>
<button on:click={dialog.close}>close dialog</button>


<!-- think about this name "values" -->
<Dialog bind:dialog={dialog} prop={dialog.props} openIf={true}>
	<input type="text" id="name" placeholder="name">
	<input type="text" id="surname" placeholder="surname">
	<input type="text" id="age" placeholder="age">
	<input type="text" id="email" placeholder="email">
	<br>

	<div class="buttons">
		<button on:click={dialog.save}>Save</button>
		<button on:click={fetchData}>fetch data</button>
		<button on:click={dialog.close}>Close</button>
	</div>
</Dialog>