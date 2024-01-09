<template>
  <v-card class="mx-auto mt-10" max-width="400">
    <v-card-title class="headline">Registration Form</v-card-title>
    <v-card-text>
      <v-form>
        <v-text-field label="First Name" v-model="user.firstName" required></v-text-field>
        <v-text-field label="Last Name" v-model="user.lastName" required></v-text-field>
        <v-text-field label="Email" v-model="user.email" required></v-text-field>
        <v-select label="State" v-model="user.state" :items="states" @change="onStateSelect" required></v-select>
        <v-select v-if="isAffiliationDropdownVisible" label="Affiliation" v-model="user.affiliation"
          :items="selectedAffiliations" required>
        </v-select>
      </v-form>
    </v-card-text>
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn color="primary" @click="registerUser">Register</v-btn>
    </v-card-actions>
  </v-card>
  <v-dialog v-model="dialog" persistent max-width="500px">
    <v-card>
      <v-card-title class="headline">Confirm Registration</v-card-title>
      <v-card-text>
        <p>First Name: {{ user.firstName }}</p>
        <p>Last Name: {{ user.lastName }}</p>
        <p>Email: {{ user.email }}</p>
        <p>State: {{ user.state }}</p>
        <p>Affiliation: {{ user.affiliation }}</p>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="green darken-1" text @click="confirmRegistration">Confirm</v-btn>
        <v-btn color="red darken-1" text @click="dialog = false">Cancel</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data() {
    return {
      user: {
        firstName: '',
        lastName: '',
        email: '',
        state: '',
        affiliation: '',
      },
      dialog: false,
      states: ['NY', 'CA', 'FL'],
      affiliations: {
        NY: ['L100', 'L102', 'L105'],
        CA: ['C31', 'C1', 'C3'],
        FL: ['R-Retiree 1', 'R-Retiree 2']
      },
      selectedAffiliations: [],
      isAffiliationDropdownVisible: false
    };
  },
  methods: {
    onStateSelect() {
      this.selectedAffiliations = this.getAffiliationsForState(this.user.state);
      this.isAffiliationDropdownVisible = true;
    },
    getAffiliationsForState(state) {
      return this.affiliations[state] || [];
    },
    registerUser() {
      this.dialog = true;
    },
    confirmRegistration() {
      console.log("User Data:", this.user);
      this.dialog = false;
      // Additional logic to actually register the user
    }
  }
};
</script>

