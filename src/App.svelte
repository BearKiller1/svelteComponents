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
</script>

<button on:click={dialog.open}>Open Dialog</button>
<button on:click={dialog.close}>close dialog</button>

<!-- <button on:click={fetchData}>fetch data</button> -->

<!-- think about this name "values" -->
<Dialog bind:dialog={dialog} prop={dialog.props} openIf={true}>
	<input type="text" bind:value={inputValue}>
	<br>

	<div class="buttons">
		<button on:click={dialog.save}>Save</button>
		<button on:click={dialog.close}>Close</button>
	</div>
</Dialog>