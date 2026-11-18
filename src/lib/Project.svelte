<script lang="ts">
	let props: {
		name: string;
		description: string;
		source?: string;
		link?: string;
	} = $props();
</script>

<article class="project-card">
	<h3>{props.name}</h3>
	<p>{props.description}</p>
	<div class="project-links">
		{#if props.source}
			<a
				href={props.source}
				target="_blank"
				rel="noreferrer"
			>Source</a>
		{/if}
		{#if props.link}
			<a
				href={props.link}
				target="_blank"
				rel="noreferrer"
			>Live</a>
		{/if}
	</div>
</article>
