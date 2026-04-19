<script lang="ts">
	import { _ } from 'svelte-i18n';
	import { localeStore } from '../i18n.svelte';
	import rsvpDeco from '$lib/assets/rsvp-deco.svg';
	import { Phone, Copy, CreditCard } from '@lucide/svelte';
	import locationTopWave from '$lib/assets/location-top-wave.svg';

	let groomOpen = $state(false);
	let brideOpen = $state(false);
	let toast = $state('');

	function copy(text: string) {
		navigator.clipboard.writeText(text);
		toast = '계좌 번호가 복사되었습니다.';
		setTimeout(() => (toast = ''), 2000);
	}
</script>

<img src={locationTopWave} class="location-top-wave" alt="" />
<section class="gift">
	<div class="header">
		<img class="header-deco" src={rsvpDeco} alt="" />
		<h2 class="title {localeStore.locale}">
			{$_('gift_info.title')}
		</h2>
	</div>

	<div class="accordion">

		<!-- 신랑측 -->
		<div class="group">
			<button class="group-title" on:click={() => (groomOpen = !groomOpen)}>
				신랑측
				<span>{groomOpen ? '−' : '+'}</span>
			</button>

			{#if groomOpen}
				<div class="people">

					<!-- 신랑 -->
					<div class="person">
						<p class="name">신랑 {$_('gift_info.groom.name')}</p>

						<div class="row center">
							<Phone size="16" />
							<a href={`tel:${$_('gift_info.groom.phone')}`}>
								{$_('gift_info.groom.phone')}
							</a>
						</div>

						<div class="row account">
							<CreditCard size="16" />
							<span>
								{$_('gift_info.groom.bank')} {$_('gift_info.groom.account')}
							</span>

							<button
								class="icon-btn"
								on:click={() =>
									copy($_('gift_info.groom.bank') + ' ' + $_('gift_info.groom.account'))
								}
							>
								<Copy size="14" />
							</button>
						</div>
					</div>

					<!-- 신랑 아버지 -->
					<div class="person">
						<p class="name">혼주 {$_('gift_info.groom_parents.father.name')}</p>
						<div class="row center">
							<Phone size="16" />
							<a href={`tel:${$_('gift_info.groom_parents.father.phone')}`}>
								{$_('gift_info.groom_parents.father.phone')}
							</a>
						</div>
						<div class="row account">
							<CreditCard size="16" />
							<span>
								{$_('gift_info.groom_parents.father.bank')}
								{' '}
								{$_('gift_info.groom_parents.father.account')}
							</span>

							<button
								class="icon-btn"
								on:click={() =>
									copy(
										$_('gift_info.groom_parents.father.bank') +
											' ' +
											$_('gift_info.groom_parents.father.account')
									)
								}
							>
								<Copy size="14" />
							</button>
						</div>
					</div>

					<!-- 신랑 어머니 -->
					<div class="person">
						<p class="name">혼주 {$_('gift_info.groom_parents.mother.name')}</p>
						<div class="row center">
							<Phone size="16" />
							<a href={`tel:${$_('gift_info.groom_parents.mother.phone')}`}>
								{$_('gift_info.groom_parents.mother.phone')}
							</a>
						</div>
						<div class="row account">
							<CreditCard size="16" />
							<span>
								{$_('gift_info.groom_parents.mother.bank')}
								{' '}
								{$_('gift_info.groom_parents.mother.account')}
							</span>

							<button
								class="icon-btn"
								on:click={() =>
									copy(
										$_('gift_info.groom_parents.mother.bank') +
											' ' +
											$_('gift_info.groom_parents.mother.account')
									)
								}
							>
								<Copy size="14" />
							</button>
						</div>
					</div>

				</div>
			{/if}
		</div>

		<!-- 신부측 -->
		<div class="group">
			<button class="group-title" on:click={() => (brideOpen = !brideOpen)}>
				신부측
				<span>{brideOpen ? '−' : '+'}</span>
			</button>

			{#if brideOpen}
				<div class="people">

					<!-- 신부 -->
					<div class="person">
						<p class="name">신부 {$_('gift_info.bride.name')}</p>

						<div class="row center">
							<Phone size="16" />
							<a href={`tel:${$_('gift_info.bride.phone')}`}>
								{$_('gift_info.bride.phone')}
							</a>
						</div>

						<div class="row account">
							<CreditCard size="16" />
							<span>
								{$_('gift_info.bride.bank')} {$_('gift_info.bride.account')}
							</span>

							<button
								class="icon-btn"
								on:click={() =>
									copy($_('gift_info.bride.bank') + ' ' + $_('gift_info.bride.account'))
								}
							>
								<Copy size="14" />
							</button>
						</div>
					</div>
					<!-- 신부 어머니 -->
					<div class="person">
						<p class="name">혼주 {$_('gift_info.bride_parents.mother.name')}</p>
						<div class="row center">
							<Phone size="16" />
							<a href={`tel:${$_('gift_info.bride_parents.mother.phone')}`}>
								{$_('gift_info.bride_parents.mother.phone')}
							</a>
						</div>
						<div class="row account">
							<CreditCard size="16" />
							<span>
								{$_('gift_info.bride_parents.mother.bank')}
								{' '}
								{$_('gift_info.bride_parents.mother.account')}
							</span>

							<button
								class="icon-btn"
								on:click={() =>
									copy(
										$_('gift_info.bride_parents.mother.bank') +
											' ' +
											$_('gift_info.bride_parents.mother.account')
									)
								}
							>
								<Copy size="14" />
							</button>
						</div>
					</div>

				</div>
			{/if}
		</div>

	</div>

	{#if toast}
		<div class="toast">{toast}</div>
	{/if}
</section>

<style lang="scss">
img.location-top-wave {
	max-width: $content-max-width;
	margin: auto;
}

.header {
	display: flex;
	flex-direction: column;
	align-items: center;
	text-align: center;
}

section.gift {
	padding: 3em 1.2em;
	max-width: $content-max-width;
	margin: 0 auto;
}

.group {
	margin-top: 1.2em;
	border-radius: 14px;
	background: white;
	border: 1px solid #eee;
}

.group-title {
	width: 100%;
	padding: 1em;
	font-weight: 600;
	background: none;
	display: flex;
	justify-content: space-between;
	font-size: 1rem;
}

.people {
	padding: 1em;
	border-top: 1px solid #f1f1f1;
}

.person {
	padding: 0.9em 0;
	border-bottom: 1px solid #f5f5f5;
}

.person:last-child {
	border-bottom: none;
}

.name {
	font-weight: 600;
	margin-bottom: 0.5em;
}

/* 가운데 정렬 */
.row.center {
	justify-content: center;
	text-align: center;
}

/* 링크 스타일 제거 */
.row a {
	color: inherit;
	text-decoration: none;
}

.row {
	display: flex;
	align-items: center;
	gap: 0.5em;
	font-size: 0.95rem;
	margin: 0.3em 0;
}

.account {
	position: relative;
	justify-content: center;
	text-align: center;
}

.account span {
	display: flex;
	align-items: center;
	gap: 0.4em;
}

.account .icon-btn {
	position: static;
}

.icon-btn {
	background: none;
	padding: 0.2em;
}

.send {
	margin-top: 0.7em;
	width: 100%;
	padding: 0.65em;

	background: white;
	border: 1px solid #ddd;
	border-radius: 8px;

	font-size: 0.95rem;
	font-weight: 500;
	color: #333;
}

.send:hover {
	background: #f7f7f7;
}

.toast {
	position: fixed;
	bottom: 3em;
	left: 50%;
	transform: translateX(-50%);

	background: rgba(0, 0, 0, 0.85);
	color: white;

	padding: 0.65em 1.2em;
	border-radius: 999px;

	font-size: 0.9rem;
	backdrop-filter: blur(8px);
}
</style>
