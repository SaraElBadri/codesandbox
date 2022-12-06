<template>
  <div>{{ saludarUsuario() }}</div>

  <div>
    {{ `${items[0].name.toUpperCase()} hola!` }}
  </div>

  <div>{{ aMayusculas(items[0]) }}</div>

  <p>{{ username }}</p>

  <input type="text" v-model="username" placeholder="Set your username" />
  <p>{{ yourPasswordIs() }}</p>

  <input type="password" v-model="password" placeholder="password" />

  <div>
    <article v-for="(item, index) of topItems" :key="item.uuid" class="flex">
      <div>{{ index }}</div>
      <div>{{ aMayusculas(item) }}</div>
      <img :src="item.image" :alt="item.name" width="96" />
    </article>
  </div>

  <div v-if="!limitReached">Añade mínimo 3 artículos</div>

  <div v-else-if="items.length < 5">
    Añade 5 articulos mas para envio gratuio
  </div>

  <button v-else>
    Confirmar compra
    {{ numberOfItems }}
  </button>
</template>


<script>
import ITEMS from "./items.json";
export default {
  data() {
    return {
      items: ITEMS,
      username: null,
      errorMessage: "please set your username",
      password: null,
      mostrar: false,
    };
  },

  computed: {
    topItems() {
      return this.items.slice(0, 5);
    },
    numberOfItems() {
      return this.topItems.length;
    },
    limitReached() {
      return this.items.length > 3;
    },
  },

  methods: {
    aMayusculas(item) {
      return item.name.toUpperCase();
    },
    saludarUsuario() {
      if (this.username) {
        const english = this.items[0].name.toUpperCase();
        const spanish = this.items[1].name.toLowerCase();

        return english + " " + spanish + " " + this.username;
      } else {
        return `${this.errorMessage} ${this.numberOfItems}`;
      }
    },
    yourPasswordIs() {
      const pass = "Te he pillado la contraseña!";
      return this.password + " " + pass;
    },
    mostrarTres(top) {
      const tres = this.items.slice(0, top);

      return tres;
    },
  },
};
</script>

<style>
.flex {
  display: flex;
  justify-content: space-around;
}
</style>
