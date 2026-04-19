<script lang="ts">
	import locationDeco from '$lib/assets/location-deco.svg';
	import { _ } from 'svelte-i18n';
	import { localeStore } from '../i18n.svelte';
	import { Clipboard, Github } from '@lucide/svelte';

	function copyAddress() {
		navigator.clipboard
			.writeText('서울 용산구 소월로 323')
			.then(() => alert($_('location.address_copied')))
			.catch(() => null);
	}
</script>

<section class="location">
	<h2 class="title {localeStore.locale}">{$_('location.title')}</h2>

	<p class="venue en">남산 한남 웨딩 가든</p>

	<button class="copy-address en" onclick={copyAddress}>
		<span class="clipboard-icon">
			<Clipboard size="1.1em" />
		</span>
		<span class="address">서울 용산구 소월로 323</span>
	</button>

	<div class="map">
		<iframe
			class="map-frame"
			title="남산 한남 웨딩 가든 지도"
			src="https://map.naver.com/p/entry/place/2145045060?placePath=%2Fhome"
			loading="lazy"
			referrerpolicy="no-referrer-when-downgrade"
		></iframe>
	</div>

	<p class="signature en">made with ♡ by Yejin & Hyun</p>

	<a
		class="github-icon"
		href="https://github.com/HyunLee103/wedding"
		target="_blank"
	>
		<Github size="1.1em" strokeWidth={1} />
	</a>

	<img class="location-deco" src={locationDeco} alt="" />
</section>

<style lang="scss">
	section.location {
		display: flex;
		flex-direction: column;
		align-items: center;
		background-color: $bg-color-1;
		padding: 1em 2em;
		position: relative;
	}

	.map {
		margin-top: 2em;
		width: 100%;
		height: 16em;
		margin-bottom: 7em;
	}

	.map-frame {
		width: 100%;
		height: 100%;
		border: 0;
		border-radius: 8px;
		box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
	}

	p.signature {
		font-size: 1rem;
	}

	.github-icon {
		margin-top: 0.2em;
		color: $font-color-default;
		cursor: pointer;
	}

	img.location-deco {
		position: absolute;
		bottom: 2.5em;
		right: 1.5em;
	}
</style>
