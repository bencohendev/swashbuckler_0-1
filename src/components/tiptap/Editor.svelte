<script>
	import { onMount, onDestroy } from 'svelte';
	import { Editor } from '@tiptap/core';
	import StarterKit from '@tiptap/starter-kit';
	import Collaboration from '@tiptap/extension-collaboration';
	import { HocuspocusProvider } from '@hocuspocus/provider';

	let element;
	let editor;

	onMount(() => {
		// Set up the Hocuspocus WebSocket provider
		const provider = new HocuspocusProvider({
			url: 'ws://127.0.0.1:1234',
			name: 'example-document'
		});
		console.log(provider);
		editor = new Editor({
			element: element,
			extensions: [
				StarterKit,
				Collaboration.configure({
					document: provider.document
				})
			],
			content: '<p>Hello World! 🌍️ </p>',
			onTransaction: () => {
				// force re-render so `editor.isActive` works as expected
				editor = editor;
			}
		});
	});
	$: console.log(editor);
	onDestroy(() => {
		if (editor) {
			editor.destroy();
		}
	});
</script>

{#if editor}
	<button
		on:click={() => editor.chain().focus().toggleHeading({ level: 1 }).run()}
		class:active={editor.isActive('heading', { level: 1 })}
	>
		H1
	</button>
	<button
		on:click={() => editor.chain().focus().toggleHeading({ level: 2 }).run()}
		class:active={editor.isActive('heading', { level: 2 })}
	>
		H2
	</button>
	<button
		on:click={() => editor.chain().focus().setParagraph().run()}
		class:active={editor.isActive('paragraph')}
	>
		P
	</button>
{/if}

<div bind:this={element} />

<style>
	button.active {
		background: black;
		color: white;
	}
</style>
