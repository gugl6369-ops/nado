# nado
```css
@mixin leaner-border{
  position: relative;
  justify-content: center;
  align-items: center;

  &::before{
    content: '';
    width: 100%;
    height: calc(100% + 2px);
    position: absolute;
    border-radius: 38px;
    background: linear-gradient(90deg, transparent, #424242, rgba(66, 66, 66, 0.51), transparent);
    z-index: -1;
  }
}
```

# ТОЛИНО ГОВНО!!!
```vue
<script setup lang="ts">
import {AppButton, AppInput} from "@/shared";
import {reactive, ref} from "vue";
import {SocialIcon} from "@/features";
import { authFormStyles} from "../../shared/ui/auth.variants.ts";
const { form, formTitle, formInputs, formDescriptionContainer, formDescription, descriptionLine, iconContainer, buttonContainer, textLink } = authFormStyles()
import {registerSchema} from "@/features/auth/register/lib/validation.ts";
import {useForm} from "vee-validate";


const socialIcons = ref(["vk", "telegram", "google", "yandex"])


const { defineField, handleSubmit, errors } = useForm({
  validationSchema: registerSchema,
})

const [username, usernameAttrs] = defineField("username")
const [email, emailAttrs] = defineField("email")
const [password, passwordAttrs] = defineField("password")
const [confirmPassword, confirmPasswordAttrs] = defineField("confirmPassword")

</script>
<template>
  <form :class="form()" class="linear-border">
    <h2 :class="formTitle()">Регистрация</h2>
    <div :class="formInputs()">
      <app-input v-model="username" v-bind="usernameAttrs" :error="errors.username" type="text" placeholder="Введите имя пользователя" />
      <app-input v-model="email" v-bind="emailAttrs" type="email" :error="errors.email" placeholder="Введите почту" />
      <app-input v-model="password" v-bind="passwordAttrs" :error="errors.password" type="password" placeholder="Введите пароль" />
      <app-input v-model="confirmPassword" v-bind="confirmPasswordAttrs" :error="errors.confirmPassword" type="password" placeholder="Повторите пароль" />
    </div>
    <div :class="formDescriptionContainer()">
      <div :class="formDescription()">
        <span :class="descriptionLine()"></span>
        <h3 class="text-gray-100 text-sm whitespace-nowrap">Зарегистрироваться с помощью</h3>
        <span :class="descriptionLine()"></span>
      </div>
      <div :class="iconContainer()">
        <template
          v-for="item in socialIcons"
          :key="item"
        >
          <social-icon :name="item" :size="30" />
        </template>
      </div>
    </div>
    <div :class="buttonContainer()">
      <app-button variant="primaryOrange" type="submit" fontWeight="Black" padding="xl1" size="md" rounded="lg" class="w-full font-second">Зарегистрироваться</app-button>
      <p :class="textLink()">Уже есть аккаунт? <router-link :to="{ name: 'auth-login' }" class="font-semibold">Войти</router-link></p>
    </div>
  </form>
</template>
<style lang="scss" scoped>
.linear-border{
  @include linear-border;
}
</style>
```

