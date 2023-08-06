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
        <!-- <v-row>
          <v-col cols="4">
            <v-subheader>Encrypted message</v-subheader>
          </v-col>
        </v-row> -->
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
          <v-col cols="8">
            <div class="text-fields-container">
              <v-col cols="6">
                <v-text-field
                  label="Decrypted Output"
                  filled
                  rounded
                  densee
                  v-model="decryptedMessage"
                ></v-text-field>
              </v-col>
            </div>
          </v-col>
        </v-row>
      </v-row>
      <v-row>
        <v-col cols="4">
          <v-subheader>Converted to Numbers</v-subheader>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          <div class="text-fields-container">
            <v-col cols="12">
              <v-text-field
                label="Numbers Output"
                filled
                rounded
                dense
                v-model="numbersOutput"
              ></v-text-field>
            </v-col>
            <v-spacer></v-spacer>
          </div>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="4">
          <v-btn @click="encryptMessage" color="primary">Encrypt</v-btn>
          <v-btn @click="decryptMessage" class="d-button" color="primary">Decrypt</v-btn>
          <v-btn @click="clearMessage" class="clear-button" color="red">Clear</v-btn>
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
    numbersOutput: '', // Numbers representation of the original message
  }),
  methods: {
    convertToNumbers(message) {
      const k = 21; // New shift value for Caesar cipher
      const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"; // All capital letters
      const encryptedIndexes = [];

      for (let i = 0; i < message.length; i++) {
        const char = message[i];
        const index = letters.indexOf(char.toUpperCase());

        if (index !== -1) {
          const encryptedIndex = (index + k) % 26;
          encryptedIndexes.push(encryptedIndex);
        }
      }

      return encryptedIndexes;
    },
    encryptMessage() {
      const message = this.message; // Get the user input message
      const encryptedMessage = this.classicalEncrypt(message);

      // Update the encryptedMessage data property
      this.encryptedMessage = encryptedMessage;

      // Convert the original message to numbers and update the numbersOutput data property
      const encryptedIndexes = this.convertToNumbers(message);
      this.numbersOutput = encryptedIndexes.join(', ');
    },
    
    decryptMessage() {
      const encryptedMessage = this.encryptedMessage; // Get the encrypted message
      const decryptedMessage = this.classicalDecrypt(encryptedMessage);

      // Update the decryptedMessage data property
      this.decryptedMessage = decryptedMessage;

      // Convert the decrypted message to numbers and update the numbersOutput data property
      const numbers = this.convertToNumbers(decryptedMessage);
      this.numbersOutput = numbers.join(', ');
    },
    classicalEncrypt(message) {
      const k = 21; // New shift value for Caesar cipher
      const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"; // All capital letters
      const encryptedMessage = [];

      for (let i = 0; i < message.length; i++) {
        const char = message[i];
        const index = letters.indexOf(char.toUpperCase());

        if (index !== -1) {
          const encryptedIndex = (index + k) % 26;
          console.log(encryptedIndex)
          const encryptedChar = letters[encryptedIndex];
          encryptedMessage.push(encryptedChar);
        } else {
          // For non-alphabetic characters, keep them as they are
          encryptedMessage.push(char);
        }
      }

      return encryptedMessage.join('');
    },

    classicalDecrypt(encryptedMessage) {
      const k = 21; // Shift value for decryption (inverse of encryption)
      const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"; // All capital letters
      const decryptedMessage = [];

      for (let i = 0; i < encryptedMessage.length; i++) {
        const char = encryptedMessage[i];
        const index = letters.indexOf(char.toUpperCase());

        if (index !== -1) {
          const decryptedIndex = (index - k + 26) % 26; // Fix the decryption formula
          console.log(decryptedIndex )
          const decryptedChar = letters[decryptedIndex];
          decryptedMessage.push(decryptedChar);
        } else {
          // For non-alphabetic characters, keep them as they are
          decryptedMessage.push(char);
        }
      }

      return decryptedMessage.join('');
    },

    clearMessage() {
      // Clear the input and output fields
      this.message = '';
      this.decryptedMessage = '';
      this.numbersOutput = '';
      this.encryptedMessage = '';
    },
  },
};
</script>
<style>
/* Add some margin to the clear-button class */
.clear-button {
  margin-left: 16px; /* Adjust the value as needed for desired spacing */
}
.d-button {
  margin-left: 16px
}
/* Your other styles here */
</style>