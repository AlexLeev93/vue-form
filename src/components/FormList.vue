<template>
    <div>
        <form @submit.prevent="submit">
        <fieldset>
            <legend>Атрибуты формы</legend>

            <div class="row">
                <div class="row__item">
                    <input class="customInput" placeholder="Имя*" type="text"
                        v-model="$v.userName.$model"
                        :class="{invalid: ($v.userName.$dirty && !$v.userName.required) }">
                    <small v-if="$v.userName.$dirty && !$v.userName.required"
                        :class="{'helper_text':$v.userName.$dirty && !$v.userName.required}" >Поле обязательное</small>
                </div>
                <div class="row__item">
                    <input class="customInput" placeholder="Фамилия*" type="text"
                        v-model="$v.surname.$model"
                        :class="{invalid: ($v.surname.$dirty && !$v.surname.required) }">
                    <small v-if="$v.surname.$dirty && !$v.surname.required"
                        :class="{'helper_text':$v.surname.$dirty && !$v.surname.required}" >Поле обязательное</small>
                </div>

                <input v-model="middleName" class="customInput" placeholder="Отчество" type="text">
            </div>
            
            <div class="row">
                <div class="row__item">
                    <input class="customInput" 
                        v-model="$v.birthday.$model" 
                        placeholder="Дата рождения*" 
                        type="text" 
                        onfocus="(this.type='date')" onblur="(this.type='text')"
                        :class="{invalid: ($v.birthday.$dirty && !$v.birthday.required) }">
                    <small v-if="$v.birthday.$dirty && !$v.birthday.required"
                        :class="{'helper_text':$v.birthday.$dirty && !$v.birthday.required}" >Поле обязательное</small>
                </div>
                
                <select v-model="gender">
                    <option value="">Пол</option>
                    <option value="male">Мужской</option>
                    <option value="female">Женский</option>
                </select>

                <div class="row__item">
                    <input class="customInput" 
                       v-model="$v.phoneNumber.$model" 
                       placeholder="Номер телефона*" 
                       type="tel"
                       :class="{invalid: ($v.phoneNumber.$dirty && !$v.phoneNumber.required) || ($v.phoneNumber.$dirty && !$v.phoneNumber.phoneValid)}">
                    <small v-if="$v.phoneNumber.$dirty && !$v.phoneNumber.required"
                       :class="{'helper_text':$v.phoneNumber.$dirty && !$v.phoneNumber.required}" >Поле обязательное</small>
                    <small v-else-if="$v.phoneNumber.$dirty && !$v.phoneNumber.phoneValid"
                       :class="{'helper_text':$v.phoneNumber.$dirty && !$v.phoneNumber.phoneValid}" >Номер не корректный</small>
                </div>

                
            </div>
            
                <div class="row">
                    <div class="row_multiselect">
                        <div class="full_width">
                            <div class="multiselect_wrapper">
                                <div class="dropdown" @click="showDropdown">
                                <div class="overselect" />
                                <select :class="{invalid: ($v.selectedGroup.$dirty && !$v.selectedGroup.required) }">
                                    <option value="">Группа клиентов*</option>
                                </select>
                                </div>
                                <div class="multiselect" v-if="show">
                                    <ul>
                                        <li v-for="(option, index) in options" :key="index">
                                            <input type="checkbox" :id="index" :value="option.value" v-model="$v.selectedGroup.$model">
                                            <div>
                                                <label :for="index">{{ option.text }}</label>
                                            </div>
                                        </li>
                                    </ul>
                                </div>
                            </div>
                <small v-if="$v.selectedGroup.$dirty && !$v.selectedGroup.required"
                       :class="{'helper_text':$v.selectedGroup.$dirty && !$v.selectedGroup.required}">Поле обязательное</small>
                </div>

            </div>

                <select v-model="selectedDoctor">
                    <option value="">Лечащий врач</option>
                    <option value="Иванов">Иванов</option>
                    <option value="Захаров">Захаров</option>
                    <option value="Чернышева">Чернышева</option>
                </select>
            </div>

            

            <div style="padding: 25px">
                <input type="checkbox" v-model="sendSmS">
                    <span>Не отправлять СМС</span>
            </div>

        </fieldset>

        <fieldset>
            <legend>Адрес</legend>

            <div class="row">
                <input v-model="index" class="customInput" placeholder="Индекс" type="text" >

                <input v-model="country" class="customInput" placeholder="Страна" type="text" >

                <input v-model="region" class="customInput" placeholder="Область" type="text" >
            </div>

            <div class="row">
                <div class="row__item">
                    <input class="customInput" placeholder="Город*" type="text"
                        v-model="$v.city.$model"
                        :class="{invalid: ($v.city.$dirty && !$v.city.required) }">
                    <small v-if="$v.city.$dirty && !$v.city.required"
                        :class="{'helper_text':$v.city.$dirty && !$v.city.required}" >Поле обязательное</small>
                </div>

                <input v-model="street" class="customInput" placeholder="Улица" type="text" >

                <input v-model="house" class="customInput" placeholder="Дом" type="text" >
            </div>

        </fieldset>

        <fieldset>
            <legend>Паспорт</legend>

            <div class="row">
                <div class="row__item">
                    <select v-model="$v.docType.$model"
                            :class="{invalid: ($v.docType.$dirty && !$v.docType.required) }">
                        <option value="">Тип документа*</option>
                        <option value="Паспорт">Паспорт</option>
                        <option value="Свидетельство о рождении">Свидетельство о рождении</option>
                        <option value="Вод. удостоверение">Вод. удостоверение</option>
                    </select>
                    <small v-if="$v.docType.$dirty && !$v.docType.required"
                        :class="{'helper_text':$v.docType.$dirty && !$v.docType.required}" >Поле обязательное</small>
                </div>

                <input v-model="ser" class="customInput" placeholder="Серия" type="text" >

                <input v-model="number" class="customInput" placeholder="Номер" type="text" >
            </div>
            
            <div class="row">
                <input v-model="issuedBy" class="customInput" placeholder="Кем выдан" type="text" >

                <div class="row__item">
                    <input class="customInput" 
                        v-model="$v.dateOfIssue.$model" 
                        placeholder="Дата выдачи*" 
                        type="text" 
                        onfocus="(this.type='date')" onblur="(this.type='text')"
                        :class="{invalid: ($v.dateOfIssue.$dirty && !$v.dateOfIssue.required) }">
                    <small v-if="$v.dateOfIssue.$dirty && !$v.dateOfIssue.required"
                        :class="{'helper_text':$v.dateOfIssue.$dirty && !$v.dateOfIssue.required}" >Поле обязательное</small>
                </div>
            </div>
            
        </fieldset>
        <button type="submit" v-on:click="submit()">Создать</button>

        <div v-if="isModalOpen" class="fixed-overlay fixed-overlay__modal">
            <div class="modal">
                <div class="modal_container"> 
                    <p v-if="submitStatus === 'OK'">Клиент успешно создан!</p>
                    <p v-if="submitStatus === 'ERROR'">Заполните все <br> обязательные поля!</p>
                    <p v-if="submitStatus === 'PENDING'">Отправка...</p>
                    
                    <button v-if="submitStatus !== 'PENDING'" class="close" v-on:click="closeModal">ок</button>
                </div>
            </div>
        </div>

        </form>



    </div>
</template>

<script>
import {required, minLength} from 'vuelidate/lib/validators';
const isPhone = (value) => /^(\+7|7|8)?[\s\-]?\(?[489][0-9]{2}\)?[\s\-]?[0-9]{3}[\s\-]?[0-9]{2}[\s\-]?[0-9]{2}$/.test(value);

export default {
    data(){
        return {
            userName: '',
            surname: '',
            middleName: '',
            birthday: '',
            gender: '',
            phoneNumber: '',
            selectedDoctor: '',
            docType: '',
            show: false,
            selectedGroup: [],
            options: [
                {
                    text: 'VIP ',
                    value: 1
                },
                {
                    text: 'Проблемные ',
                    value: 2
                },
                {
                    text: 'ОМС ',
                    value: 3
                }
            ],
            sendSmS: false,
            city: '',
            dateOfIssue: '',
            index: '',
            country: '',
            region: '',
            street: '',
            house: '',
            ser: '',
            number: '',
            issuedBy: '',
            submitStatus: '',
            isModalOpen: false,
        }
    },
    validations: {
        userName: {
            required
        },
        surname: {
            required
        },
        birthday: {
            required
        },
        phoneNumber: {
            required,
            phoneValid:isPhone
        },
        selectedGroup: {
            required
        },
        city: {
            required
        },
        docType: {
            required
        },
        dateOfIssue: {
            required
        }
    },
    methods: {
        showDropdown() {
            this.show = !this.show
        },
        openModal(){
            this.isModalOpen = true;
        },
        closeModal(){
            this.isModalOpen = false
        },
        submit() {
            console.log('submit!')
            this.$v.$touch()
        if (this.$v.$invalid) {
            this.submitStatus = 'ERROR'
            this.$v.$touch()
            this.openModal()
            return
        } else {
        this.submitStatus = 'PENDING'
        this.openModal()
        setTimeout(() => {
          this.submitStatus = 'OK'
        }, 1000)
      }
    }
    }
}
</script>

<style lang="scss" scoped>

$color: #1abc9c;



@media (min-width: 1024px){

fieldset{
    margin-bottom: 10px;
    padding: 26px 160px;
} 

.row {
    display: flex;
    justify-content: space-between;
}

select{
    width: 200px;
}

.customInput {
    width: 200px;
}

}

@media (min-width: 768px) and (max-width: 1024px) {
  
  fieldset{
    margin-bottom: 10px;
} 

.row {
    display: flex;
    justify-content: space-between;
}

select{
    width: 200px;
}

.customInput {
    width: 200px;
}
  
}

@media (min-width: 320px) and (max-width: 480px) {

.row{
    display: flex;
    align-items: center;
    flex-direction: column;
    }

.row__item {
    width: 100%;
    display: flex;
    align-items: center;
    flex-direction: column;
}    

.customInput {
    width: 70%;
    }

.full_width{
    width: 100%;
}

.row_multiselect{
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
}

select {
    width: 70%;
}

.multiselect_wrapper {
    width: 100%;
    } 
}

fieldset{
    margin-bottom: 10px;
}

.row{
      display: flex;
      align-items: center;
}



.row_multiselect {
    display: flex;
}

.dropdown { 
    width: 100%;
    align-items: center;
    display: flex;
    justify-content: center;  
    position: relative; 
    cursor: pointer;
}

.multiselect_wrapper {
    align-items: center;
    display: flex;
}

.multiselect {
  position: relative;
  width: 100%;
  ul {
    list-style: none;
    padding-left: 20px;
    li {
        display: flex;
    }
  }
}

.overselect {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
}

select {
  margin: 40px 25px 0 25px;
  display: block;
  font-size: 12px;
  cursor: pointer;
  border-radius: 0;
  border: none;
  border-bottom: solid 1px $color;
  color: $color;
  padding: 10px 0;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
}

select:focus{
    outline: none;
}

.customInput {
  margin: 40px 25px 0 25px;
  display: block;
  border: none;
  padding: 12px 0 6px 0;
  border-bottom: solid 1px $color;
  background-size: 100%;
  background-repeat: no-repeat;
  color: $color;
  &::-webkit-input-placeholder{
      color: $color;
  }
  &:focus {
    box-shadow: none;
    outline: none;
    background-position: 0 0;
    &::-webkit-input-placeholder {
      color: $color;
      font-size: 12px;
      transform: translateY(-14px);
      visibility: visible !important;
    }
  }
}

.invalid {
    border-bottom: solid 1px red;
    color: red;
    &::-webkit-input-placeholder{
      color: red;
    }
    &:focus {
        &::-webkit-input-placeholder {
            color: red;
        }
    }
}

.helper_text {
    color: red;
    font-size: 11px;
}

button {
  border: none;
  background: $color;
  cursor: pointer;
  border-radius: 3px;
  padding: 6px;
  width: 200px;
  color: white;
  margin-left: 25px;
  box-shadow: 0 3px 6px 0 rgba(0,0,0,0.2);
  &:hover { 
    transform: translateY(-3px);
    box-shadow: 0 6px 6px 0 rgba(0,0,0,0.2);
  }
}

.fixed-overlay {
    position: fixed;
    overflow: auto;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,0.5);
}

.modal {
    position: absolute;
    left: 50%;
    top: 50%;
    margin-left: -100px;
    margin-top: -75px;
    // width: 50%;
}

.modal_container {
    background-color: #fff;
    display: flex;
    flex-direction: column;
    align-items: center;
    border-radius: 15px;
    p {
        margin: 20px;
    }
}

.close {
  color: #fff;
  float: right;
  font-size: 12px;
  font-weight: bold;
  margin: 0 0 15px 0;
  width: 50%;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}

</style>