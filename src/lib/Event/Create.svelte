<script>
  import { createEventDispatcher } from "svelte";
  import timezones from "timezones-list";

  const countries = timezones.sort((a, b) => a.label.localeCompare(b.label));

  export let handleSubmit;

  const dispatch = createEventDispatcher();
</script>

<div class="fixed inset-0 bg-black opacity-75" />
<div
  class="min-h-screen py-6 flex flex-col justify-center sm:py-12 fixed inset-0 z-10"
>
  <div class="relative py-3 sm:max-w-xl sm:mx-auto">
    <div
      class="relative px-4 py-10 mx-8 md:mx-0 shadow rounded-3xl sm:p-10 bg-white"
    >
      <form on:submit|preventDefault={handleSubmit} class="max-w-md mx-auto">
        <div class="flex items-center space-x-5">
          <div
            class="h-14 w-14 bg-yellow-200 rounded-full flex flex-shrink-0 justify-center items-center text-yellow-500 text-2xl font-mono"
          >
            i
          </div>
          <div
            class="block pl-2 font-semibold text-xl self-start text-gray-700"
          >
            <h2 class="leading-relaxed">Add an Event</h2>
            <p class="text-sm text-gray-500 font-normal leading-relaxed">
              Add an event happening in another timezone.
            </p>
          </div>
        </div>
        <div class="divide-y divide-gray-200">
          <div
            class="py-8 text-base leading-6 space-y-4 text-gray-700 sm:text-lg sm:leading-7"
          >
            <div class="flex flex-col">
              <label for="title" class="leading-loose">Event Title</label>
              <input
                id="title"
                name="title"
                type="text"
                class="px-4 py-2 border focus:ring-gray-500 focus:border-gray-900 w-full sm:text-sm border-gray-300 rounded-md focus:outline-none text-gray-600"
                placeholder="Event title"
              />
            </div>
            <div class="flex flex-col">
              <label for="location" class="leading-loose"
                >Where is the event taking place?</label
              >
              <select
                id="location"
                name="location"
                class="px-4 py-2 border focus:ring-gray-500 focus:border-gray-900 w-full sm:text-sm border-gray-300 rounded-md focus:outline-none text-gray-600"
              >
                {#each countries as country}
                  <option value={country.tzCode}>{country.label}</option>
                {/each}
              </select>
            </div>
            <div class="flex items-center space-x-4">
              <div class="flex flex-col w-1/2">
                <label for="startDate" class="leading-loose">Start Date</label>
                <div class="relative focus-within:text-gray-600 text-gray-400">
                  <input
                    id="startDate"
                    name="startDate"
                    type="date"
                    class="pr-4 pl-10 py-2 border focus:ring-gray-500 focus:border-gray-900 w-full sm:text-sm border-gray-300 rounded-md focus:outline-none text-gray-600"
                    placeholder="25/02/2020"
                  />
                  <div class="absolute left-3 top-2">
                    <svg
                      class="w-6 h-6"
                      fill="none"
                      stroke="currentColor"
                      viewBox="0 0 24 24"
                      xmlns="http://www.w3.org/2000/svg"
                      ><path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
                      /></svg
                    >
                  </div>
                </div>
              </div>
              <div class="flex flex-col w-1/2">
                <label for="startTime" class="leading-loose">Start Time</label>
                <div class="relative focus-within:text-gray-600 text-gray-400">
                  <input
                    id="startTime"
                    name="startTime"
                    type="time"
                    class="pr-4 pl-10 py-2 border focus:ring-gray-500 focus:border-gray-900 w-full sm:text-sm border-gray-300 rounded-md focus:outline-none text-gray-600"
                    placeholder="26/02/2020"
                  />
                  <div class="absolute left-3 top-2">
                    <svg
                      class="w-6 h-6"
                      fill="none"
                      stroke="currentColor"
                      viewBox="0 0 24 24"
                      xmlns="http://www.w3.org/2000/svg"
                      ><path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
                      /></svg
                    >
                  </div>
                </div>
              </div>
            </div>
            <div class="flex items-center space-x-4">
              <div class="flex flex-col w-1/2">
                <label for="endDate" class="leading-loose">End Date</label>
                <div class="relative focus-within:text-gray-600 text-gray-400">
                  <input
                    id="endDate"
                    name="endDate"
                    type="date"
                    class="pr-4 pl-10 py-2 border focus:ring-gray-500 focus:border-gray-900 w-full sm:text-sm border-gray-300 rounded-md focus:outline-none text-gray-600"
                    placeholder="25/02/2020"
                  />
                  <div class="absolute left-3 top-2">
                    <svg
                      class="w-6 h-6"
                      fill="none"
                      stroke="currentColor"
                      viewBox="0 0 24 24"
                      xmlns="http://www.w3.org/2000/svg"
                      ><path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
                      /></svg
                    >
                  </div>
                </div>
              </div>
              <div class="flex flex-col w-1/2">
                <label for="endTime" class="leading-loose">End Time</label>
                <div class="relative focus-within:text-gray-600 text-gray-400">
                  <input
                    id="endTime"
                    name="endTime"
                    type="time"
                    class="pr-4 pl-10 py-2 border focus:ring-gray-500 focus:border-gray-900 w-full sm:text-sm border-gray-300 rounded-md focus:outline-none text-gray-600"
                    placeholder="26/02/2020"
                  />
                  <div class="absolute left-3 top-2">
                    <svg
                      class="w-6 h-6"
                      fill="none"
                      stroke="currentColor"
                      viewBox="0 0 24 24"
                      xmlns="http://www.w3.org/2000/svg"
                      ><path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"
                      /></svg
                    >
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="pt-4 flex items-center space-x-4">
            <button
              on:click={() => dispatch("closeModal")}
              class="flex justify-center items-center w-full text-gray-900 px-4 py-3 rounded-md focus:outline-none"
            >
              <svg
                class="w-6 h-6 mr-3"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
                ><path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M6 18L18 6M6 6l12 12"
                /></svg
              > Cancel
            </button>
            <button
              type="submit"
              class="bg-blue-500 flex justify-center items-center w-full text-white px-4 py-3 rounded-md focus:outline-none"
              >Create</button
            >
          </div>
        </div>
      </form>
    </div>
  </div>
</div>
