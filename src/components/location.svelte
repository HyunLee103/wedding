<script lang="ts">
	import { onMount } from 'svelte';
	import locationDeco from '$lib/assets/location-deco.svg';
	import { _ } from 'svelte-i18n';
	import { localeStore } from '../i18n.svelte';
	import { Clipboard } from '@lucide/svelte';
	import { PUBLIC_NAVER_MAPS_API_KEY } from '$env/static/public';

	const naverMapsKey = PUBLIC_NAVER_MAPS_API_KEY;

	function copyAddress() {
		navigator.clipboard
			.writeText('서울 용산구 소월로 323')
			.then(() => alert($_('location.address_copied')))
			.catch(() => null);
	}

	onMount(() => {
		const script = document.createElement('script');
		script.src = `https://oapi.map.naver.com/openapi/v3/maps.js?ncpKeyId=${naverMapsKey}`;
		script.async = true;

		script.onload = () => {
			const map = new naver.maps.Map('naverMap', {
				center: new naver.maps.LatLng(37.541522, 126.997032),
				zoom: 15
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

	<p class="venue">남산 한남 웨딩 가든</p>

	<button class="copy-address" onclick={copyAddress}>
		<span class="clipboard-icon">
			<Clipboard size="1.1em" />
		</span>
		<span class="address">서울 용산구 소월로 323</span>
	</button>

	<div class="map">
		<div id="naverMap" class="naver-map"></div>
	</div>

	<div class="location-guide kr">
		<p class="guide-line">
			예식장 내 주차 공간이 마련되어 있지 않아 대중교통 이용을 부탁드립니다.
		</p>
		<p class="guide-line shuttle-line"><strong>셔틀</strong> 한강진역 2번 출구 앞 탑승</p>
		<div class="parking-list">
			<p class="parking-title">인근 주차장</p>
			<ul>
				<li>그랜드 하얏트 서울 주차장 (서울 용산구 한남동 747-7)</li>
				<li>이태원2동 공영 주차장 (서울 용산구 회나무로 55)</li>
				<li>삼호민영주차장 (서울 용산구 회나무로 85 삼호주차장)</li>
			</ul>
		</div>
		<div class="atm-list">
			<p class="atm-title">ATM</p>
			<p class="guide-line">예식장 내 ATM이 없어 하얏트 호텔 본관 ATM 이용을 부탁드립니다.</p>
		</div>
	</div>

	<img class="location-deco" src={locationDeco} alt="" />
</section>

<style lang="scss">
	section.location {
		display: flex;
		flex-direction: column;
		align-items: center;
		background-color: $bg-color-1;
		font-family: 'Noto Serif KR', serif;
		padding: 1em 2em 2.7em;
		position: relative;
	}

	.venue {
		margin-top: 0.2rem;
		font-size: 1.05rem;
		line-height: 1.6;
		text-align: center;
	}

	.copy-address {
		margin-top: 0.25rem;
		display: inline-flex;
		align-items: center;
		gap: 0.45rem;
		font-size: 0.95rem;
		line-height: 1.6;
		text-align: center;
	}

	.map {
		margin-top: 2em;
		width: 100%;
		height: 16em;
		margin-bottom: 1.5em;
	}

	.naver-map {
		width: 100%;
		height: 100%;
		border-radius: 8px;
		box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
	}

	.location-guide {
		width: 100%;
		padding: 1.1rem 1rem;
		border-radius: 14px;
		background: rgba(255, 255, 255, 0.72);
		box-shadow: 0 10px 24px rgba(0, 0, 0, 0.06);
		backdrop-filter: blur(6px);
	}

	.guide-line,
	.parking-title,
	.atm-title,
	.parking-list li {
		color: $font-color-default;
		font-size: 0.92rem;
		line-height: 1.75;
		word-break: keep-all;
	}

	.guide-line + .guide-line {
		margin-top: 0.35rem;
	}

	.shuttle-line {
		margin-top: 0.75rem;
		padding-top: 0.75rem;
		border-top: 1px solid rgba(185, 148, 147, 0.24);
	}

	.guide-line strong {
		display: inline-block;
		margin-right: 0.35rem;
		color: $primary-color-dark;
		font-weight: 700;
	}

	.parking-list {
		margin-top: 0.75rem;
	}

	.parking-title,
	.atm-title {
		font-weight: 700;
		color: $primary-color-dark;
		margin-bottom: 0.35rem;
	}

	.parking-list ul {
		margin: 0;
		padding-left: 1.1rem;
	}

	.parking-list li + li {
		margin-top: 0.35rem;
	}

	.atm-list {
		margin-top: 0.85rem;
		padding-top: 0.85rem;
		border-top: 1px solid rgba(185, 148, 147, 0.24);
	}

	img.location-deco {
		position: absolute;
		bottom: 2.3em;
		right: 1.5em;
	}

	@media (max-width: 640px) {
		section.location {
			padding: 1em 1.25em 2.85em;
		}

		.location-guide {
			padding: 1rem 0.95rem;
		}

		.venue {
			font-size: 1rem;
		}

		.copy-address {
			font-size: 0.9rem;
		}

		.guide-line,
		.parking-title,
		.parking-list li,
		.atm-title {
			font-size: 0.88rem;
			line-height: 1.7;
		}
	}
</style>
