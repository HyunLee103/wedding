<script lang="ts">
	import photo1 from '$lib/assets/gallery/1.jpg';
	import photo2 from '$lib/assets/gallery/2.jpg';
	import photo3 from '$lib/assets/gallery/3.jpg';
	import photo4 from '$lib/assets/gallery/4.jpg';
	import photo5 from '$lib/assets/gallery/5.jpg';
	import photo6 from '$lib/assets/gallery/6.jpg';
	import photo7 from '$lib/assets/gallery/7.jpg';
	import photo8 from '$lib/assets/gallery/8.jpg';

	import PhotoSwipeLightBox from 'photoswipe/lightbox';
	import PhotoSwipe from 'photoswipe';
	import 'photoswipe/style.css';
	import { onMount } from 'svelte';
	import { localeStore } from '../i18n.svelte';
	import { _ } from 'svelte-i18n';

// Lightbox 최대 크기 제한
	const MAX_WIDTH = 1920;
	const MAX_HEIGHT = 1080;
	
// 이미지 크기 조정 함수
	function resizePhoto(w: number, h: number, maxW: number, maxH: number) {
		const ratio = Math.min(maxW / w, maxH / h, 1); // 1보다 크면 그대로
		return { width: Math.round(w * ratio), height: Math.round(h * ratio) };
	}
	
	const photosOriginal = [
		{ src: photo1, width: 1066, height: 1600 },
		{ src: photo2, width: 1067, height: 1600 },
		{ src: photo3, width: 1066, height: 1600 },
		{ src: photo4, width: 1066, height: 1600 },
		{ src: photo5, width: 1066, height: 1600 },
		{ src: photo6, width: 1066, height: 1600 },
		{ src: photo7, width: 1600, height: 1066 },
		{ src: photo8, width: 1066, height: 1600 }
	];

	// Lightbox용 최대 크기 적용
	const photos = photosOriginal.map(p => {
		const { width, height } = resizePhoto(p.width, p.height, MAX_WIDTH, MAX_HEIGHT);
		return { src: p.src, width, height };
	});

	onMount(() => {
		const lightbox = new PhotoSwipeLightBox({
			gallery: '#gallery',
			children: 'a',
			showHideAnimationType: 'fade',
			pswpModule: PhotoSwipe,
			zoom: false,           // 클릭시 확대 애니메이션 X
			wheelToZoom: false,    // 마우스 휠 확대 X
			pinchToZoom: false,    // 모바일 핀치 줌 X
			doubleTapToZoom: false, // 더블탭 확대 X
			maxScale: 1.5
		});
		lightbox.on('zoomPanUpdate', (detail) => {
			// scale이 1보다 커지면 강제로 1로 제한
			if (detail.scale > 1) {
				detail.instance.zoomTo(1, { x: 0, y: 0, time: 0 });
			}
		});
		lightbox.init();
		document.body.addEventListener('touchmove', (e) => {
		if ((e as TouchEvent).scale && (e as TouchEvent).scale !== 1) {
			e.preventDefault();
		}
	}, { passive: false });
	});
</script>

<section class="gallery">
	<div class="header">
		<h2 class="title {localeStore.locale}">{$_('gallery.title')}</h2>
	</div>
	<div id="gallery">
		{#each photos as photo}
			<a
				href={photo.src}
				class="slide"
				data-pswp-width={photo.width}
				data-pswp-height={photo.height}
				target="_blank"
			>
				<img class="thumbnail" src={photo.src} alt="" />
			</a>
		{/each}
	</div>
</section>

<style lang="scss">
.pswp {
  touch-action: pan-y; /* 세로 스크롤만 허용, 핀치 확대 막음 */
}

	section.gallery {
		padding: 4.5em 2em 2em 2em;
		background-color: $white;
	}

	.header {
		margin-bottom: 2em;
	}

	h2.title {
		text-align: center;
		color: $primary-color;
		&.en {
		font-size: 1.8rem;
		font-weight: 700;
		letter-spacing: 1px;
	}

	&.kr {
		font-size: 1.3rem;
		font-weight: 600;
		letter-spacing: 1px;
	}
	}

	#gallery {
		display: grid;
		gap: 1em;
		grid-template-columns: repeat(2, 1fr);
		grid-auto-rows: 6.5em;
		}

.slide {
	display: block;
	width: 100%;
}	

	img.thumbnail {
		border-radius: 4px;
		width: 100%;
		height: 100%;
		object-fit: cover;
	}

	.slide:nth-child(4) img.thumbnail {
		object-position: center 28%;
	}

	.slide:nth-child(1),
	.slide:nth-child(2),
	.slide:nth-child(3),
	.slide:nth-child(5),
	.slide:nth-child(7),
	.slide:nth-child(8) {
		grid-row: span 2;
	}

</style>
