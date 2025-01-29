<script>
  // Example data for the UI
  let recentImages = [
    "https://via.placeholder.com/150",
    "https://via.placeholder.com/150",
    "https://via.placeholder.com/150",
    "https://via.placeholder.com/150",
  ];

  let highlights = [
    { label: "Marathon", icon: "🏃" },
    { label: "Cycling", icon: "🚴" },
    { label: "Swimming", icon: "🏊" },
    { label: "Trail Run", icon: "🌲" },
  ];

  let maps = [
    "https://via.placeholder.com/300x200", // Example placeholder images for maps
    "https://via.placeholder.com/300x200",
    "https://via.placeholder.com/300x200",
    "https://via.placeholder.com/300x200",
  ];

  let user = {
    name: "John Doe",
    sports: ["🏃 Running", "🚴 Cycling"],
    location: "New York, USA",
    stats: {
      allTime: "All Time",
      activities: "800 activities",
      miles: "9000 miles",
      time: "300 h 53m",
      elevation: "1500 ft",
    },
  };
</script>

<style>
  /* Ensure circular images maintain proper aspect ratio */
  .circular {
    aspect-ratio: 1 / 1;
  }
</style>

<div class="max-w-4xl mx-auto p-4 space-y-6">
  <!-- Banner Section -->
  <div class="relative">
    <div class="grid grid-cols-4 gap-1 h-32 md:h-48">
      {#each recentImages as image}
        <img
          src={image}
          alt="Recent activity"
          class="w-full h-full object-cover"
        />
      {/each}
    </div>
    <!-- Profile Picture -->
    <div class="absolute left-1/2 transform -translate-x-1/2 bottom-0 translate-y-1/2">
      <img
        src="https://via.placeholder.com/100"
        alt="Profile"
        class="w-24 md:w-32 rounded-full border-4 border-white shadow-md circular"
      />
    </div>
  </div>

  <!-- Profile Info -->
  <div class="mt-12 text-center md:text-left md:flex md:justify-between">
    <div>
      <!-- Name -->
      <h1 class="text-xl font-bold">{user.name}</h1>
      <!-- Tagline -->
      <p class="text-sm text-gray-600 mt-1 flex items-center justify-center md:justify-start">
        {#each user.sports as sport, i}
          <span>{sport}</span>
          {#if i < user.sports.length - 1}
            <span class="mx-2">|</span>
          {/if}
        {/each}
        <span class="mx-2">|</span>
        <span class="flex items-center">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="w-4 h-4 mr-1 text-gray-600"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M17.657 16.657L13.414 20.9a2 2 0 01-2.828 0L6.343 16.657a8.001 8.001 0 1111.314 0z"
            />
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
            />
          </svg>
          {user.location}
        </span>
      </p>
    </div>
    <!-- All-Time Stats -->
    <div class="text-sm text-gray-600 mt-4 md:mt-0 md:ml-6 text-center md:text-right">
      <p class="font-medium text-gray-800">{user.stats.allTime}</p>
      <p>{user.stats.activities}</p>
      <p>{user.stats.miles}</p>
      <p>{user.stats.time}</p>
      <p>{user.stats.elevation}</p>
    </div>
  </div>

  <!-- Story Highlights -->
  <div>
    <h2 class="text-lg font-bold mb-2">Highlights</h2>
    <div class="flex space-x-4 overflow-x-auto scrollbar-hide">
      {#each highlights as highlight}
        <div class="flex-shrink-0 text-center">
          <div class="w-16 h-16 bg-gray-100 rounded-full flex items-center justify-center text-2xl">
            {highlight.icon}
          </div>
          <p class="text-sm mt-2">{highlight.label}</p>
        </div>
      {/each}
    </div>
  </div>

  <!-- Posts (Maps) -->
  <div>
    <h2 class="text-lg font-bold mb-2">Activities</h2>
    <div class="grid grid-cols-2 md:grid-cols-3 gap-4">
      {#each maps as map}
        <img
          src={map}
          alt="Activity Map"
          class="w-full h-40 md:h-48 object-cover rounded-lg"
        />
      {/each}
    </div>
  </div>
</div>