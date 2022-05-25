<template>
  <v-card 
    outlined
    color="transparent"
    width="100%"
  >
    <v-row>
      <v-col cols="12" lg="6">
          <v-img
              :src="require('../assets/logo.svg')"
              width="300"
              class="mx-auto"
          ></v-img>
      </v-col>
      <v-col cols="12" lg="6">
        <v-form
          ref="form"
          v-model="valid"
          lazy-validation
        >
          <v-text-field
            v-model="name"
            :counter="100"
            :rules="nameRules"
            label="Name"
            required
          ></v-text-field>

          <v-text-field
            v-model="email"
            :rules="emailRules"
            label="E-mail"
            required
          ></v-text-field>

          <v-text-field
            type="password"
            v-model="password"
            :rules="passwordRules"
            label="Password"
            required
          ></v-text-field>

          <DevizPassword :password="password" />

          <v-checkbox
            v-model="checkbox"
            :rules="[v => !!v || 'You must agree to continue!']"
            label="Do you agree?"
            required
          ></v-checkbox>

          <v-btn
            :disabled="!valid"
            color="success"
            class="mr-4"
            @click="validate"
            >
            Submit form
          </v-btn>

          <v-btn
            class="mr-4"
            @click="reset"
            >
            Reset Form
          </v-btn>
        </v-form>
      </v-col>
    </v-row>        
  </v-card>
</template>

<script>
  import DevizPassword from "./DevizPassword.vue"

  export default {
    name: "DevizForm",
    components: { DevizPassword },
    data: () => ({
        valid: true,
        name: "",
        nameRules: [
            v => !!v || "Name is required",
            v => (v && v.length <= 100) || "Name must be less than 10 characters",
        ],
        email: "",
        emailRules: [
            v => !!v || "E-mail is required",
            v => /.+@.+\..+/.test(v) || "E-mail must be valid",
        ],
        password: "",
        passwordRules: [
            v => !!v || "Password is required",
        ],
        checkbox: false,
        power: 30
    }),
    methods: {
        validate() {
            this.$refs.form.validate();
        },
        reset() {
            this.$refs.form.reset();
            this.password = ''
        },
        resetValidation() {
            this.$refs.form.resetValidation();
        },
    }
}
</script>