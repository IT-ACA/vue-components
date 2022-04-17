<template>
  <v-dialog v-model="dialog" persistent max-width="500">
    <v-card>
      <v-card-title class="card-title-bar">
        User Password Reset
        <!-- {{ dialogTitle }}  -->
      </v-card-title>
      <v-divider style="margin-bottom: 20px;"></v-divider>
      <v-card-text>
        <h4>Create or reset a password for  {{ user.firstname }} {{ user.lastname }}</h4>
        <br>
        <!-- {{ dialogText }} -->
        <!-- {{ passwordsMatch }} -->
        <p class="text-justify">
          Passwords are stored using one-way encryption. 
          Once a password is saved it cannot cannot be retrieved in plain text. 
          If the password is lost a new one must be created here.
        </p>
      </v-card-text>   
      <!--<v-card-text> {{ user }} </v-card-text>-->
      <v-card-text>
        <!-- <v-form class="px-1">
          <v-text-field v-model="user.password" label="New Password" prepend-icon=""></v-text-field>
        </v-form> -->

          <!-- <v-layout row wrap>
              <v-flex xs12 md12>
                <v-text-field
                  class="input-group--focused mr-6 ml-6"
                  name="firstname"
                  prepend-icon="mdi-account"
                  v-model="user.firstname"
                  label="First Name"
                  value="Input text"
                ></v-text-field>
              </v-flex>
          </v-layout> -->

          <!-- <v-layout row wrap>
              <v-flex xs12 md12>
                <v-text-field
                  class="input-group--focused mr-6 ml-6"
                  name="lastname"
                  prepend-icon="mdi-account"
                  v-model="user.firstname"
                  label="Last Name"
                  value="Input text"
                ></v-text-field>
              </v-flex>
          </v-layout> -->

          <v-layout row wrap>
              <v-flex xs12 md12>
                <v-text-field
                  class="input-group--focused mr-6 ml-6"
                  name="password"
                  type="password"
                  v-model="user.password"
                  label="New Password"
                  value="Input text"
                  :rules="inputRules"
                  prepend-icon="mdi-pencil"
                ></v-text-field>
              </v-flex>
          </v-layout>
          <v-layout row wrap>
              <v-flex xs12 md12>
                <v-text-field
                  class="input-group--focused mr-6 ml-6"
                  name="retype"
                  type="password"
                  v-model="user.confirmPassword"
                  label="Repeat Password"
                  value="Input text"
                  :rules="inputRules"
                  prepend-icon="mdi-pencil"
                ></v-text-field>
              </v-flex>
              <v-flex xs12 md12 v-if="!passwordsMatch">
                <v-text
                  class="input-group--focused mr-6 ml-6"
                >Passwords do not match</v-text>
              </v-flex>
              
          </v-layout>
      </v-card-text>

      <v-card-text v-show="confirmPasswordFailMsg !== ''"
        style="border-top: 1px solid red;
          border-bottom: 1px solid red;
          height: 40px;
          line-height: 40px;
          background-color: #fe5442;
          margin: 10px 0px 10px"> 
        <span style="color: white;font-size: 16px;">  
          {{ confirmPasswordFailMsg }}
        </span>
      </v-card-text>

      <v-card-actions>
        <v-btn
          class="blue--text darken-1"
          text="text"
          @click.native="checkPass(user)"
          >Confirm</v-btn
        >
        <v-btn
          class="orange--text darken-1"
          text="text"
          @click.native="cancelSetPasswordDialog(user)"
          >Cancel</v-btn
        >
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script lang="ts">
import { Component, Prop } from "vue-property-decorator";
import Vue from "vue";

@Component
export default class ConfirmDialog extends Vue {
  @Prop() dialogText!: string;
  @Prop() dialogTitle!: string;
  @Prop() dialog!: string;
  @Prop() user!: object;
  @Prop() passwordsMatch!: boolean;
  confirmPasswordFailMsg = ''
  mini = false;
  isRootComponent = true;

  drawer = true;
  fixed = false;
  data() {
    return {
      inputRules: [
        v => v.length > 3 || 'Minimun length is 3 characters'
      ]
    }
  }
  created() {}
  mounted() {}
  public cancelSetPasswordDialog(user) {
    console.log('User cancel : ', user)
    // user.password = ''
    // user.confirmPassword = ''
    this.confirmPasswordFailMsg = ''
    this.$emit('onCancel', user)
  }
  
  public checkPass(user): void {
    // alert(`CheckPass Func ${JSON.stringify(user)}`) 
    if(user.password === '' || user.confirmPassword === '') {
      console.log('A field is empty.')
      user.password = ''
      user.confirmPassword = ''
      this.confirmPasswordFailMsg = 'Please fill both fields before confirming.'
      return
    }

    if(user.password !== user.confirmPassword) {
      console.log('Passwords do not match. Please try again.')
      user.password = ''
      user.confirmPassword = ''
      // Add function with setTimeout to close alert after few seconds
      this.confirmPasswordFailMsg = 'Passwords do not match. Please try again.'
      return
    } else {
      this.confirmPasswordFailMsg = ''
      this.$emit('onConfirm', { user: user })
     }
  }
}
</script>

<style scoped>
  .card-title-bar {
    background-color: #eff2f5;
    color: #697070;
  }
</style>
