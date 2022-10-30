<template>
  <div class="context-menu-wrapper">
    <ul class="menu-items-list">
      <li class="menu-item" @click="completeTask">Complete</li>
      <li class="menu-item" @click="deleteTask">Delete</li>
      <li class="menu-item" @click="editTask">Edit</li>
    </ul>
  </div>
</template>

<style>
.context-menu-wrapper {
  width: 120px;
  background: lightblue;
  border-radius: 5px;
}

.menu-items-list {
  padding: 0;
}

.menu-item {
  list-style-type: none;
  padding: 6px 15px;
  text-align: left;
  border-bottom: 1px solid grey;
  border-radius: 5px 5px 0 0;
}

.menu-item:hover {
  cursor: pointer;
  background: lightgrey;
}

.menu-item:last-child {
  border: none;
  border-radius: 0 0 5px 5px;
}
</style>
