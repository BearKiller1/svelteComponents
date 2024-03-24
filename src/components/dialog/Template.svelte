<script>
    // CHANGE THIS
	import Dialog from './Dialog.svelte';

	let dialog = {
		save: saveDialog,
	
		props: {
			title: 'Title from the parent',
		},
	};

	function saveDialog(){
		console.log(dialog.values);
	}
    
</script>

<button on:click={dialog.open}>Open Dialog</button>
<!-- THIS WORKS BUT NOT LOGICAL TO HAVE IT -->
<button on:click={dialog.close}>close dialog</button>

<!-- 
	Dialog params:bind:

	bind:dialog - takes all the parameters and functions
	and bind it to the variable we give it to.
	in this case variable is named as "dialog" and it stores:
		values (array) - with all the elements names & values
		open (function) - lets u open the dialog  


	prop - takes all the addition data such as:
	title; bg (background); dragable etc.
	
	openIf - takes boolean parameter. and on that
	there is a listener, if its value becomes true,
	dialog is open automaticly
 -->
 
<!-- think about this name "values" -->
<Dialog 
  bind:dialog={dialog} 
  prop={dialog.props} 
  openIf={false}
  >
	<input type="text" id="name"    placeholder="name"      value="defName">
	<input type="text" id="surname" placeholder="surname"   value="defSurname">
	<input type="text" id="age"     placeholder="age"       value="12">
	<input type="text" id="email"   placeholder="email"     value="defEmail">

 	<select id="position">
		<option >noob</option>
		<option selected>beginer</option>
		<option>legend</option>
	</select>
 
	<br>

	<div class="buttons">
		<button on:click={dialog.save}>Save</button>
		<button on:click={dialog.close}>Close</button>
	</div>
</Dialog>