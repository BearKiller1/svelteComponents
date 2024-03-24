<script>
    import { onMount } from 'svelte';

	import './Dialog.css';
	import Draggable from '../dragable/Draggable.svelte';

 	export let prop;
	export let dialog;
	export let openIf;
	
	let values = []; // Initialize your variable
	let toggle = false;
	let observer; // Declare the observer variable

	function open() {
		toggle = true;
		storeValues();
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

	function storeValues(){
		// Create a new observer instance
		observer = new MutationObserver((mutationsList, observer) => {
			for (let mutation of mutationsList) {
				if (mutation.type === 'childList') {
					const slotContent = document.querySelector('.lucidContent');

					if (slotContent) {
						slotContent.childNodes.forEach((node, i) => {

							// add element inside array as soon as it is observed
							if(node.id != undefined && node.id != ""){
								values[node.id] = node.value ? node.value : ""
							}

							if (node.nodeName === 'INPUT') {
								if (!node.id) {
									let id = node.nodeName + `${Math.random().toString(36).substr(2, 9)}`;
									node.id = id;
								}

								node.addEventListener('input', (event) => {
									values[node.id] = event.target.value;
								});
							} else if(node.nodeName === "SELECT"){
								if (!node.id) {
									let id = node.nodeName + `${Math.random().toString(36).substr(2, 9)}`;
									node.id = id;
								}

								node.addEventListener('change', (event) => {
									values[node.id] = event.target.value;
								});
							}
						});

						observer.disconnect(); // Stop observing once slots are inserted
						break;
					}
				}
			}
		});

		// Start observing the target node for childList mutations
		observer.observe(document.body, { childList: true, subtree: true });
	};

	onMount(() => {
		if (openIf) {
			open();
		}
	});

	// check props
	if(prop.bg == undefined){
		prop.bg = true;
	}
</script>


{#if toggle}
	{#if prop.bg}
		<div class="lucidBackground"></div>
	{/if}
	<!-- TODO make draggable optionable param -->
	<Draggable>
		<div class="lucidDialog">
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<h1 class="lucidClose" on:click={close}>x</h1>
			<h1 class="lucidTitle">{prop.title	? prop.title : 'Title'}</h1>
			
			<div class="lucidContent">
				<slot></slot>
			</div>
		</div>
	</Draggable>
{/if}
