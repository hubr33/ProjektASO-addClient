<template>
  <div class="clientWrapper">
    <h2 class="title">Rejestracja nowego klienta</h2>
    <form @submit.prevent="saveClient">
      <label for="name">Imię</label>
      <input type="text" placeholder="..." v-model="name" />
      <label for="surname">Nazwisko</label>
      <input type="text" placeholder="..." v-model="surname" />
      <label for="companyName"
        >Nazwa firmy (jeśli posiada, jeśli nie wpisz - )</label
      >
      <input type="text" placeholder="..." v-model="companyName" />
      <label for="pesel">Pesel</label>
      <input type="text" placeholder="..." v-model="pesel" />
      <label for="nip">NIP (jeśli posiada, jeśli nie wpisz - )</label>
      <input type="text" placeholder="..." v-model="nip" />
      <label for="address">Adres</label>
      <input type="text" placeholder="..." v-model="address" />
      <label for="email">E-mail</label>
      <input type="text" placeholder="..." v-model="email" />
      <label for="phoneNumber">Numer kontaktowy</label>
      <input type="text" placeholder="..." v-model="phoneNumber" />
      <button class="addClient">Dodaj nowego klienta</button>
      <p class="error">Wpisz poprawnie wszystkie dane</p>
    </form>
    <div class="successfulRegister">
      <h2>Pomyślnie dodano nowego klienta!</h2>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    VueAddClient: {},
    name: "",
    surname: "",
    companyName: "",
    pesel: "",
    nip: "",
    address: "",
    email: "",
    phoneNumber: "",
  }),
  methods: {
    closeMessage() {
      const showMessage = document.querySelector(".successfulRegister");
      setTimeout(() => {
        showMessage.classList.remove("active");
        this.coachViewContext.binding.set("value", this.VueAddClient);
        this.coachViewContext.trigger();
        this.name = "";
        this.surname = "";
        this.companyName = "";
        this.pesel = "";
        this.nip = "";
        this.address = "";
        this.email = "";
        this.phoneNumber = "";
      }, 2000);
    },
    saveClient() {
      const allInputs = document.querySelectorAll("form input");
      const showMessage = document.querySelector(".successfulRegister");
      const errorMessage = document.querySelector(".error");
      if (
        this.name !== "" &&
        this.surname !== "" &&
        this.companyName !== "" &&
        this.pesel !== "" &&
        this.nip !== "" &&
        this.address !== "" &&
        this.email !== "" &&
        this.phoneNumber !== ""
      ) {
        this.VueAddClient.name = this.name;
        this.VueAddClient.surname = this.surname;
        this.VueAddClient.companyName = this.companyName;
        this.VueAddClient.pesel = this.pesel;
        this.VueAddClient.nip = this.nip;
        this.VueAddClient.address = this.address;
        this.VueAddClient.email = this.email;
        this.VueAddClient.phoneNumber = this.phoneNumber;
        allInputs.forEach((input) => input.classList.remove("active"));
        showMessage.classList.add("active");
        errorMessage.classList.remove("active");
        this.closeMessage();
      } else {
        errorMessage.classList.add("active");
        allInputs.forEach((input) => {
          if (input.value === "") {
            input.classList.add("active");
          } else {
            input.classList.remove("active");
          }
        });
      }
    },
  },
};
</script>

<style scoped>
@import "./css/app.css";
</style>
