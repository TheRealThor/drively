<script>
  import { createEventDispatcher } from 'svelte';

	export let name;
  export let id;
  export let iconLink;
  export let webViewLink;

	const dispatch = createEventDispatcher();

	$: type = name.slice(name.lastIndexOf('.') + 1);

  function handleContextMenu(e) {
    dispatch('contextmenu', {id, clientX: e.clientX, clientY: e.clientY});
  }
</script>

<style>
	div {
		padding: 0 0 0 1.5em;
		background: 0 0.1em no-repeat;
		background-size: 1em 1em;
    user-select: none;
	}

  span {
    color: rgba(25, 23, 17, 0.7);
    font-weight: 500;
    text-decoration: none;
    display: block;
    cursor: pointer;
  }
</style>

<div draggable="true" on:contextmenu|preventDefault={handleContextMenu} style="background-image: url({iconLink})">
  <span on:click={e => {if (webViewLink !== '#') window.open(webViewLink, '_blank');}} href={webViewLink} target='_blank'>{name}</span>
</div>
