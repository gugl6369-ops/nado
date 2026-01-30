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
##Input

```
<script setup lang="ts">
import { vMaska } from 'maska/vue'
import {AppIcon, inputVariants, type InputVariants} from '@/shared'
import {computed, ref} from "vue";

interface Props {
  error?: string
  disabled?: boolean
  type?: string
  placeholder?: string
  mask?: string
}

const props = withDefaults(defineProps<Props>(), {
  type: 'text',
  disabled: false,
  size: 'md',
  error: undefined,
  placeholder: '',
  mask: '',
})

const check = ref<boolean>(false)
const model = defineModel<string>()

const checkPassword = () =>{
  check.value = !check.value
}

const checkType = computed<string>(() =>{
  if (check.value && props.type === 'password') return 'text'
  if ( !check.value && props.type === 'password') return 'password'
  return props.type
});
</script>


<template>
  <div class="flex flex-col transition duration-500 ">
    <transition
      name="errorShow"
      class="text-primary-orange pl-5 text-xs transition duration-500 pb-2"
    >
      <p v-if="error">
        {{error}}
      </p>
    </transition>
    <label
      :class="inputVariants({ error: !!error, disabled })"
    >
      <input
        v-maska
        :data-maska="mask"
        :type="checkType"
        :value="modelValue"
        :placeholder="placeholder"
        :disabled="disabled"
        :error="error"
        v-model="model"
        required
      >
      <template v-if="type === 'password'">
        <template v-if="check === true">
          <app-icon
            name="password-open"
            class="cursor-pointer hover:opacity-70 transition-opacity duration-300"
            @click="checkPassword"
          />
        </template>
        <template v-else>
          <app-icon
            name="password-lock"
            class="cursor-pointer hover:opacity-70 transition-opacity duration-300"
            @click="checkPassword"
          />
        </template>
      </template>
    </label>
  </div>
</template>

<style lang="scss" scoped>
.errorShow-enter-active{
  max-height: 15px;
  transition: .2s ease-in-out;
  transform: translateY(20px);
}
.errorShow-enter-from {
  max-height: 0;
  padding-bottom: 0;
  opacity: 0;
  transform: translateY(10px);
}
.errorShow-leave-active{
  max-height: 15px;
  padding-bottom: 8px;
  transition: 0.5s ease-in-out;
}
.errorShow-leave-to {
  max-height: 0;
  padding-bottom: 0;
  opacity: 0;
  transform: translateY(10px);
  transition: .3s;
}
input{
  width: 100%;
  outline: none;
}
label{
  justify-content: center;
  align-items: center;

  &:has(input:focus){
    background-color: #212121;
  }
}

</style>

```
