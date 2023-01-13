<script>
  import timezones from 'timezones-list';
  import dayjs from "dayjs";
  import utc from "dayjs/plugin/utc";
  import timezone from "dayjs/plugin/timezone"
  import relativeTime from "dayjs/plugin/relativeTime"
  import { onMount } from "svelte";
  

  dayjs.extend(utc);
  dayjs.extend(timezone);
  dayjs.extend(relativeTime);
  
  export let title;
  export let location;
  export let startDate;
  export let startTime;
  export let endDate;
  export let endTime;
  export let deleteEvent;

  const start = `${startDate}T${startTime}`;
  const end = `${endDate}T${endTime}`;
  let countdown = null;

  function getCountry() {
    return timezones.find((country) => country.tzCode === location);
  }

  function when() {
    const remoteTime = dayjs.tz(start, "MM-DD-YYYY", getCountry().tzCode);

    return dayjs(remoteTime).fromNow();
  }

  function status() {
    const now = dayjs();
    const nowLocal = dayjs.tz(now, "MM-DD-YYYY", getCountry().tzCode);
    const endtime = dayjs.tz(end, "MM-DD-YYYY", getCountry().tzCode);
    const startTime = dayjs.tz(start, "MM-DD-YYYY", getCountry().tzCode);

    if(nowLocal > startTime && nowLocal < endtime) {
      return {
        text: 'active',
        color: 'black',
        bg: 'green'
      }
    }
    else if(nowLocal > endtime) {
      return {
        text: 'ended',
        color: 'black',
        bg: 'red'
      }
    }
    else if(nowLocal < startTime) {
      return {
        text: 'upcoming',
        color: 'black',
        bg: 'orange'
      }
    }
  }

  onMount(() => {
		const interval = setInterval(() => {
			countdown = when();
		}, 1000);

		return () => {
			clearInterval(interval);
		};
	});
</script>

<div
  class="block rounded-lg shadow-lg bg-white text-center border border-gray-100"
>
  <h4 class="py-3 px-6 text-l font-medium border-b border-gray-300 bg-{status().bg}-500 rounded-t-lg">
    {title}: {status().text}
  </h4>
  <div class="p-6">
    <h5 class="text-gray-900 text-xl font-medium mb-2">
      {#if countdown}
        {countdown}
      {:else}
        Loading...
      {/if}
    </h5>
  </div>
  <p class="text-gray-800 font-medium text-base border-b border-t border-gray-300">
    Event information
  </p>
  <div class="flex gap-3 items-center text-left p-4 pb-0">
    <div class="text-center w-1/3">
      {getCountry().name}
    </div>
    <div>
      <p class="text-gray-700 font-medium text-base mr-5">
        Starts:
      </p>
      <p class="text-gray-700 text-base">
        {dayjs(start).format('MMMM DD YYYY, hh:mm:ss a')}
      </p>
      <p class="text-gray-700 font-medium text-base mr-5">
        Ends:
      </p>
      <p class="text-gray-700 text-base">
        {dayjs(end).format('MMMM DD YYYY, hh:mm:ss a')}
      </p>
    </div>
  </div>
  <div class="items-center text-center text-red-500">
    <button on:click={() => deleteEvent()}>delete event</button>
  </div>

</div>
