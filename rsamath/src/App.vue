<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app>
    </v-navigation-drawer>

    <v-app-bar app color="primary">
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>RSA Cryptosystem</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <v-row>
        <v-col cols="4">
          <v-subheader>Public Key</v-subheader>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          <div class="text-fields-container">
            <v-col cols="12">
              <v-text-field
                label="First Index Number"
                filled
                rounded
                dense
                v-model="publicKey.e"
                type="number"
              ></v-text-field>
            </v-col>
            <v-spacer></v-spacer>
            <v-col cols="12">
              <v-text-field
                label="Second Index Number"
                filled
                rounded
                dense
                v-model="publicKey.n"
                type="number"
              ></v-text-field>
            </v-col>
          </div>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          <v-subheader>Private Key</v-subheader>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          <div class="text-fields-container">
            <v-col cols="12">
              <v-text-field
                label="First Index Number"
                filled
                rounded
                dense
                v-model="privateKey.d"
                type="number"
              ></v-text-field>
            </v-col>
            <v-spacer></v-spacer>
            <v-col cols="12">
              <v-text-field
                label="Second Index Number"
                filled
                rounded
                dense
                v-model="privateKey.n"
                type="number"
              ></v-text-field>
            </v-col>
          </div>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          <v-subheader>Original Message</v-subheader>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          <div class="text-fields-container">
            <v-col cols="12">
              <v-text-field
                label="Output"
                outlined
                dense
                v-model="message"
                type="number"
              ></v-text-field>
            </v-col>
            <v-spacer></v-spacer>
          </div>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          <v-subheader>Encrypted message</v-subheader>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          <div class="text-fields-container">
            <v-col cols="12">
              <v-text-field
                label="Encrypted Output"
                outlined
                dense
                v-model="encryptedMessage"
                type="number"
              ></v-text-field>
            </v-col>
            <v-spacer></v-spacer>
          </div>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          <v-subheader>Decrypted message</v-subheader>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          <div class="text-fields-container">
            <v-col cols="12">
              <v-text-field
                label="Decrypted Output"
                outlined
                dense
                v-model="decryptedMessage"
                type="number"
              ></v-text-field>
            </v-col>
            <v-spacer></v-spacer>
          </div>
        </v-col>
      </v-row>
    </v-main>
  </v-app>
</template>

<script>
// Function to calculate phi(n) for a given number n
function phi(n) {
  // Your implementation here
}

// Function to calculate gcd(a, b) using the Euclidean algorithm
function gcd(a, b) {
  // Your implementation here
}

// Function to calculate a^b mod m using modular exponentiation
function modpow(a, b, m) {
  // Your implementation here
}

// Function to generate a random primitive root modulo n
function generatePrimitiveRoot(n) {
  // Your implementation here
}

export default {
  data: () => ({
    drawer: null,
    publicKey: { e: 0, n: 0 },
    privateKey: { d: 0, n: 0 },
    message: 0,
    encryptedMessage: 0,
    decryptedMessage: 0,
  }),
  methods: {
    encryptMessage() {
      const m = parseInt(this.message);
      this.encryptedMessage = modpow(m, this.publicKey.e, this.publicKey.n);
    },
    decryptMessage() {
      const c = parseInt(this.encryptedMessage);
      this.decryptedMessage = modpow(c, this.privateKey.d, this.privateKey.n);
    },
    // Add the phi, gcd, modpow, and generatePrimitiveRoot functions here
    phi,
    gcd,
    modpow,
    generatePrimitiveRoot,
  },
};
</script>

<style>
/* Your styles here */
</style>
