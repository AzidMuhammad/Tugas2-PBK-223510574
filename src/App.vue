<template>
  <div id="app">
    <div class="container" :style="{ backgroundColor: backgroundColor, color: textColor }">
      <h1 :style="{ color: textColor }">Form Saran</h1>
      <form @submit.prevent="submitForm">
        <div class="form-group">
          <label :style="{ color: textColor }" for="name">Nama:</label>
          <input type="text" id="name" :class="{ 'error': !formData.name }" :style="{ border: formData.name ? '1px solid #ccc' : '1px solid red' }" v-model="formData.name" required>
          <span class="error-message" v-if="!formData.name">*Nama harus diisi!</span>
        </div>
        <div class="form-group">
          <label :style="{ color: textColor }" for="npm">NPM:</label>
          <input type="number" id="npm" v-model.number="formData.npm" required>
        </div>
        <div class="form-group radio-group">
          <label :style="{ color: textColor }">Jenis Kelamin:</label>
          <div class="radio-option">
            <input type="radio" id="male" value="Laki-laki" v-model="formData.gender">
            <label for="male" :style="{ color: textColor }">Laki-laki</label>
          </div>
          <div class="radio-option">
            <input type="radio" id="female" value="Perempuan" v-model="formData.gender">
            <label for="female" :style="{ color: textColor }">Perempuan</label>
          </div>
        </div>
        <div class="form-group">
          <label :style="{ color: textColor }" for="message">Pesan:</label>
          <textarea id="message" v-model="formData.message" @input="updateDisplay" required></textarea>
        </div>
        <div class="modal" v-if="showPopup" @click="closePopup">
          <div class="modal-content" @click.stop>
            <span class="close" @click="closePopup">&times;</span>
            <h2>Text yang dimasukkan</h2>
            <table>
              <tr>
                <td></td>
              </tr>
              <tr>
                <td>{{ formData.message }}</td>
              </tr>
            </table>
          </div>
        </div>                    
        <div class="form-group">
          <label for="color" :style="{ color: textColor }">Ubah Warna Latar Belakang:</label>
          <input type="color" id="color" v-model="backgroundColor">
        </div>
        <div class="form-group">
          <label for="textColor" :style="{ color: textColor }">Ubah Warna Teks:</label>
          <input type="color" id="textColor" v-model="textColor">
        </div>
        <button type="submit" @submit.prevent="submitForm">Kirim</button>
      </form>
    </div>

    <div class="modal" v-if="showModal" @click="closeModal">
      <div class="modal-content" @click.stop>
        <span class="close" @click="closeModal">&times;</span>
        <h2>Hasil Formulir</h2>
        <table>
          <tr>
            <td><strong>Nama:</strong></td>
            <td>{{ formData.name }}</td>
          </tr>
          <tr>
            <td><strong>NPM:</strong></td>
            <td>{{ formData.npm }}</td>
          </tr>
          <tr>
            <td><strong>Jenis Kelamin:</strong></td>
            <td>{{ formData.gender }}</td>
          </tr>
          <tr>
            <td><strong>Pesan:</strong></td>
            <td>{{ formData.message }}</td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        name: '',
        email: '',
        phone: '',
        npm: '',
        gender: '',
        message: ''
      },
      backgroundColor: '#ffffff',
      textColor: '#000000',
      showModal: false,
      showPopup: false
    }
  },
  methods: {
    submitForm() {
      this.showModal = true;
    },
    closePopup() {
    this.showPopup = false;
    },
    closeModal() {
      this.showModal = false;
      this.resetForm();
    },
    resetForm() {
      for (let key in this.formData) {
        this.formData[key] = '';
      }
    },
    updateDisplay() {
      this.showPopup = true;
    }
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: 'Courier New', Courier, monospace;
  font-weight: normal;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: whitesmoke;
}

.container {
  text-align: center;
  background-color: #fff;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  width: 400px;
  height: 560px;
}

h1 {
  color: #000;
  margin-bottom: 20px;
  font-size: 26px;
}

h2 {
  text-align: center;
  font-size: 26px;
}

p {
  font-size: 20px;
}

.form-group {
  margin-bottom: 15px;
  text-align: left;
}

label {
  display: block;
  margin-bottom: 7px;
  color: #000;
  font-weight: bolder;
}

input[type="text"],
input[type="email"],
input[type="number"],
input[type="tel"],
textarea {
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-sizing: border-box;
}

button {
  position: fixed;
  left: 50%;
  bottom: 50px;
  transform: translateX(-50%);
  padding: 10px 20px;
  background-color: brown;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.5s ease;
  font-family: 'Courier New', Courier, monospace;
}

button:hover {
  background-color: rgb(78, 20, 20);
}

textarea {
  height: 70px;
}

.radio-group {
  display: flex;
  flex-direction: row;
}

.radio-option {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
  margin-left: 15px;
}

.radio-option input[type="radio"] {
  margin-right: 10px;
  margin-bottom: 10px;
}

.error {
  color: red;
  border-radius: 5px;
}

.error-message {
  color: red;
  font-size: 12px;
  margin-top: 5px;
}

.modal {
  display: block;
  position: fixed;
  z-index: 9999;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  font-family: 'Courier New', Courier, monospace;
  background-color: rgba(0, 0, 0, 0.4);
}

.modal-content {
  background-color: #fefefe;
  font-family: 'Courier New', Courier, monospace;
  margin: 15% auto;
  padding: 20px;
  border: 1px solid #888;
  border-radius: 8px;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2), 0 6px 20px 0 rgba(0,0,0,0.19);
  max-width: 600px;
}

table {
  width: 100%;
}

td {
  padding: 8px;
  border-bottom: 1px solid #ddd;
}

.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}

@media only screen and (max-width: 600px) {
  .container {
    width: 60%;
    height: 500px;
  }

  h1 {
    font-size: 20px;
  }

  input[type="text"],
  input[type="email"],
  input[type="number"],
  input[type="tel"],
  textarea {
    width: calc(100% - 20px);
  }
}

@media only screen and (max-width: 400px) {
  .container {
    padding: 10px;
  }

  input[type="text"],
  input[type="email"],
  input[type="number"],
  input[type="tel"],
  textarea {
    padding: 6px;
  }

  button {
    padding: 8px 16px;
  }
}

</style>
