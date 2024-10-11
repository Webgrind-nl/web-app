<template>
  <div class="wrapper">
    <div class="contact-form-container">
      <h2 class="form-title">Neem Contact Met Ons Op</h2>
      <form class="contact-form">
        <div class="form-group">
          <label for="name">Naam</label>
          <input
            type="text"
            id="name"
            name="name"
            class="form-input"
            placeholder="Vul je naam in"
          />
        </div>
        <div class="form-group">
          <label for="email">E-mail</label>
          <input
            type="email"
            id="email"
            name="email"
            class="form-input"
            placeholder="Vul je e-mailadres in"
          />
        </div>
        <div class="form-group">
          <label for="message">Bericht</label>
          <textarea
            id="message"
            name="message"
            class="form-input"
            rows="5"
            placeholder="Typ hier je bericht..."
          ></textarea>
        </div>
        <button type="submit" class="form-button">Verstuur Bericht</button>
      </form>
    </div>
  </div>
</template>

<script setup lang="ts"></script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  width: 100vw;
}

.contact-form-container {
  width: 600px;
  max-width: 90%;
  margin: 50px auto;
  background: linear-gradient(135deg, #181a35, #2a2c5c);
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.5);
  animation: fadeInUp 1s ease-out;
}

.contact-form-container {
  margin-bottom: 100px !important;
}

.form-title {
  text-align: center;
  color: linear-gradient(135deg, #6a0dad, #d16ba5, #45aaf2);
  font-size: 28px;
  margin-bottom: 20px;
  background: linear-gradient(135deg, #835aff, #5ec8f7);
  -webkit-background-clip: text;
  color: transparent;
}

.contact-form {
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 20px;
  position: relative;
}

.form-group label {
  display: block;
  margin-bottom: 8px;
  font-size: 16px;
  color: #fff;
}

.form-input {
  width: 100%;
  padding: 15px;
  border: 1px solid #444;
  border-radius: 8px;
  background-color: rgba(255, 255, 255, 0.1);
  color: #fff;
  outline: none;
  font-size: 16px;
  transition: all 0.3s ease-in-out;
}

.form-input::placeholder {
  color: #888;
}

.form-input:focus {
  border: 1px solid #5ec8f7;
  box-shadow: 0 0 10px rgba(94, 200, 247, 0.5);
}

.form-button {
  padding: 15px;
  border: none;
  border-radius: 25px;
  cursor: pointer;
  font-size: 18px;
  color: #fff;
  background: linear-gradient(45deg, #835aff, #5ec8f7);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.form-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 20px rgba(131, 90, 255, 0.3);
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media screen and (max-width: 600px) {
  .contact-form-container {
    padding: 20px;
  }

  .form-title {
    font-size: 20px;
  }

  .form-input,
  .form-button {
    font-size: 14px;
  }
}
</style>
