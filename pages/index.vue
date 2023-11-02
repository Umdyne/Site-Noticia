<template>
    <v-app class="bg-grey-darken-4">
      <v-app-bar class="bg-grey">
        <v-app-bar-title class="text-center">
          NOTICIAS
        </v-app-bar-title>
      </v-app-bar>
      <v-main>
        <v-container class="bg-grey-darken-1">
          <ul>
            <template v-for="dado in dados.articles" >
              <v-card class="bg-grey-darken-3 ma-5">
                <v-card-title>{{ dado.title }}</v-card-title>
                <v-card-subtitle>{{ dado.description }}</v-card-subtitle>
                <v-card-text>{{ dado.content }}</v-card-text>
                <v-card-actions class="border border-white">
                  <v-btn :href="dado.url" target="_blank">
                    Ir para a notícia
                  </v-btn>
                </v-card-actions>
              </v-card>
            </template>
          </ul>
        </v-container>
      </v-main>
    </v-app>
  </template>
  
  <script setup>

  
  const dados = ref({ articles: [] });
  
  async function recebe() {  
    const response = await fetch(`https://newsapi.org/v2/everything?domains=wsj.com&apiKey=b991ab4e7d1c4a1a87468a17fcc49f82`);
    const valores = await response.json();
    dados.value = valores;
  }
  onMounted(async () => {
    await recebe();
    console.log(dados.articles);
  });
  </script>