<template>
  <v-layout align-center justify-center>
    <v-flex xs12 sm8 md4>
      <v-card class="elevation-12">
        <v-toolbar>
            <v-toolbar-title>Register Page!</v-toolbar-title>
        </v-toolbar>

        <v-card-text justify-center>
            <v-form v-model="valid" ref="form" lazy-validation>
                <v-text-field
                    label="Email"
                    v-model="email"
                    required
                >
                </v-text-field>
                <v-text-field
                    label="Password"
                    type="password"
                    v-model="password"
                    required
                >
                </v-text-field>
                
                <v-btn
                    :disabled="!valid"
                    @click="register"
                > 
                    register
                </v-btn>

                <v-btn @click="clear">clear</v-btn>
           
            </v-form>
        </v-card-text>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'

export default {
  data () {
    return {
      valid: true,
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    async register () {
      try {
        const response = await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
      } catch (error) {
        this.error = error.response.data.error
      }
    },
    clear () {
        this.$refs.form.reset()
    }
  }
}
</script>

<style scoped>
</style>