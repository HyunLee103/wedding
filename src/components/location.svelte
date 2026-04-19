<script lang="ts">
	import { onMount } from 'svelte';
	import locationDeco from '$lib/assets/location-deco.svg';
	import { _ } from 'svelte-i18n';
	import { localeStore } from '../i18n.svelte';
	import { Clipboard, Github } from '@lucide/svelte';
	import { PUBLIC_NAVER_MAPS_API_KEY } from '$env/static/public';

	const naverMapUrl = 'https://naver.me/FAPXf05C';
	const hasNaverMapKey = Boolean(PUBLIC_NAVER_MAPS_API_KEY);

	function copyAddress() {
		navigator.clipboard
			.writeText('서울 용산구 소월로 323')
			.then(() => alert($_('location.address_copied')))
			.catch(() => null);
	}

	onMount(() => {
		if (!hasNaverMapKey) return;

		const script = document.createElement('script');
		script.src = `https://oapi.map.naver.com/openapi/v3/maps.js?ncpKeyId=${PUBLIC_NAVER_MAPS_API_KEY}`;
		script.async = true;

		script.onload = () => {
			const map = new naver.maps.Map('naverMap', {
				center: new naver.maps.LatLng(37.541522, 126.997032),
				zoom: 17
			});

			new naver.maps.Marker({
				position: new naver.maps.LatLng(37.541522, 126.997032),
				map,
				title: '남산 한남 웨딩 가든'
			});
		};

		document.head.appendChild(script);

		return () => {
			script.remove();
		};
	});
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
		{#if hasNaverMapKey}
			<div id="naverMap" class="naver-map"></div>
		{:else}
			<a class="naver-map-link" href={naverMapUrl} target="_blank" rel="noreferrer">
				네이버 지도에서 보기
			</a>
		{/if}
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

	.naver-map {
		width: 100%;
		height: 100%;
		border-radius: 8px;
		box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
	}

	.naver-map-link {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100%;
		border-radius: 8px;
		background: #f4f1ec;
		color: $primary-color;
		font-weight: 600;
		text-decoration: none;
		box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
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
