<template>
  <form class="sign-in pt-5">    
    <div class="form-group">
      <label for="login">Логин:</label>
      <input type="text" class="form-control" id="login" v-model.trim="form.login">
    </div>

    <div class="form-group">
      <label for="email">Почта:</label>
      <input type="email" class="form-control" id="email" v-model.trim="form.email">
    </div>

    <div class="form-group">
      <label for="password">Пароль:</label>
      <input type="password" class="form-control" id="password" v-model.trim="form.password">
    </div>

    <div class="form-group">
      <label for="country">Страна:</label>
      <select name="country" id="country" class="form-control" v-model="form.country">
        <option 
          v-for="(country, index) in countrys"
          :key="index"
          :value="country.value"
        >
          {{country.label}}
        </option>
      </select>
    </div>

    <div class="form-group">
      <label for="country">Любимые темы:</label>
      <select name="country" id="country" class="form-control" v-model="form.favoiriteThemes" multiple>
        <option 
          v-for="(theme, index) in themes"
          :key="index"
          :value="theme.value"
        >
          {{theme.label}}
        </option>
      </select>
    </div>

    <div class="custom-control custom-checkbox">
      <input type="checkbox" value="1" class="custom-control-input" id="notification" v-model="form.agreeWithSendEmail">
      <label class="custom-control-label" for="notification">Уведомлять меня о новых курсах</label>
    </div>
    <div class="custom-control custom-checkbox mb-3">
      <input type="checkbox" value="2" class="custom-control-input" id="notification2" v-model="form.agreeWithSendEmail">
      <label class="custom-control-label" for="notification2">Уведомлять меня о новых курсах2</label>
    </div>

    <div class="flex mb-3">
      <div class="form-check mr-3">
        <input class="form-check-input" type="radio" value="male" name="exampleRadios" id="male" v-model="form.gendere">
        <label class="form-check-label" for="male">
          Мужчина
        </label>
      </div>
      <div class="form-check">
        <input class="form-check-input" type="radio" value="female" name="exampleRadios" id="female" v-model="form.gendere">
        <label class="form-check-label" for="female">
          Женщина
        </label>
      </div>
    </div>
    <button type="submit" class="btn btn-primary">Сохранить</button>
  </form>
</template>

<script>

import { validationMixin } from 'vuelidate'

export default {
  name: "UserForm",
  mixins: [validationMixin],
  data(){
    return{
      form:{
        login: '',
        email: '',
        password: '',
        country: 'Russia',
        favoiriteThemes: ['IT'],
        agreeWithSendEmail: [],
        gendere: 'male',
      },
      
      countrys: [
        {
          label: 'Россия',  
          value: 'Russia'
        },
        {
          label: 'Украина',
          value: 'Ukraine'
        },
        {
          label: 'США',
          value: 'USA'
        }
      ],
      themes: [
         {
          label: 'Технологии',
          value: 'IT'
        },
        {
          label: 'Языки',
          value: 'languages'
        },
        {
          label: 'Математика',
          value: 'mathematics'
        }
      ]

    }
    
  },
  validations: {

  }

}
</script>
