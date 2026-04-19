<script lang="ts">
	import sundayCol from '$lib/assets/calendar/calendar-sunday.svg';
	import mondayCol from '$lib/assets/calendar/calendar-monday.svg';
	import tuesdayCol from '$lib/assets/calendar/calendar-tuesday.svg';
	import wednesdayCol from '$lib/assets/calendar/calendar-wednesday.svg';
	import thursdayCol from '$lib/assets/calendar/calendar-thursday.svg';
	import fridayCol from '$lib/assets/calendar/calendar-friday.svg';
	import saturdayCol from '$lib/assets/calendar/calendar-saturday.svg';
	import calendarDeco from '$lib/assets/calendar-deco.svg';
</script>

<section class="calendar">
	<h2 class="title en">May</h2>
	<div class="calendar-content">
		<img class="week-col" src={sundayCol} alt="sunday column" />
		<img class="week-col" src={mondayCol} alt="monday column" />
		<img class="week-col" src={tuesdayCol} alt="tuesday column" />
		<img class="week-col" src={wednesdayCol} alt="wednesday column" />
		<img class="week-col" src={thursdayCol} alt="thursday column" />
		<img class="week-col" src={fridayCol} alt="friday column" />
		<img class="week-col" src={saturdayCol} alt="saturday column" />
	</div>
	<img class="calendar-deco" src={calendarDeco} alt="calendar deco" />
</section>

<style lang="scss">
	.calendar {
	position: relative;
	background-color: $white;
	padding: 2em 3.5em 4em 3.5em;

	.title {
		color: $primary-color;
		font-size: 1.8rem;
		font-weight: 700;
		text-align: center;
		margin-bottom: 1em;
	}

	.calendar-content {
		display: flex;
		justify-content: space-between;
		width: 100%;
		max-width: $content-max-width;  /* 컬럼 전체 최대 폭 */
		margin: 0 auto;    /* 중앙 정렬 */
	}

	.week-col {
		height: 100%;       /* 기존 높이 유지 */
		width: auto;        /* 모바일에서 비율 유지 */
	}

	img.calendar-deco {
		position: absolute;
		bottom: 0.5em;
		right: 2.5em;
	}

@media (max-width: 768px) {
  .calendar-content {
    display: flex;
    flex-wrap: nowrap;         /* 한 줄 유지 */
    justify-content: center;
    align-items: flex-start;   /* 상단 기준 정렬 */
    gap: 0.2em;                /* gap 줄이기 */
  }
  }
}
</style>
