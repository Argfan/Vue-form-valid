<template>

  <div>
    <form v-if="!registrationPassed" class="sign-in pt-5" @submit.prevent="checkForm">    
      <div class="form-group">
        <label for="login">Логин:</label>
        <input 
          type="text" 
          class="form-control" 
          :class="$v.form.login.$error ? 'is-invalid' : ''"
          id="login" 
          v-model.trim="form.login">
        <div v-if="$v.form.login.$dirty && !$v.form.login.required" class="invalid-feedback">
          Обязательное поле
        </div>
        <div v-if="$v.form.login.$dirty && !$v.form.login.minLength" class="invalid-feedback">
          Здесь должно быть больше 5-и символов
        </div>
      </div>

      <div class="form-group">
        <label for="email">Почта:</label>
        <input type="email" class="form-control" id="email" :class="$v.form.email.$error ? 'is-invalid' : ''" v-model.trim="form.email">
        <div v-if="$v.form.email.$dirty && !$v.form.email.required" class="invalid-feedback">
          Обязательное поле
        </div>
        <div v-if="$v.form.email.$dirty && !$v.form.email.minLength" class="invalid-feedback">
          Email неккоректный
        </div>
      </div>    

      <div class="form-group">
        <label for="password">Пароль:</label>
        <input type="password" class="form-control" id="password" :class="$v.form.password.$error ? 'is-invalid' : ''" v-model.trim="form.password">
        <div v-if="$v.form.login.$dirty && !$v.form.password.required" class="invalid-feedback">
          Обязательное поле
        </div>
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
        <label for="theme">Любимые темы:</label>
        <select name="country" id="theme" class="form-control" :class="$v.form.favoiriteThemes.$error ? 'is-invalid' : ''" v-model="form.favoiriteThemes" multiple>
          <option 
            v-for="(theme, index) in themes"
            :key="index"
            :value="theme.value"
          >
            {{theme.label}}
          </option>
        </select>
        <div v-if="$v.form.favoiriteThemes.$dirty && !$v.form.favoiriteThemes.maxCount" class="invalid-feedback">
          Не больше 3
        </div>
      </div>
      <div class="custom-control custom-checkbox">
        <input type="checkbox" class="custom-control-input" id="r1"  :class="$v.form.agreeWithRules.$error ? 'is-invalid' : ''" v-model="form.agreeWithRules">
        <label class="custom-control-label" for="r1">Правила</label>
        <div v-if="$v.form.agreeWithRules.$dirty  && !$v.form.agreeWithRules.mustBeTrue" class="invalid-feedback">
          Правила прочти
        </div>
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
    <div v-else>
      <h2 class="my-5 text-center">
        {{ `${ form.login }, вы успешно зарегистрировались` }}
      </h2>
    </div>
    
  </div>
  
  
</template>

<script>

import { validationMixin } from 'vuelidate'
import { required, minLength, email } from 'vuelidate/lib/validators'

export default {
  name: "UserForm",
  mixins: [validationMixin],
  data(){
    return{
      registrationPassed: false,
      form:{
        login: '',
        email: '',
        password: '',
        country: 'Russia',
        favoiriteThemes: ['IT'],
        agreeWithRules: false,
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
        },
        {
          label: 'Йога',
          value: 'Yoga'
        }
      ]
    }    
  },
  validations: {
    form: {
      login: { required, minLength: minLength(5)},
      email: { required, email},
      password: { required },
      favoiriteThemes: {
        maxCount(value) {
          return value.length <= 3
        }
      },
      agreeWithRules: {
        mustBeTrue(value) {
          return value
        }
      }
    }
    

  },
  methods: {
    checkForm(){
      this.$v.form.$touch()
      if (!this.$v.form.$error){
        this.registrationPassed = true
      }
    }
  }
  // this.$v.form.$touch(){

  // }

}
</script>
