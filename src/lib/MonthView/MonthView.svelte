<script>
    import {DateTime} from "luxon";

    export let currentMonth = DateTime.local().month;
    export let currentYear = DateTime.local().year;
    const dateTime = DateTime.fromObject({
        month: currentMonth,
        year: currentYear,
    });
    const firstDayOfMonth = dateTime.startOf("month");
    const firstDayOfView = firstDayOfMonth.startOf("week");
    const lastDayOfMonth = dateTime.endOf("month");
    const lastDayOfView = lastDayOfMonth.endOf("week");
    const nDays = lastDayOfView.diff(firstDayOfMonth, "days").days;
    const days = Array.apply(null, { length: Math.ceil(nDays)}).map((_, i) => {
        return firstDayOfView.plus({ days: i });
    });
</script>

<div class="month-view-container">
    <p class="month-view-title">
        {dateTime.monthLong} {dateTime.year}
    </p>
    <div class="month-view-weeks" >
        {#each days as day}
            <div class="month-view-day">
                {day.weekdayShort}
                {day.day}
            </div>
        {/each} 
    </div>
</div>

<style>
    .month-view-title {
        font-size: 1.5rem;
        font-weight: bold;
        text-transform: capitalize;
    }
    .month-view-weeks {
        display: flex;
        flex-wrap: wrap;
    }
    .month-view-day {
        flex: 1 0 14%;
    }
</style>

