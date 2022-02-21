<template>
    <v-app>
        <v-main>
            <div class="text-center">
                <router-link width="20px" to="/" class="grey lighten-3 black--text">Form</router-link> | 
                <router-link to="/rapidoc" class="grey lighten-3 black--text">API Documentation</router-link>
            </div>
            <router-view />
        </v-main>
    </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
