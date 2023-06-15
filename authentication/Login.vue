<template>
  <v-card class="mx-auto pa-4 mt-4" width="100%" max-width="500" dir="rtl">
    <div class="text-center mb-4">
      <span style="color: orangered"> ورود به حساب کاربری </span>
    </div>
    <v-form v-model="form" dir="rtl" @submit.prevent="onSubmit">
      <v-text-field
        v-model="userName"
        :rules="[required]"
        class="mb-4"
        clearable
        label="نام کاربری یا شماره همراه"
        type="text"
        dir="ltr"
      ></v-text-field>
      <v-text-field
        v-model="password"
        :rules="[required]"
        class="mb-4"
        clearable
        label="رمز ورود"
        type="password"
        dir="ltr"
      ></v-text-field>
      <v-btn
        :disabled="!form"
        block
        color="success"
        size="large"
        type="submit"
        variant="elevated"
      >
        ورود
      </v-btn>
    </v-form>
    <v-radio-group class="mt-4 text-center" color="success" v-model="radios">
      <template v-slot:label>
        <div>انتخاب <strong>نحوه ورود به حساب کاربری:</strong></div>
      </template>
      <v-radio value="شماره تلفن همراه">
        <template v-slot:label>
          <div><strong class="text-orange">شماره تلفن همراه</strong></div>
        </template>
      </v-radio>
      <v-radio value="نام کاربری">
        <template v-slot:label>
          <div><strong class="text-primary">نام کاربری</strong></div>
        </template>
      </v-radio>
    </v-radio-group>
  </v-card>

  <Alert
    :msg="alertMsg"
    :activate="alertActivator"
    :timeout="alertTimeout"
    :color="alertColor"
  />
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";
import { loginStore } from "@/stores/index";
import axios from "axios";

// Childs
import Alert from "@/components/Alert.vue";

// Variables
const store = loginStore();
const router = useRouter();
const form = ref(false);
const userName = ref(null);
const password = ref(null);
const alertMsg = ref("");
const alertActivator = ref(false);
const alertTimeout = ref(5000);
const alertColor = ref("error");
const radios = ref("شماره تلفن همراه");

// Functions
function onSubmit() {
  const apiUrl = "/api/account/api-token-auth/";
  let param;
  if (radios.value === "شماره تلفن همراه") {
    const validPhoneNumber = "+98" + userName.value.slice(1);
    param = {
      username: validPhoneNumber,
      password: password.value,
    };
  } else {
    param = {
      username: userName.value,
      password: password.value,
    };
  }

  axios
    .post(apiUrl, param)
    .then((response) => {
      store.login(response.data.token);
      router.push("/dashboard");
    })
    .catch((error) => {
      console.log("error from api", error);
      alertActivator.value = true;
      alertMsg.value = "رمز ورود یا نام کاربری اشتباه است";
    })
    .finally(() => {
      alertActivator.value = false;
    });
}

function required(v) {
  return !!v || "این فیلد الزامی است";
}
</script>
