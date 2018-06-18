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
                    :rules="emailRules"
                    required
                >
                </v-text-field>
                <v-text-field
                    label="Password"
                    type="password"
                    v-model="password"
                    :rules="passwordRules"
                    required
                >
                </v-text-field>
                <br>
                <div class="red" v-html="error" />
                <br>
                <v-btn
                    :disabled="!valid"
                    dark
                    class="cyan"
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
      error: null,
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
      ],
      passwordRules: [
        v => !!v || 'password is required',
        v => (v && v.length <= 32) || 'password must be less than 32 characters',
        v => (v && v.length >= 8) || 'password must be at least 8 characters in length',
      ],
    }
  },
  methods: {
    async register () {
        if (this.$refs.form.validate()) {
            try {
                const response = await AuthenticationService.register({
                email: this.email,
                password: this.password
            })
            } catch (error) {
                this.error = error.response.data.error
            }
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