<template>
  <v-app>
    <v-main>
      <v-container fill-height fluid>
        <Form />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Form from './components/Form';

export default {
  name: 'App',

  components: {
    Form
  },

  data: () => ({
    //
  }),
};
</script>
