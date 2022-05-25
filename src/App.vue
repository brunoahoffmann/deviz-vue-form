<template>
  <v-app>
    <v-main>
      <v-container fill-height>
        <DevizForm />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import DevizForm from './components/DevizForm';

export default {
  name: 'App',

  components: {
    DevizForm
  },

  data: () => ({
    //
  }),
};
</script>
