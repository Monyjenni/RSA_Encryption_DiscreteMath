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
          <v-subheader>Original Message</v-subheader>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          <div class="text-fields-container">
            <v-col cols="12">
              <v-text-field
                label="Original Message"
                filled
                rounded
                dense
                v-model="message"
              ></v-text-field>
            </v-col>
            <v-spacer></v-spacer>
          </div>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          <v-btn @click="encryptMessage" color="primary">Encrypt</v-btn>
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
                filled
                rounded
                dense
                v-model="encryptedMessage"
              ></v-text-field>
            </v-col>
            <v-spacer></v-spacer>
          </div>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          <v-btn @click="decryptMessage" color="primary">Decrypt</v-btn>
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
                filled
                rounded
                densee
                v-model="decryptedMessage"
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
export default {
  data: () => ({
    drawer: null,
    message: '', // User input message
    encryptedMessage: '', // Encrypted message result
    decryptedMessage: '', // Decrypted message result
  }),
  methods: {
    encryptMessage() {
      const message = this.message; // Get the user input message
      const encryptedMessage = this.classicalEncrypt(message);

      // Update the encryptedMessage data property
      this.encryptedMessage = encryptedMessage;
    },
    decryptMessage() {
      const encryptedMessage = this.encryptedMessage; // Get the encrypted message
      const decryptedMessage = this.classicalDecrypt(encryptedMessage);

      // Update the decryptedMessage data property
      this.decryptedMessage = decryptedMessage;
    },
    classicalEncrypt(message) {
      // Perform classical encryption algorithm here
      // For demonstration, we'll use a simple Caesar cipher

      const shift = 5; // Shift value for Caesar cipher
      let encryptedMessage = '';

      for (let i = 0; i < message.length; i++) {
        const charCode = message.charCodeAt(i);

        // Encrypt each character by shifting it by the specified value
        if (charCode >= 65 && charCode <= 90) {
          // Uppercase letters
          encryptedMessage += String.fromCharCode(((charCode - 65 + shift) % 26) + 65);
        } else if (charCode >= 97 && charCode <= 122) {
          // Lowercase letters
          encryptedMessage += String.fromCharCode(((charCode - 97 + shift) % 26) + 97);
        } else {
          // Non-alphabetic characters remain unchanged
          encryptedMessage += message[i];
        }
      }

      return encryptedMessage;
    },
    classicalDecrypt(encryptedMessage) {
      // Perform decryption to reverse the encryption algorithm
      // For demonstration, we'll reverse the Caesar cipher

      const shift = 5; // Shift value for Caesar cipher
      let decryptedMessage = '';

      for (let i = 0; i < encryptedMessage.length; i++) {
        const charCode = encryptedMessage.charCodeAt(i);

        // Decrypt each character by shifting it back by the specified value
        if (charCode >= 65 && charCode <= 90) {
          // Uppercase letters
          decryptedMessage += String.fromCharCode(((charCode - 65 - shift + 26) % 26) + 65);
        } else if (charCode >= 97 && charCode <= 122) {
          // Lowercase letters
          decryptedMessage += String.fromCharCode(((charCode - 97 - shift + 26) % 26) + 97);
        } else {
          // Non-alphabetic characters remain unchanged
          decryptedMessage += encryptedMessage[i];
        }
      }

      return decryptedMessage;
    },
  },
};
</script>

<style>
/* Your styles here */
</style>