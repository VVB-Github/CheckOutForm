<script setup>

import { ref, computed } from 'vue'

const firstName = ref('')
const lastName = ref('')
const userName = ref('')
const email = ref('')
const address = ref('')
const country = ref('')
const zip = ref('')

const form_data = ref({
    firstName: '',
    lastName: '',
    userName: '',
    email: '',
    address: '',
    country: '',
    zip: '',
})

// чекаем имя - если оно пустое или короче 3-х, то false, иначе - true
const NameCheck = computed(() => {
    if (firstName.value.trim() === '') {
        return false;
    }
    else if (firstName.value.trim().length < 3) {
        return false;
    }
    else {
        return true;
    }
});

// чекаем фамилию
const lastNameCheck = computed(() => {
    if (lastName.value.trim() === '') {
        return false;
    }
    else if (lastName.value.trim().length < 3) {
        return false;
    }
    else {
        return true;
    }
});

// чекаем имя юзера
const userNameCheck = computed(() => {
    if (userName.value.trim() === '') {
        return false;
    }
    else if (userName.value.trim().length < 3) {
        return false;
    }
    else {
        return true;
    }
});

// проверка емэйла на соответствие емэйловскому паттерну
const EmailCheck = computed(() => {
    /* проверяем email на соответствие формату адреса электр. почты 
    Эта регулярная выражение используется для проверки строк, которые должны
    соответствовать формату адреса электронной почты. Давайте разберём её по частям:
        ^ — начало строки.
        [a-zA-Z0-9._-]+ — 
            один или более символов из набора: букв латинского алфавита в верхнем
            или нижнем регистре (a-zA-Z), цифр (0-9), точки (.), подчёркивания (_),
            или дефиса (-). Эта часть соответствует пользовательской части адреса
            электронной почты (то, что идёт до @).
        @ — символ собачки, разделяющий локальную часть адреса и домен.
        [a-zA-Z0-9.-]+ — 
            один или более символов из набора: букв латинского алфавита в верхнем
            или нижнем регистре, цифр, точки или дефиса. Эта часть соответствует
            доменному имени (то, что идёт после @ и до точки перед верхнеуровневым
            доменом).
        \. — литеральная точка, разделяющая доменное имя и верхнеуровневый домен (TLD).
        [a-zA-Z]{2,4} —
            от двух до четырёх букв латинского алфавита в верхнем или нижнем регистре.
            Эта часть соответствует верхнеуровневому домену (например, .com, .org, .info).
        $ — конец строки.
    */
    const regex = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/;
    /* return regex.test(email); выполняет проверку строки email на соответствие
    регулярному выражению, заданному в переменной regex. Метод test регулярного
    выражения возвращает true, если строка соответствует паттерну регулярного выражения,
    и false, если не соответствует. */
    return regex.test(email.value);
});

// чекаем адрес
const addressCheck = computed(() => {
    if (address.value.trim() === '') {
        return false;
    }
    else if (address.value.trim().length < 10) {
        return false;
    }
    else {
        return true;
    }
});

const validateForm = () => {
    if (NameCheck.value && lastNameCheck.value && userNameCheck.value && EmailCheck.value && addressCheck.value) {
        console.log('y')

        form_data.value.firstName = firstName.value
        form_data.value.lastName = lastName.value
        form_data.value.userName = userName.value
        form_data.value.email = email.value
        form_data.value.address = address.value
        form_data.value.country = country.value
        form_data.value.zip = zip.value

        console.log(form_data.value)

        firstName.value = ''
        lastName.value = ''
        userName.value = ''
        email.value = ''
        address.value = ''
        country.value = ''
        zip.value = ''
        return true;
    }
    else {
        console.log('n')
        return false;
    }
}

</script>

<template>
    <div class="form-group">
        <h1>Validation Form</h1>
        <div class="input_name">
            <label for="first_name">First Name</label>
            <input id="first_name" v-model="firstName" />
            <span class="error_msg" v-if="!NameCheck">Добавте имя</span>
        </div>
        <div class="input_name">
            <label for="last_name">Last Name</label>
            <input id="last_name" v-model="lastName" />
            <span class="error_msg" v-if="!lastNameCheck">Добавте фамилию</span>
        </div>
        <div class="input_name">
            <label for="userName">User Name</label>
            <input id="userName" v-model="userName" />
            <span class="error_msg" v-if="!userNameCheck">Добавте имя пользователя</span>
        </div>
        <div class="input_name">
            <label for="email">Email</label>
            <input id="email" v-model="email" />
            <span class="error_msg" v-if="!EmailCheck">Добавте валидный емэйл</span>
        </div>
        <div class="input_name">
            <label for="address">Address</label>
            <input id="address" v-model="address" />
            <span class="error_msg" v-if="!addressCheck">Добавте адрес, больше 10 симв.</span>
        </div>
        <div class="input_name">
            <label for="select_country">Country</label>
            <select class="select_country" id="select_country" v-model="country">
                <option value="Afghanistan">Afghanistan</option>
                <option value="Albania">Albania</option>
                <option value="Algeria">Algeria</option>
                <option value="American Samoa">American Samoa</option>
                <option value="Andorra">Andorra</option>
                <option value="Angola">Angola</option>
                <option value="Anguilla">Anguilla</option>
                <option value="Antartica">Antarctica</option>
                <option value="Antigua and Barbuda">Antigua and Barbuda</option>
                <option value="Argentina">Argentina</option>
                <option value="Armenia">Armenia</option>
                <option value="Aruba">Aruba</option>
                <option value="Australia">Australia</option>
                <option value="Austria">Austria</option>
                <option value="Azerbaijan">Azerbaijan</option>
                <option value="Bahamas">Bahamas</option>
                <option value="Bahrain">Bahrain</option>
                <option value="Bangladesh">Bangladesh</option>
                <option value="Barbados">Barbados</option>
                <option value="Belarus">Belarus</option>
                <option value="Belgium">Belgium</option>
                <option value="Belize">Belize</option>
                <option value="Benin">Benin</option>
                <option value="Bermuda">Bermuda</option>
                <option value="Bhutan">Bhutan</option>
                <option value="Bolivia">Bolivia</option>
                <option value="Bosnia and Herzegowina">Bosnia and Herzegowina</option>
                <option value="Botswana">Botswana</option>
                <option value="Bouvet Island">Bouvet Island</option>
                <option value="Brazil">Brazil</option>
                <option value="British Indian Ocean Territory">British Indian Ocean Territory</option>
                <option value="Brunei Darussalam">Brunei Darussalam</option>
                <option value="Bulgaria">Bulgaria</option>
                <option value="Burkina Faso">Burkina Faso</option>
                <option value="Burundi">Burundi</option>
                <option value="Cambodia">Cambodia</option>
                <option value="Cameroon">Cameroon</option>
                <option value="Canada">Canada</option>
                <option value="Cape Verde">Cape Verde</option>
                <option value="Cayman Islands">Cayman Islands</option>
                <option value="Central African Republic">Central African Republic</option>
                <option value="Chad">Chad</option>
                <option value="Chile">Chile</option>
                <option value="China">China</option>
                <option value="Christmas Island">Christmas Island</option>
                <option value="Cocos Islands">Cocos (Keeling) Islands</option>
                <option value="Colombia">Colombia</option>
                <option value="Comoros">Comoros</option>
                <option value="Congo">Congo</option>
                <option value="Congo">Congo, the Democratic Republic of the</option>
                <option value="Cook Islands">Cook Islands</option>
                <option value="Costa Rica">Costa Rica</option>
                <option value="Cota D'Ivoire">Cote d'Ivoire</option>
                <option value="Croatia">Croatia (Hrvatska)</option>
                <option value="Cuba">Cuba</option>
                <option value="Cyprus">Cyprus</option>
                <option value="Czech Republic">Czech Republic</option>
                <option value="Denmark">Denmark</option>
                <option value="Djibouti">Djibouti</option>
                <option value="Dominica">Dominica</option>
                <option value="Dominican Republic">Dominican Republic</option>
                <option value="East Timor">East Timor</option>
                <option value="Ecuador">Ecuador</option>
                <option value="Egypt">Egypt</option>
                <option value="El Salvador">El Salvador</option>
                <option value="Equatorial Guinea">Equatorial Guinea</option>
                <option value="Eritrea">Eritrea</option>
                <option value="Estonia">Estonia</option>
                <option value="Ethiopia">Ethiopia</option>
                <option value="Falkland Islands">Falkland Islands (Malvinas)</option>
                <option value="Faroe Islands">Faroe Islands</option>
                <option value="Fiji">Fiji</option>
                <option value="Finland">Finland</option>
                <option value="France">France</option>
                <option value="France Metropolitan">France, Metropolitan</option>
                <option value="French Guiana">French Guiana</option>
                <option value="French Polynesia">French Polynesia</option>
                <option value="French Southern Territories">French Southern Territories</option>
                <option value="Gabon">Gabon</option>
                <option value="Gambia">Gambia</option>
                <option value="Georgia">Georgia</option>
                <option value="Germany">Germany</option>
                <option value="Ghana">Ghana</option>
                <option value="Gibraltar">Gibraltar</option>
                <option value="Greece">Greece</option>
                <option value="Greenland">Greenland</option>
                <option value="Grenada">Grenada</option>
                <option value="Guadeloupe">Guadeloupe</option>
                <option value="Guam">Guam</option>
                <option value="Guatemala">Guatemala</option>
                <option value="Guinea">Guinea</option>
                <option value="Guinea-Bissau">Guinea-Bissau</option>
                <option value="Guyana">Guyana</option>
                <option value="Haiti">Haiti</option>
                <option value="Heard and McDonald Islands">Heard and Mc Donald Islands</option>
                <option value="Holy See">Holy See (Vatican City State)</option>
                <option value="Honduras">Honduras</option>
                <option value="Hong Kong">Hong Kong</option>
                <option value="Hungary">Hungary</option>
                <option value="Iceland">Iceland</option>
                <option value="India">India</option>
                <option value="Indonesia">Indonesia</option>
                <option value="Iran">Iran (Islamic Republic of)</option>
                <option value="Iraq">Iraq</option>
                <option value="Ireland">Ireland</option>
                <option value="Israel">Israel</option>
                <option value="Italy">Italy</option>
                <option value="Jamaica">Jamaica</option>
                <option value="Japan">Japan</option>
                <option value="Jordan">Jordan</option>
                <option value="Kazakhstan">Kazakhstan</option>
                <option value="Kenya">Kenya</option>
                <option value="Kiribati">Kiribati</option>
                <option value="Democratic People's Republic of Korea">Korea, Democratic People's Republic of</option>
                <option value="Korea">Korea, Republic of</option>
                <option value="Kuwait">Kuwait</option>
                <option value="Kyrgyzstan">Kyrgyzstan</option>
                <option value="Lao">Lao People's Democratic Republic</option>
                <option value="Latvia">Latvia</option>
                <option value="Lebanon" selected>Lebanon</option>
                <option value="Lesotho">Lesotho</option>
                <option value="Liberia">Liberia</option>
                <option value="Libyan Arab Jamahiriya">Libyan Arab Jamahiriya</option>
                <option value="Liechtenstein">Liechtenstein</option>
                <option value="Lithuania">Lithuania</option>
                <option value="Luxembourg">Luxembourg</option>
                <option value="Macau">Macau</option>
                <option value="Macedonia">Macedonia, The Former Yugoslav Republic of</option>
                <option value="Madagascar">Madagascar</option>
                <option value="Malawi">Malawi</option>
                <option value="Malaysia">Malaysia</option>
                <option value="Maldives">Maldives</option>
                <option value="Mali">Mali</option>
                <option value="Malta">Malta</option>
                <option value="Marshall Islands">Marshall Islands</option>
                <option value="Martinique">Martinique</option>
                <option value="Mauritania">Mauritania</option>
                <option value="Mauritius">Mauritius</option>
                <option value="Mayotte">Mayotte</option>
                <option value="Mexico">Mexico</option>
                <option value="Micronesia">Micronesia, Federated States of</option>
                <option value="Moldova">Moldova, Republic of</option>
                <option value="Monaco">Monaco</option>
                <option value="Mongolia">Mongolia</option>
                <option value="Montserrat">Montserrat</option>
                <option value="Morocco">Morocco</option>
                <option value="Mozambique">Mozambique</option>
                <option value="Myanmar">Myanmar</option>
                <option value="Namibia">Namibia</option>
                <option value="Nauru">Nauru</option>
                <option value="Nepal">Nepal</option>
                <option value="Netherlands">Netherlands</option>
                <option value="Netherlands Antilles">Netherlands Antilles</option>
                <option value="New Caledonia">New Caledonia</option>
                <option value="New Zealand">New Zealand</option>
                <option value="Nicaragua">Nicaragua</option>
                <option value="Niger">Niger</option>
                <option value="Nigeria">Nigeria</option>
                <option value="Niue">Niue</option>
                <option value="Norfolk Island">Norfolk Island</option>
                <option value="Northern Mariana Islands">Northern Mariana Islands</option>
                <option value="Norway">Norway</option>
                <option value="Oman">Oman</option>
                <option value="Pakistan">Pakistan</option>
                <option value="Palau">Palau</option>
                <option value="Panama">Panama</option>
                <option value="Papua New Guinea">Papua New Guinea</option>
                <option value="Paraguay">Paraguay</option>
                <option value="Peru">Peru</option>
                <option value="Philippines">Philippines</option>
                <option value="Pitcairn">Pitcairn</option>
                <option value="Poland">Poland</option>
                <option value="Portugal">Portugal</option>
                <option value="Puerto Rico">Puerto Rico</option>
                <option value="Qatar">Qatar</option>
                <option value="Reunion">Reunion</option>
                <option value="Romania">Romania</option>
                <option value="Russia">Russian Federation</option>
                <option value="Rwanda">Rwanda</option>
                <option value="Saint Kitts and Nevis">Saint Kitts and Nevis</option>
                <option value="Saint LUCIA">Saint LUCIA</option>
                <option value="Saint Vincent">Saint Vincent and the Grenadines</option>
                <option value="Samoa">Samoa</option>
                <option value="San Marino">San Marino</option>
                <option value="Sao Tome and Principe">Sao Tome and Principe</option>
                <option value="Saudi Arabia">Saudi Arabia</option>
                <option value="Senegal">Senegal</option>
                <option value="Seychelles">Seychelles</option>
                <option value="Sierra">Sierra Leone</option>
                <option value="Singapore">Singapore</option>
                <option value="Slovakia">Slovakia (Slovak Republic)</option>
                <option value="Slovenia">Slovenia</option>
                <option value="Solomon Islands">Solomon Islands</option>
                <option value="Somalia">Somalia</option>
                <option value="South Africa">South Africa</option>
                <option value="South Georgia">South Georgia and the South Sandwich Islands</option>
                <option value="Span">Spain</option>
                <option value="SriLanka">Sri Lanka</option>
                <option value="St. Helena">St. Helena</option>
                <option value="St. Pierre and Miguelon">St. Pierre and Miquelon</option>
                <option value="Sudan">Sudan</option>
                <option value="Suriname">Suriname</option>
                <option value="Svalbard">Svalbard and Jan Mayen Islands</option>
                <option value="Swaziland">Swaziland</option>
                <option value="Sweden">Sweden</option>
                <option value="Switzerland">Switzerland</option>
                <option value="Syria">Syrian Arab Republic</option>
                <option value="Taiwan">Taiwan, Province of China</option>
                <option value="Tajikistan">Tajikistan</option>
                <option value="Tanzania">Tanzania, United Republic of</option>
                <option value="Thailand">Thailand</option>
                <option value="Togo">Togo</option>
                <option value="Tokelau">Tokelau</option>
                <option value="Tonga">Tonga</option>
                <option value="Trinidad and Tobago">Trinidad and Tobago</option>
                <option value="Tunisia">Tunisia</option>
                <option value="Turkey">Turkey</option>
                <option value="Turkmenistan">Turkmenistan</option>
                <option value="Turks and Caicos">Turks and Caicos Islands</option>
                <option value="Tuvalu">Tuvalu</option>
                <option value="Uganda">Uganda</option>
                <option value="Ukraine">Ukraine</option>
                <option value="United Arab Emirates">United Arab Emirates</option>
                <option value="United Kingdom">United Kingdom</option>
                <option value="United States">United States</option>
                <option value="United States Minor Outlying Islands">United States Minor Outlying Islands</option>
                <option value="Uruguay">Uruguay</option>
                <option value="Uzbekistan">Uzbekistan</option>
                <option value="Vanuatu">Vanuatu</option>
                <option value="Venezuela">Venezuela</option>
                <option value="Vietnam">Viet Nam</option>
                <option value="Virgin Islands (British)">Virgin Islands (British)</option>
                <option value="Virgin Islands (U.S)">Virgin Islands (U.S.)</option>
                <option value="Wallis and Futana Islands">Wallis and Futuna Islands</option>
                <option value="Western Sahara">Western Sahara</option>
                <option value="Yemen">Yemen</option>
                <option value="Serbia">Serbia</option>
                <option value="Zambia">Zambia</option>
                <option value="Zimbabwe">Zimbabwe</option>
            </select>
        </div>
        <div class="input_name">
            <label for="zip">Zip</label>
            <input id="zip" v-model="zip" />
        </div>
        <hr>
        <button class="submitButton" @click="validateForm">Submit</button>
    </div>
</template>

<style>
.select_country {
    max-width: 173px;
}

.submitButton {
    margin-top: 20px;
    margin-bottom: 20px;
    margin-left: 20px;
    font-size: 19px;
    color: black;
    background-color: rgb(106, 26, 210);
    border-radius: 5px;
    font-family: Times;
}

.error_msg {
    color: rgb(116, 10, 17);
    font-size: 10.5px;
}

.form-group {
    min-width: 250px;
    height: 550px;
    display: flex;
    /* делает .form-group флекс-контейнером */
    flex-direction: column;
    /* устанавливает основное направление стека внутренних элементов в вертикальное */
    align-items: flex-start;
    /* выравнивает элементы внутри по началу оси */
    background-color: rgb(209, 93, 162);
}

.form-group>h1 {
    align-self: center;
    /* центрирует заголовок внутри .form-group */
}

.input_name {
    display: flex;
    /* делает каждый .input_name флекс-контейнером */
    flex-direction: column;
    /* устанавливает направление стека элементов внутри в вертикальное */
    margin-right: 20px;
    /* добавляет небольшой отступ справа между полями ввода */
    margin-left: 20px;
}

.form-group {
    display: flex;
    /* изменяет направление .form-group на горизонтальное */
    flex-wrap: wrap;
    /* позволяет элементам переноситься на следующую строку, если не хватает места */
}
</style>