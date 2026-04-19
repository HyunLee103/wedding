<script lang="ts">
	import { Github } from '@lucide/svelte';
</script>

<footer class="site-footer">
	<a
		class="github-icon"
		href="https://github.com/HyunLee103/wedding"
		target="_blank"
		rel="noreferrer"
		aria-label="GitHub repository"
	>
		<Github size="1.1em" strokeWidth={1} />
	</a>

	<p class="signature en">Made with ♡ by Yejin & Hyun</p>
</footer>

<style lang="scss">
	.site-footer {
		padding: 0.6rem 1.2rem 2.1rem;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 0.45rem;
		background-color: $bg-color-1;
	}

	.github-icon {
		color: $font-color-default;
		cursor: pointer;
	}

	.signature {
		margin: 0;
		font-size: 1rem;
	}

	@media (max-width: 640px) {
		.site-footer {
			padding: 0.35rem 1rem 1.8rem;
		}
	}
</style>
