<script>
    import { onMount } from 'svelte';
	import './Dialog.css';
 	export let prop;
	
	export let dialog;
	export let openIf;
	
	let values = []; // Initialize your variable
	let toggle = false;

	// this guy is used everywhere
	function open() {
		toggle = true;
	}

	function close(){
		toggle = false;
		openIf = false;
	}

	dialog = {
		// send functions back to parent
		...dialog,
		open,
		close,
		values,
	};

	
	$: {
		// awailable when called param
		if (openIf) {
			open();
		}
  	}


	onMount(() => {
		const slotContent = document.querySelector('.lucidContent');
		if (slotContent) {
			slotContent.childNodes.forEach( (node, i) => {
				if (node.nodeName === 'INPUT') {
					if(!node.id){
						let id = node.nodeName + `${Math.random().toString(36).substr(2, 9)}`;
						node.id = id;
					}

					node.addEventListener('input', (event) => {
						values[node.id] = event.target.value;
					});
				}
			});
		}

	});
</script>


{#if toggle}
<div class="lucidBackground"></div>

<div class="lucidDialog">
	<!-- svelte-ignore a11y-click-events-have-key-events -->
	<h1 class="lucidClose" on:click={close}>x</h1>
	<h1 class="lucidTitle">{prop.title	? prop.title : 'Title'}</h1>

	<div class="lucidContent">
		<slot></slot>
	</div>
</div>
{/if}