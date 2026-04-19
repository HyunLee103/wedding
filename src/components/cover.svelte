<script lang="ts">
	import { browser } from '$app/environment';
	import { Confetti } from 'svelte-confetti';
	import coverImage from '$lib/assets/cover.jpg';

	const maxSectionHeight = 900;
	let sectionHeight = $state(maxSectionHeight);

	function setSectionHeight() {
		sectionHeight = window.innerHeight < maxSectionHeight ? window.innerHeight : maxSectionHeight;
	}

	if (browser && window.matchMedia('(max-width: 1024px)')) {
		setSectionHeight();
	}
</script>

<section
	style:height={`${sectionHeight}px`}
	style:background-image={`url(${coverImage})`}
	class="cover"
>
	<div class="confetti-area">
		<Confetti
			x={[-5, 5]}
			y={[0, 0.1]}
			colorArray={['#588adb', '#f5e298', '#fff', '#9aa3f5']}
			delay={[500, 2000]}
			infinite
			duration={5000}
			amount={70}
			fallDistance={`${sectionHeight}px`}
		/>
	</div>

	<div class="names-kr-box">
		<span class="names kr">이현</span>
		<span class="names kr">그리고</span>
		<span class="names kr">김예진</span>
	</div>
</section>

<style lang="scss">
	section.cover {
		position: relative;
		background-repeat: no-repeat;
		background-position: center center;
		background-size: cover;
	}
	.confetti-area {
		position: absolute;
		top: -50px;
		left: -50px;
		height: 100vh;
		width: 100%;
		overflow: hidden;
		pointer-events: none;
	}
	.names-kr-box {
		position: absolute;
		top: 2.2em;
		left: 2em;
		z-index: 1;

		span.names {
			color: $white;
			display: block;
			font-size: 1rem;
			font-weight: 500;
			letter-spacing: 0.45em;
			line-height: 2;
			text-shadow: 0 2px 10px rgba(0, 0, 0, 0.28);
		}
	}

	@media (max-width: 640px) {
		.names-kr-box {
			top: 2em;
			left: 1.5em;

			span.names {
				font-size: 0.92rem;
				letter-spacing: 0.38em;
			}
		}
	}
</style>
