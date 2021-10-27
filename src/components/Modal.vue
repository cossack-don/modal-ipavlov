<template>
  <form class="modal" @submit.prevent="sendForm">
    <img src="@/assets/ipavlov_logo.png" alt="logo" class="modal__logo" />
    <h4 class="modal__title">Аутентификация</h4>
<!-- email -->
    <div class="modal__wrapper-email">
      <label for="email-input" class="modal__label-email">Email</label>
      <input
        type="email"
        placeholder="ser@yandex.ru"
        id="email-input"
        class="modal__input-email"
        required
        v-model.trim="formData.email"
      />
    </div>
<!-- passowrd -->
    <div class="modal__wrapper-password">
      <label for="password-input" class="modal__label-password">Пароль</label>

      <div class="icon-oko__svg-icon-password" @click="showPassword">
        <svg
          :class="{ chengeFill: chengeOkocolor }"
          fill="#231F20"
          version="1.1"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 512 512"
          xmlns:xlink="http://www.w3.org/1999/xlink"
          enable-background="new 0 0 512 512"
        >
          <g>
            <g>
              <path
                d="m34,256l26.2,26.2c108,108 283.7,108 391.7,0l26.1-26.2-26.2-26.2c-108-108-283.7-108-391.7,0l-26.1,26.2zm222,126.2c-75.8,0-151.6-28.9-209.3-86.6l-32.9-32.9c-3.7-3.7-3.7-9.7 0-13.5l32.9-32.9c115.4-115.4 303.2-115.4 418.6,0l32.9,32.9c3.7,3.7 3.7,9.7 0,13.5l-32.9,32.9c-57.7,57.7-133.5,86.6-209.3,86.6z"
              />
              <path
                d="m256,183.5c-40,0-72.5,32.5-72.5,72.5s32.5,72.5 72.5,72.5c40,0 72.5-32.5 72.5-72.5s-32.5-72.5-72.5-72.5zm0,164c-50.5,0-91.5-41.1-91.5-91.5 0-50.5 41.1-91.5 91.5-91.5s91.5,41.1 91.5,91.5c0,50.5-41,91.5-91.5,91.5z"
              />
            </g>
          </g>
        </svg>
      </div>

      <input
        :type="password"
        placeholder="Passowrd"
        id="password-input"
        class="modal__input-password"
        required
        v-model.trim="formData.password"
      />
    </div>
<!-- message success form-->
    <div v-if="successfullyFormSend" class="message-form">
      Форма успешно отправлена
    </div>
<!-- btn send form -->
    <button class="modal__button">Отправить</button>
  </form>
</template>

<script>
export default {
data() {
        return {
            // form data
            formData: {
                name: '',
                email: ''
            },
            // hide show passord
            password: 'password',
            // flag for svg icon show-hide
            chengeOkocolor: false,
            // flag for message form
            successfullyFormSend: false
        }
    },

    methods: {
        // показать пароль hide-show
        showPassword() {
            if (this.password === 'password') {
                this.chengeOkocolor = true
                this.password = 'text'
            } else {
                this.chengeOkocolor = false
                this.password = 'password'
            }

        },
        // отправить форму
        async sendForm() {

            try {

                const urlBackEnd = 'https://jsonplaceholder.typicode.com/posts';

                let response = await fetch(urlBackEnd, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json;charset=utf-8'
                    },
                    body: JSON.stringify({
                        ...this.formData
                    })
                });


                let result = await response.json();

                // reset form
                this.formData.email = '',
                this.formData.password = ''
                console.log(result);

                // сообщение форма успешно отправлена
                this.successfullyFormSend = true

                // скрыть сообщение через 2.5 секунды
                setTimeout(() => {
                    this.successfullyFormSend = false
                }, 2500)

            } catch (error) {
                console.log("Проблема с отправкой данных на сервер")
            }


        }
    }
}
</script>

<style>
.modal {
  max-width: 400px;
  height: 400px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  border: 3px solid #f9dd06;
  border-radius: 5px;
  margin: 0 auto;
  background: #ffffff;
}
.modal__logo {
  margin-top: 20px;
  margin-bottom: 20px;
  height: auto;
  width: 95px;
}
.modal__title {
  margin-bottom: 30px;
  font-size: 20px;
}
.modal__button {
  color: #2477d2;
  background-color: #f9dd06;
  width: 120px;
  height: 35px;
  font-weight: bold;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: 0.5s;
  margin-top: 10px;
}
.modal__button:hover {
  transition: 0.5s;
  color: #f9dd06;
  background-color: #2477d2;
}
.modal__wrapper-email {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 50px;
  margin-bottom: 30px;
}
.modal__wrapper-password {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 50px;
  margin-bottom: 15px;
  position: relative;
}
.modal__label-email {
  margin-right: 31px;
}
.modal__label-password {
  margin-right: 15px;
}
.modal__input-email {
  height: 35px;
  width: 100%;
  padding-left: 10px;
  border: 3px solid #f9dd06;
  border-radius: 5px;
}
.modal__input-email:focus,
.modal__input-password:focus {
  border: 3px solid #2477d2;
}
.modal__input-password {
  height: 35px;
  width: 100%;
  padding-left: 10px;
  border: 3px solid #f9dd06;
  border-radius: 5px;
}
.icon-oko__svg-icon-password {
  cursor: pointer;
}
.icon-oko__svg-icon-password svg {
  position: absolute;
  width: 30px;
  height: 30px;
  right: 10px;
  top: 5px;
}
/* добавляем класс при событие hide-show */
.chengeFill {
  fill: red;
}

/*  */

.message-form {
  background: #1670d1;
  color: #ffffff;
  max-width: 250px;
  height: 30px;
  border-radius: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
}
</style>
