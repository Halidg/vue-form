<template>
  <form class="form-content" @submit.prevent="submitForm">
    <div class="user-info">
        <h2>Атрибуты Формы</h2>
      <div class="user-info__block">
        <label for="secondName">Фамилия</label>
        <input id="secondName" class="user-info__input" v-model="secondName" 
        type="text"
        :class="v$.secondName.$error==true
              ? 'invalid'
              : null"
        >
       <small  class="invalid-text" v-for="error of v$.secondName.$errors"
          :key="error.$uid"
          >{{error.$message}}
       </small> 
      </div>

      <div class="user-info__block">
        <label for="name">Имя</label>
        <input id="name" class="user-info__input" 
        v-model="name" 
        type="text"
        :class="v$.name.$error==true
              ? 'invalid'
              : null">
       <small  class="invalid-text" v-for="error of v$.name.$errors"
          :key="error.$uid"
          >{{error.$message}}
       </small>       
      </div>          
      
      <div class="user-info__block">
        <label for="patronymic">Отчество</label>
        <input id="patronymic" class="user-info__input" type="text">
      </div>     

      <div class="user-info__block">
        <label for="dateOfBirth">Дата рождения</label>
        <input id="dateOfBirth"  class="user-info__input" v-model="dateOfBirth" 
        placeholder="Дата Рождения" 
        type="date"
        :class="v$.dateOfBirth.$error==true
              ? 'invalid'
              : null"> 
        <small  class="invalid-text" v-for="error of v$.dateOfBirth.$errors"
          :key="error.$uid"
          >{{error.$message}}
       </small>
      </div>

      <div class="user-info__block">
         <label for="">Номер телефона</label> 
        <input  class="user-info__input" 
        v-model="telephone" 
        placeholder="+7" 
        type="number"
         :class="v$.telephone.$error==true
              ? 'invalid'
              : null"> 
       <small  class="invalid-text" 
         v-if="v$.telephone.$error"
       >
       Минимальное количество символов ({{v$.telephone.minLength.$params.min}})
       </small>
        <small  class="invalid-text" 
         v-if="isLimit"
       >
       Превышено количество символов ({{v$.telephone.maxLength.$params.max}})
       </small>
      </div>          
      
      <div class="user-info__block">
      <label for="select">Выберите пол</label>   
        <select id="select" class="user-info__select">
          <option value="man">Мужской</option>
          <option value="women">Женский</option>        
        </select>  
      </div>

      <!-- Если зажать crtl или левый SHIFT и кликнуть можно выделить сразу несколько -->
      <div class="user-info__block">
      <label for="multiple-select">Выберите группу клиентов</label>   
        <select multiple size="2"
        id="multiple-select" 
        v-model="clients" 
        class="user-info__select"
        :class="v$.clients.$error==true
              ? 'invalid'
              : null">
          <option class="user-info__option" value="vip">VIP</option>
          <option class="user-info__option" value="problematic">Проблемные</option>
          <option class="user-info__option" value="OMS">ОМС</option>        
        </select>  
         <small  class="invalid-text"  v-for="error of v$.clients.$errors"
          :key="error.$uid"
          >{{error.$message}}
         </small>
      </div>

      <div class="user-info__block">
      <label for="doctors-select">Выберите лечащего врача</label>   
        <select id="doctors-select" class="user-info__select">
          <option>Иванов</option>
          <option>Захаров</option>
          <option>Чернышева</option>        
        </select> 
      </div> 

      <div class="user-info__alignment">
        <input class="user-info__checkbox" id="checkbox" type="checkbox">
        <label for="checkbox">Не отправлять сообщение</label>
      </div> 

    </div>

    <div class="user-adress">
      
      <div class="user-adress__block">
        <label for="index">Индекс</label>
        <input id="index" class="user-info__input"  type="text">
      </div>

      <div class="user-adress__block">
        <label for="country">Страна</label>
         <input class="user-info__input" type="text" list="country">
            <datalist id="country">
              <option value="Россия"></option>
              <option value="Англия"></option>
              <option value="Италия"></option>
            </datalist>
      </div>

       <div class="user-adress__block">
         <label for="city">Город</label>
        <input
        id="city" 
        class="user-info__input" 
        v-model="city"
        type="text"
         :class="v$.city.$error==true
              ? 'invalid'
              : null">
         <small  class="invalid-text"  v-for="error of v$.city.$errors"
          :key="error.$uid"
          >{{error.$message}}
        </small>
      </div>

      <div class="user-adress__block">
        <label for="region">Область</label>
        <input id="region" class="user-info__input"  type="text">
      </div>

      <div class="user-adress__block">
        <label for="street">Улица</label>
        <input id="street" class="user-info__input"  type="text">
      </div>

       <div class="user-adress__block">
        <label for="house">Дом</label>
        <input id="house" class="user-info__input"  type="text">
      </div>

    </div>

    <div class="user-passport">

      <div class="user-passport__block">
       <label for="passport-select">Тип документа</label>
         <select class="user-passport__select"
          v-model="documentType"  
          id="passport-select"
          :class="v$.documentType.$error==true
              ? 'invalid'
              : null">
           <option>Паспорт</option>
           <option>Свидетельство о рождении</option>
           <option>Вод. удостоверение</option> 
         </select>
         <small  class="invalid-text"  v-for="error of v$.documentType.$errors"
          :key="error.$uid"
          >{{error.$message}}</small>   
       </div>

       <div class="user-passport__block">
         <label for="passport series">Серия</label>
         <input id="passport series" class="user-passport__input" type="text"> 
       </div>

       <div class="user-passport__block">
         <label for="number">Номер</label>
         <input id="number" class="user-passport__input"  type="text"> 
       </div> 

       <div class="user-passport__block">
         <label  for="issued by">Кем выдан</label>
         <input id="issued by" class="user-passport__input"  type="text"> 
       </div> 

       <div class="user-passport__block">
         <label for="dateOfIssue">Дата выдачи</label>
         <input id="dateOfIssue" class="user-passport__input" 
         v-model="dateOfIssue" 
         type="date"
         :class="v$.dateOfIssue.$error==true
              ? 'invalid'
              : null">
         <small  class="invalid-text"  v-for="error of v$.dateOfIssue.$errors"
          :key="error.$uid"
          >{{error.$message}}</small>
       </div>  

    </div>
    <button class="form-content__button">Отправить форму</button>
  </form>  
</template>

<script>
import useValidate from '@vuelidate/core'
import { required, helpers, minLength, maxLength, numeric} from '@vuelidate/validators'

export default {
  data() {
    return {
      v$: useValidate(),
      name: '',
      secondName: '',
      dateOfBirth: '',
      telephone: 7,
      clients: [],
      city: '',
      documentType: '',
      dateOfIssue: null 
    }  
  },
  validations() {
    return {
      name: {required:helpers.withMessage(`Введите имя`, required), $autoDirty: true},
      secondName: {required:helpers.withMessage(`Введите фамилию`, required), $autoDirty: true},
      dateOfBirth: {required:helpers.withMessage(`Укажите дату рождения`, required), $autoDirty: true},
      telephone: {minLength:minLength(11), maxLength:maxLength(11), required, numeric, $autoDirty: true},
      clients: {required:helpers.withMessage(`Выберите группу`, required),  $autoDirty: true},
      city: {required:helpers.withMessage(`Укажите город`, required),  $autoDirty: true},
      documentType: {required:helpers.withMessage(`Укажите тип документа`, required),  $autoDirty: true},
      dateOfIssue: {required:helpers.withMessage(`Укажите дату выдачи`, required),  $autoDirty: true}   
    }
  },
  methods: {
    submitForm() {
      this.v$.$touch()
      if (!this.v$.$error) {
        alert('Форма успешно создана')
      }
    }
  },
  computed: {
    isLimit() {
      if (String(this.telephone).length > 11) {
        return true
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.form-content {
  max-width: 700px;
  background-color: #141625;
  color: #fff;
  padding: 56px;
  &__button {
    border: none;
    color: white;
    padding: 10px 15px;
    margin-top: 15px;
    border-radius: 15px;
    background-color: #0d26e0;
    &:hover {
      cursor: pointer;
      background-color: #596bf3;
      transition: 1s;
    }  
  }
}

.user-info {
  display: flex;
  gap: 16px;
  flex-direction: column;
  &__block {
    display: flex;
    flex-direction: column;
    margin-bottom: 24px;
    flex: 1;  
  }
  &__alignment {
    display: flex;
    align-items: center;     
  }
  &__input {
    width: 100%;
    background-color: #1e2139;
    color: #fff;
    border-radius: 4px;
    margin-top: 5px;
    padding: 12px 12px;
    border: none;
    outline: none;
  }
  &__select {
    width: 100%;
    background-color: #1e2139;
    color: #fff;
    border-radius: 4px;
    padding: 8px 2px;
    border: none;
    margin-top: 15px;  
  }
  &__option {
    font-size: 15px;
    padding-top: 5px;
  }
  &__checkbox {
    margin-right: 5px; 
  }
}

.user-adress {
  display: flex;
  flex-direction: column;
  margin-top: 20px;
  &__block {
    display: flex;
    flex-direction: column;
    margin-bottom: 24px;
    flex: 1;
  }      
}

.user-passport {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-top: 25px;
  &__block {
    display: flex;
    flex-direction: column;
    flex: 1;
  }
  &__select {
    width: 100%;
    background-color: #1e2139;
    color: #fff;
    border-radius: 4px;
    padding: 8px 2px;
    border: none;
    margin-top: 15px;
  }
  &__input {
    width: 50%;
    background-color: #1e2139;
    color: #fff;
    border-radius: 4px;
    margin-top: 5px;
    padding: 12px 12px;
    border: none;
    outline: none;       
  }
}

.invalid {
    border: 1px solid red;  
  }
.invalid-text {
  color: red;
  padding-top: 10px;  
}

::-webkit-calendar-picker-indicator {
    filter: invert(1);
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0; 
}
</style>