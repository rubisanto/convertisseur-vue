<template>
    <nav>
      <ul>
        <li>
          <router-link to="/">Accueil</router-link>
        </li>
        <li>
          <router-link to="/credits">Crédits</router-link>
        </li>
      </ul>
    </nav>
  </template>
  
  <script>


  </script>
  
  <style scoped>
  .close {
    display: none;
  }
  .open {
    display: block;
  }
  li, a{
    display: block;
    text-align: center;
    font-size: 1.2em;
    width: 200px;
    margin: 10px auto;
    background: var(--app-dark);
    color: var(--app-light);
    text-decoration: none;
    cursor: pointer
  }
  li:hover, li a:hover {
    color: var(--app-primary);
    box-shadow: 3px 3px 3px var(--app-primary);
  }
  li a.router-link-active {
    background: var(--app-light);
    color: var(--app-dark);
  }
  </style>