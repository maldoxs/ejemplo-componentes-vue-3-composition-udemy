<script setup>
   import { ref, computed, onUnmounted, onMounted } from "vue";

   import BlogPost from "./components/BlogPost.vue";
   import PaginatePost from "./components/PaginatePost.vue";
   import Loading from "./components/Loading.vue";

   const posts = ref([]);
   const favorito = ref("");
   const postXpagina = 10;
   const inicio = ref(0);
   const fin = ref(postXpagina); //cantidad de elementos por paginacion
   const loading = ref(true);

   const cambiarFavorito = (title) => {
      favorito.value = title;
   };

   const next = () => {
      inicio.value = inicio.value + postXpagina; //el inicio parte en 10
      fin.value = fin.value + postXpagina; //cada vez q se precione next aumenta de 10 en 10

      console.log(fin.value);
   };

   const previus = () => {
      inicio.value += -postXpagina;
      fin.value += -postXpagina;
   };

   //observar el tamaño del arreglo

   //se carga el html primero y despues hacemos la peticion..onMounted
   //    onMounted(async () => {
   //       //loading.value = true;
   //       try {
   //          const res = await fetch(
   //             "https://jsonplaceholder.typicode.com/posts" //nos traimos la respuesta
   //          );
   //          posts.value = await res.json(); //formateamos el resultado y se lo devolvemos a posts.value
   //       } catch (error) {
   //          console.log(error);
   //       } finally {
   //          setTimeout(() => {
   //             loading.value = false;
   //          }, 2000);
   //       }
   //    });

   //create-------> todavia no se monta nuestro sitio web y ya estamos haciendo la solcitud a la APi
   // fetch("https://jsonplaceholder.typicode.com/posts")
   //     .then((res) => res.json()) //recibe la respuesta y la formatea a JSON
   //     .then((data) => (posts.value = data)) //lo que formatiamos se devuelve en (data)
   //     .catch((e) => console.log(e))
   //     .finally(() => {
   //         setTimeout(() => {
   //             loading.value = false;
   //         }, 2000);
   //     });

   const fetchData = async () => {
      try {
         const res = await fetch(
            "https://jsonplaceholder.typicode.com/posts" //nos traimos la respuesta
         );
         posts.value = await res.json(); //formateamos el resultado y se lo devolvemos a posts.value
      } catch (error) {
         console.log(error);
      } finally {
         setTimeout(() => {
            loading.value = false;
         }, 2000);
      }
   };

   fetchData();

   const maxLength = computed(() => posts.value.length);
</script>

<template>
   <loading v-if="loading" />
   <div class="container" v-else="loading">
      <h1>App</h1>
      <h2>Mis Post Favorito: {{ favorito }}</h2>
      s

      <PaginatePost
         class="mb-2"
         @siguiente="next"
         @anterior="previus"
         :inicio="inicio"
         :fin="fin"
         :totalArreglo="maxLength"
      />

      <BlogPost
         v-for="post in posts.slice(inicio, fin)"
         :key="post.id"
         :id="post.id"
         :title="post.title"
         :body="post.body"
         @cambiarFa="cambiarFavorito"
         class="mb-2"
      />
   </div>
</template>
