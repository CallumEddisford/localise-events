<script>
  import dayjs from "dayjs";
  import CreateEvent from "../lib/Event/Create.svelte";
  import EventList from "../lib/Event/List.svelte";
  import logo from "../assets/iconmonstr-clock-thin.svg"

  let isCreating = false;
  let events = JSON.parse(localStorage.getItem("events")) || [];
  events = events.sort(
    (a, b) => {
      console.log(a);
      return dayjs(`${b.startDate}T${b.startTime}`).valueOf() - dayjs(`${a.startDate}T${a.startTime}`).valueOf()
    }  
  );

  function toggleModal() {
    isCreating = !isCreating;
  }

  function deleteEvent(title) {
    const eventIndex = events.findIndex((event) => event.title !== title);
    events.splice(eventIndex, 1);
    $: events = events;
    localStorage.setItem("events", JSON.stringify(events));
  }

  function handleSubmit(event) {
    const formData = new FormData(event.target);
    const data = {};
    for (let field of formData) {
      const [key, value] = field;
      data[key] = value;
    }

    events = [...events, data];

    localStorage.setItem("events", JSON.stringify(events));
    isCreating = !isCreating;
  }
</script>

<main>
  <div class="h-screen md:flex">
    <div
      class="relative
            overflow-hidden
            md:flex
            w-1/3
            i 
            hidden 
            bg-gradient-to-r
            from-pink-500
            via-red-500
            to-yellow-500
            background-animate"
    >
      <div class="w-full flex justify-center items-center border-r-2">
        <div class="px-4 text-center text-white">
          <img src="{logo}" alt="Logo" class="h-10 mx-auto mb-2" />
          <h1 class="font-bold text-4xl font-sans">EventLocaliser</h1>
          <p class="mt-1">Localise and track events in different timezones!</p>
        </div>
      </div>
    </div>
    <div class="relative md:w-2/3 bg-white p-10 pt-0 overflow-x-scroll h-full">
      <nav
        class="rounded-lg mt-5 border z-1 bg-white w-1/3 top-0 left-0 w-full p-4 shadow-lg sticky"
      >
        <div class="flex items-center">
          <div class="w-1/2 text-xl font-extrabold text-pink-400">EventLocaliser</div>
          <div class="w-1/2 text-center text-right self-end">
            {#if events.length}
              <button
                on:click={toggleModal}
                type="button"
                class="text-white bg-blue-500 hover:bg-blue-800 font-medium rounded-lg text-sm px-5 py-2"
                >Add an Event</button
              >
            {/if}
          </div>
        </div>
      </nav>
      <div class="pt-10">
        <div class="px-4 text-center md:hidden mb-10">
          <h1 class="font-bold text-4xl font-sans">EventLocaliser</h1>
          <p class="mt-1">Localise and track events in different timezones!</p>
        </div>
        <EventList {events} toggleModal={toggleModal} deleteEvent={deleteEvent} />
      </div>
    </div>
  </div>

  {#if isCreating}
  <CreateEvent
    on:closeModal={toggleModal}
    {handleSubmit}
  />
  {/if}
</main>
