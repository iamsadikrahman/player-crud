<script setup>
import { ref, onBeforeMount } from "vue";

const players = ref([]);

onBeforeMount(() => {
  fetch("http://localhost:5000/players")
    .then((response) => response.json())
    .then((data) => {
      players.value = data;
    });
});
</script>

<template>
  <h1 class="text-3xl font-bold text-center shadow py-5 rounded">
    Player CRUD Operations
  </h1>
  <section class="flex justify-between my-10 bg-gray-100 py-10 px-2 rounded shadow">
    <input class="border px-2 py-2 rounded border-black" type="text" placeholder="Name" />
    <input class="border px-2 py-2 rounded border-black" type="text" placeholder="Team" />
    <input
      class="border px-2 py-2 rounded border-black"
      type="text"
      placeholder="Highest Score"
    />
    <button class="bg-green-500 text-white py-3 px-5 rounded font-semibold" type="button">
      Add New Player
    </button>
  </section>
  <table class="table-fixed w-full border text-center text-lg">
    <thead class="font-semibold text-green-900">
      <tr class="py-4 shadow">
        <td class="py-5">Name</td>
        <td class="py-5">Team</td>
        <td class="py-5">Highest Score</td>
        <td class="py-5">Actions</td>
      </tr>
    </thead>
    <tbody class="text-gray-700 font-medium">
      <tr class="shadow" v-for="player in players" :key="player._id">
        <td class="py-5">{{ player.name }}</td>
        <td class="py-5">{{ player.team }}</td>
        <td class="py-5">{{ player.highest_score }}</td>
        <td class="py-4 flex items-center justify-center space-x-4">
          <button class="bg-yellow-500 text-white py-1.5 px-5 rounded font-semibold">
            Edit
          </button>
          <button class="bg-red-500 text-white py-1.5 px-5 rounded font-semibold">
            Delete
          </button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<style scoped></style>
