<script setup lang="ts"></script>

<template>
  <header>
    <div class="container d-flex flex-wrap">
      <ul class="nav me-auto">
        <li class="nav-item">
          <a
            href="\project\sandbox\index.html"
            class="nav-link link-body-emphasis px-2 active"
            aria-current="page"
            ><i class="bi bi-journal-album"></i> Dictionary</a
          >
        </li>
        <li class="nav-item">
          <a href="#" class="nav-link link-body-emphasis px-2"></a>
        </li>
        <li class="nav-item">
          <a href="#" class="nav-link link-body-emphasis px-2"></a>
        </li>
        <li class="nav-item">
          <a href="#" class="nav-link link-body-emphasis px-2"></a>
        </li>
        <li class="nav-item">
          <a href="#" class="nav-link link-body-emphasis px-2"></a>
        </li>
      </ul>
      <ul class="nav">
        <li class="nav-item">
          <div class="dropdown">
            <button
              class="btn btn-secondary dropdown-toggle"
              type="button"
              data-bs-toggle="dropdown"
              aria-expanded="false"
            >
              Select type
            </button>
            <ul class="dropdown-menu">
              <li><a class="dropdown-item" href="#">Verdana</a></li>
              <li><a class="dropdown-item" href="#">Serif</a></li>
              <li><a class="dropdown-item" href="#">Times New Roman</a></li>
            </ul>
          </div>
        </li>
        <li class="nav-item">
          <a href="#" class="nav-link link-body-emphasis px-2"
            ><i class="bi bi-moon-fill"></i> Dark Mode</a
          >
        </li>
      </ul>
    </div>
  </header>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
