<template>
    <div class="content">
        <v-row class="section1">
            <v-col cols="1"></v-col>
            <v-col cols="5">
                <v-row class="my-0">
                    <v-col cols="4" class="text-left">
                        <v-subheader>Тип счета-фактуры</v-subheader>
                    </v-col>
                    <v-col cols="6" class="text-right">
                        <v-text-field class="input1"
                            label="text-field"
                            outlined
                        ></v-text-field>
                    </v-col>
                </v-row>
                <v-row class="my-0">
                    <v-col cols="4">
                        <v-subheader>Счет-фактура № </v-subheader>
                    </v-col>
                    <v-col cols="6">
                        <v-text-field class="input1"
                            label="text-field"
                            outlined v-model="arr[0].invoices[0].document.document_number" :rules="onlyRequired" required
                        ></v-text-field>
                    </v-col>
                </v-row>
                <v-row class="my-0" v-if="!checkboxes.poterminalu">
                    <v-col cols="4">
                        <v-subheader>К договору №</v-subheader>
                    </v-col>
                    <v-col cols="6">
                        <v-text-field
                            label="text-field"
                            outlined v-model="arr[0].invoices[0].document.contract_number" :rules="onlyRequired" required
                        ></v-text-field>
                    </v-col>
                </v-row>
                <v-row class="my-0" v-else>
                    <v-col cols="4">
                    </v-col>
                    <v-col cols="6">
                        <v-textarea
                            rows="2"
                            outlined
                            name="input-7-4"
                            label="Outlined textarea"
                            value="Продажа по терминалу"
                        ></v-textarea>
                    </v-col>
                </v-row>

            </v-col>
            <v-col cols="4">
                <v-row class="mt-10">
                    <v-col cols="4">
                    </v-col>
                    <v-col
                        cols="6"
                    >
                        <v-menu
                            v-model="menu1"
                            :close-on-content-click="false"
                            :nudge-right="40"
                            :nudge-top="20"
                            transition="scale-transition"
                            offset-y
                            min-width="auto"
                        >
                            <template v-slot:activator="{ on, attrs }">
                                <v-text-field
                                    v-model="arr[0].invoices[0].document.document_date"
                                    label="Picker without buttons"
                                    prepend-icon="mdi-calendar"
                                    readonly
                                    outlined
                                    v-bind="attrs"
                                    v-on="on"
                                ></v-text-field>
                            </template>
                            <v-date-picker
                                no-title
                                v-model="arr[0].invoices[0].document.document_date"
                                @input="menu1 = false"
                            ></v-date-picker>
                        </v-menu>
                    </v-col>
                </v-row>
                <v-row>
                    <v-col cols="4">
                    </v-col>
                    <v-col
                        cols="6"
                    >
                        <v-menu
                            v-model="menu2"
                            :close-on-content-click="false"
                            :nudge-right="40"
                            :nudge-top="20"
                            transition="scale-transition"
                            offset-y
                            min-width="auto"
                        >
                            <template v-slot:activator="{ on, attrs }">
                                <v-text-field
                                    v-model="arr[0].invoices[0].document.contract_date"
                                    label="Picker without buttons"
                                    prepend-icon="mdi-calendar"
                                    outlined
                                    readonly
                                    v-bind="attrs"
                                    v-on="on" :rules="onlyRequired" required
                                ></v-text-field>
                            </template>
                            <v-date-picker
                            no-title
                            v-model="arr[0].invoices[0].document.contract_date"
                            @input="menu2 = false"
                            ></v-date-picker>
                        </v-menu>
                    </v-col>
                </v-row>
            </v-col>
            <v-col cols="2">
                <v-row>
                    <v-col></v-col>
                </v-row>
                <v-row>
                    <v-col></v-col>
                </v-row>
                <v-row class="mt-16">
                    <v-col class="mt-16">
                        <v-checkbox class="mt-8"
                            label="По терминалу "
                            color="success"
                            value="true"
                            hide-details v-model="checkboxes.poterminalu"
                        ></v-checkbox>
                    </v-col>
                </v-row>
            </v-col>
        </v-row>
        <hr class="grey lighten-1">
        <br>
        <v-row  class="section2">
            <v-col cols="6">
                <v-row  class="input2">
                    <v-col cols="4">
                        <p class="text-right grey--text">Статус</p>
                    </v-col>
                    <v-col cols="8">
                        <p class="text-left">{{status}}</p>
                    </v-col>
                </v-row>
                <v-row  class="input2">
                    <v-col cols="4">
                        <p class="text-right grey--text" v-if="!checkboxes.komissioner">Поставщик</p>
                        <p class="text-right grey--text" v-else>Поставщик /Комиссионер</p>
                    </v-col>
                    <v-col cols="8">
                        <v-text-field class="input2"
                            label="text-field"
                            outlined v-model="arr[0].invoices[0].head.sender.sender_info.company_name"
                        ></v-text-field>
                    </v-col>
                </v-row>
                <v-row>
                    <v-col cols="4">
                        <p class="text-right grey--text">Адрес</p>
                    </v-col>
                    <v-col cols="8">
                        <v-text-field class="input2"
                            label="text-field"
                            outlined v-model="arr[0].invoices[0].head.sender.sender_info.address.street" :rules="onlyRequired" required
                        ></v-text-field>
                    </v-col>
                </v-row>
                <v-row>
                    <v-col cols="4">
                        <p class="text-right grey--text">ИНН / ПИНФЛ</p>
                    </v-col>
                    <v-col cols="3">
                        <v-text-field class="input2"
                            label="text-field" disabled
                            outlined v-model="arr[0].invoices[0].head.sender.sender_info.INN"
                            :rules="innRules" :counter="9" required
                        ></v-text-field>
                    </v-col>
                    <v-col cols="2">
                        <p class="text-right grey--text">Код НДС </p>
                    </v-col>
                    <v-col cols="3">
                        <v-text-field class="input2"
                            label="text-field"
                            outlined v-model="arr[0].invoices[0].head.sender.sender_info.company_vat_code"
                        ></v-text-field>
                    </v-col>
                </v-row>
                <v-row  class="input2">
                    <v-col cols="4">
                        <p class="text-right grey--text">Банковский счёт </p>
                    </v-col>
                    <v-col cols="4">
                        <v-text-field
                            label="text-field"
                            outlined v-model="arr[0].invoices[0].head.sender.sender_info.bank_details.account_number"
                        ></v-text-field>
                    </v-col>
                    <v-col cols="1">
                        <p class="text-right grey--text">МФО</p>
                    </v-col>
                    <v-col cols="3">
                        <v-text-field
                            label="text-field"
                            outlined v-model="arr[0].invoices[0].head.sender.sender_info.bank_details.bank_code"
                        ></v-text-field>
                    </v-col>
                </v-row>
                <v-row>
                    <v-col cols="4"></v-col>
                    <v-col>
                        <v-checkbox
                            label="Комиссионер"
                            color="success"
                            value="true"
                            hide-details v-model="checkboxes.komissioner"
                            ></v-checkbox>
                    </v-col>
                </v-row>
            </v-col>
            <v-col cols="6">
                <v-row>
                    <v-col cols="4"></v-col>
                    <v-col>
                        <v-checkbox
                            label="Односторонняя счёт-фактура "
                            color="success"
                            value="true"
                            hide-details v-model="checkboxes.odnostoronnaya"
                        ></v-checkbox>
                    </v-col>
                </v-row>
                <div v-if="!checkboxes.odnostoronnaya">
                    <v-row>
                        <v-col cols="4">
                            <p class="text-right grey--text">ИНН / ПИНФЛ покупателя</p>
                        </v-col>
                        <v-col cols="8">
                            <v-text-field class="input3"
                                label="text-field"
                                outlined v-model="arr[0].invoices[0].head.receiver.receiver_info.INN" :rules="innRules" :counter="9" required
                            ></v-text-field>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col cols="4">
                            <p class="text-right grey--text">Адрес</p>
                        </v-col>
                        <v-col cols="8">
                            <v-text-field class="input3"
                                label="text-field"
                                outlined v-model="arr[0].invoices[0].head.receiver.receiver_info.address.street"
                            ></v-text-field>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col cols="4">
                            <p class="text-right grey--text">ИНН / ПИНФЛ</p>
                        </v-col>
                        <v-col cols="3">
                            <v-text-field class="input3"
                                label="text-field"
                                outlined v-model="arr[0].invoices[0].head.receiver.receiver_info.INN" 
                            ></v-text-field>
                        </v-col>
                        <v-col cols="2">
                            <p class="text-right grey--text">Код НДС </p>
                        </v-col>
                        <v-col cols="3">
                            <v-text-field class="input3"
                                label="text-field"
                                outlined v-model="arr[0].invoices[0].head.receiver.receiver_info.company_vat_code"
                            ></v-text-field>
                        </v-col>
                    </v-row>
                    <v-row >
                        <v-col cols="4">
                            <p class="text-right grey--text">Банковский счёт </p>
                        </v-col>
                        <v-col cols="4" class="input3">
                            <v-text-field
                                label="text-field"
                                outlined v-model="arr[0].invoices[0].head.receiver.receiver_info.bank_details.account_number"
                            ></v-text-field>
                        </v-col>
                        <v-col cols="1">
                            <p class="text-right grey--text">МФО</p>
                        </v-col>
                        <v-col cols="3" class="input3">
                            <v-text-field
                                label="text-field"
                                outlined v-model="arr[0].invoices[0].head.receiver.receiver_info.bank_details.bank_code"
                            ></v-text-field>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col cols="4">
                            <p class="text-right grey--text">Директор</p>
                        </v-col>
                        <v-col cols="8" class="input3">
                            <v-text-field
                                label="text-field"
                                outlined v-model="arr[0].invoices[0].head.receiver.approver_and_signers.signer_director.last_name"
                            ></v-text-field>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col cols="4">
                            <p class="text-right grey--text">Главный Бухгалтер</p>
                        </v-col>
                        <v-col cols="8">
                            <v-text-field class="input3"
                                label="text-field"
                                outlined v-model="arr[0].invoices[0].head.receiver.approver_and_signers.signer_accountant.last_name"
                            ></v-text-field>
                        </v-col>
                    </v-row>
                </div>
                <div v-else>
                    <v-row>
                        <v-col cols="4"></v-col>
                        <v-col cols="7">
                            <v-select :items="items" class="input2"></v-select>
                        </v-col>
                    </v-row>
                </div>
                <v-row v-if="checkboxes.komissioner">
                        <v-col cols="4"></v-col>
                        <v-col>
                            <v-checkbox
                                label=" Поручитель "
                                color="success"
                                value="true"
                                hide-details v-model="checkboxes.prouchitel"
                            ></v-checkbox>
                        </v-col>
                    </v-row>
            </v-col>
        </v-row>
        <br>
        <hr class="grey lighten-1">
        <div class="section3">
            <v-row>
                <v-col cols="2">
                    <v-checkbox
                        label=" Ручное вычисление  "
                        color="success"
                        value="true"
                        hide-details v-model="checkboxes.vichislenie"
                    ></v-checkbox>
                </v-col>
                <v-col cols="8">
                    <v-checkbox
                        label=" Cчитать до 4 знаков (после запятой) "
                        color="success"
                        value="true"
                        hide-details v-model="checkboxes.poslezapitoy"
                    ></v-checkbox>
                </v-col>
                <v-col cols="2">
                    <v-checkbox
                        label=" Обратный расчет "
                        color="success"
                        value="true"
                        hide-details v-model="checkboxes.obratniy" class="text-right"
                    ></v-checkbox>
                </v-col>
            </v-row>
            <v-simple-table class="table1">
                <template v-slot:default>
                    <thead border="1">
                        <tr>
                            <th rowspan="2" class="text-center">
                                №
                            </th>
                            <th rowspan="2" class="text-center">
                                ИКПУ и наименование товаров (работ, услуг) 
                            </th>
                            <th rowspan="2" class="text-center">
                                Описание товаров (работ, услуг)
                            </th>
                            <th rowspan="2" class="text-center">
                                Штрих-код товара (услуги)
                            </th>
                            <th rowspan="2" class="text-center">
                                Ед. изм.
                            </th>
                            <th rowspan="2" class="text-center">
                                Кол - во 
                            </th>
                            <th rowspan="2" class="text-center">
                                Цена
                            </th>
                            <th rowspan="2" class="text-center">
                                Стоимость поставки 
                            </th>
                            <th colspan="2" class="text-center">
                                НДС
                            </th>
                            <th rowspan="2" class="text-center">
                                Стоимость поставок с учётом НДС 
                            </th>
                            <th rowspan="2" class="text-center">
                                Льгота НДС 
                            </th>
                            <th rowspan="2" class="text-center">
                                
                            </th>
                        </tr>
                        <tr>
                            <th class="text-cente">
                                ставка
                            </th>
                            <th class="text-cente">
                                сумма
                            </th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="item in arr[0].invoices[0].document.items" :key="item.item_number">
                            <td>{{ item.item_number }}</td>
                            <td>
                                <v-text-field
                                    label=""
                                    solo v-model="item.description"
                                ></v-text-field>
                            </td>
                            <td>
                                <v-text-field
                                    label=""
                                    solo v-model="item.catalog.name"
                                ></v-text-field>
                            </td>
                            <td>
                                <v-text-field
                                    label=""
                                    solo v-model="item.catalog.barcode"
                                ></v-text-field>
                            </td>
                            <td>
                                <v-text-field
                                    label=""
                                    solo v-model="item.measurement_unit"
                                ></v-text-field>
                            </td>
                            <td>
                                <v-text-field
                                    label=""
                                    solo v-model="item.volume"
                                ></v-text-field>
                            </td>
                            <td>
                                <v-text-field
                                    label=""
                                    solo v-model="item.unit_price"
                                ></v-text-field>
                            </td>
                            <td>
                                <v-text-field
                                    class="text-right"
                                    label=""
                                    solo v-model="item.subtotal"
                                ></v-text-field>
                            </td>
                            <td>
                                <v-text-field
                                    class="text-right"
                                    label=""
                                    solo v-model="item.vat.vat_rate"
                                ></v-text-field>
                            </td>
                            <td>
                                <v-text-field
                                    class="text-right"
                                    label=""
                                    solo v-model="item.vat.vat_value"
                                ></v-text-field>
                            </td>
                            <td>
                                <v-text-field
                                    class="text-right"
                                    label=""
                                    solo v-model="item.subtotal_with_taxes"
                                ></v-text-field>
                            </td>
                            <td>
                                <v-text-field
                                    class="text-right"
                                    label=""
                                    solo v-model="item.lgota_id"
                                ></v-text-field>
                            </td>
                            <td></td>
                        </tr>
                    </tbody>
                </template>
            </v-simple-table>
            <v-row>
                <v-col cols="8"></v-col>
                <v-col cols="1" class="text-right">
                    <v-subheader>Доп. поле</v-subheader>
                </v-col>
                <v-col cols="3">
                    <v-textarea
                            rows="1"
                            outlined
                            name="input"
                            label="Outlined textarea"
                            value=""
                        ></v-textarea>
                </v-col>
            </v-row>
        </div>
        <hr class="grey lighten-1">
        <br>
        <div class="section4">
            <v-row>
                <v-col cols="1"></v-col>
                <v-col cols="4">
                    <v-row>
                        <v-col cols="4" class="text-right">
                            <v-subheader>
                                Руководитель
                            </v-subheader>
                        </v-col>
                        <v-col cols="8">
                            <v-text-field
                                label=""
                                solo v-model="arr[0].invoices[0].head.receiver.approver_and_signers.signer_director.last_name" :rules="onlyRequired" required
                            ></v-text-field>
                        </v-col>
                        <v-col cols="4" class="text-right">
                            <v-subheader>
                                Главный бухгалтер
                            </v-subheader>
                        </v-col>
                        <v-col cols="8">
                            <v-text-field
                                label=""
                                solo v-model="arr[0].invoices[0].head.receiver.approver_and_signers.signer_accountant.last_name"
                            ></v-text-field>
                        </v-col>
                        <v-col cols="4" class="text-right">
                            <v-subheader>
                                Товар передал
                            </v-subheader>
                        </v-col>
                        <v-col cols="8">
                            <v-text-field
                                label=""
                                solo v-model="arr[0].invoices[0].head.receiver.approver_and_signers.signer_warehouse.last_name"
                            ></v-text-field>
                        </v-col>
                    </v-row>
                </v-col>
                <v-col cols="1"></v-col>
                <v-col cols="2">
                    <v-checkbox
                        label=" По доверенности "
                        color="success"
                        value="true"
                        hide-details v-model="checkboxes.podoverennosti" class="text-right"
                    ></v-checkbox>
                </v-col>
                <v-col cols="4">
                    <v-row v-if="checkboxes.podoverennosti">
                        <v-col cols="8">
                            <v-text-field
                                label="Номер"
                                solo v-model="number"
                            ></v-text-field>
                        </v-col>
                        <v-col cols="4">
                            <v-menu
                            v-model="menu3"
                            :close-on-content-click="false"
                            :nudge-left="150"
                            transition="scale-transition"
                            offset-y
                            min-width="auto"
                            >
                                <template v-slot:activator="{ on, attrs }">
                                    <v-text-field
                                        v-model="date3"
                                        label="Date"
                                        readonly
                                        solo
                                        v-bind="attrs"
                                        v-on="on"
                                    ></v-text-field>
                                </template>
                                <v-date-picker
                                    no-title
                                    v-model="date3"
                                    @input="menu3 = false"
                                ></v-date-picker>
                            </v-menu>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field
                                label="ИНН / ПИНФЛ"
                                solo v-model="inn3"
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field
                                label="ФИО"
                                solo v-model="fio"
                            ></v-text-field>
                        </v-col>
                    </v-row>
                </v-col>
                <v-col>
                    <router-link to="/invoice">
                    <v-btn class="float-right"
                    color="blue-grey darken-4 white--text"
                    elevation="5"
                    >Создать документ</v-btn></router-link>
                    <v-btn class="float-right mr-5"
                    color="blue-grey darken-4 white--text"
                    elevation="5" @click="DataInAlert"
                    >Просмотр</v-btn>
                </v-col>
            </v-row>
        </div>
        <!-- <div>
            <p>{{universalvatinvoice}}</p>
        </div> -->
        <!-- <v-snackbar
            v-model="snackbar"
        >
            <pre>{{ text }}</pre>
            

            <template v-slot:action="{ attrs }">
                <v-btn
                color="pink"
                text
                v-bind="attrs"
                @click="snackbar = false"
                >
                Close
                </v-btn>
            </template>
        </v-snackbar> -->
    </div>
</template>

<script>
export default {
    data(){
        return{
            arr:[
                {
                    invoices:[
                        {

                        head: {
                            file_name : "",
                            program_version: "1.0.0",
                            format_version: "1.0.0",
                            sender: {
                                sender_info: {
                                    INN: "302563857",
                                    company_name: "",
                                    company_vat_code: "",
                                    address: {
                                        region: "",
                                        street: ""
                                    },
                                    phone: "",
                                    bank_details: {
                                        account_number: "",
                                        bank_name: "",
                                        bank_code: ""
                                    }
                                },
                                approver_and_signers: {
                                    approver: {
                                        last_name: "",
                                        first_name: "",
                                        middle_name: ""
                                    },
                                    signer: {
                                        last_name: "",
                                        first_name: "",
                                        middle_name: ""
                                    },
                                    signer_director: {
                                        last_name: "",
                                        first_name: "",
                                        middle_name: ""
                                    },
                                    signer_accountant: {
                                        last_name: "",
                                        first_name: "",
                                        middle_name: ""
                                    },
                                    signer_warehouse: {
                                        last_name: "",
                                        first_name: "",
                                        middle_name: ""
                                    }
                                }
                            },
                            receiver: {
                                receiver_info: {
                                    INN: "",
                                    company_name: "",
                                    company_vat_code: "",
                                    address: {
                                        region: "",
                                        street: ""
                                    },
                                    phone: "",
                                    bank_details: {
                                        account_number: "",
                                        bank_name: "",
                                        bank_code: ""
                                    }
                                },
                                approver_and_signers: {
                                    approver: {
                                        last_name: "",
                                        first_name: "",
                                        middle_name: ""
                                    },
                                    signer: {
                                        last_name: "",
                                        first_name: "",
                                        middle_name: ""
                                    },
                                    signer_director: {
                                        last_name: "",
                                        first_name: "",
                                        middle_name: ""
                                    },
                                    signer_accountant: {
                                        last_name: "",
                                        first_name: "",
                                        middle_name: ""
                                    },
                                    signer_warehouse: {
                                        last_name: "",
                                        first_name: "",
                                        middle_name: ""
                                    }
                                }
                            }
                        },
                        document: {
                            document_version: "v1",
                            document_number: "",
                            document_date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
                            contract_number: "",
                            contract_date: "",
                            lot_number: "",
                            items: [
                                {
                                    item_number: "1",
                                    description: "",
                                    volume: "",
                                    unit_price: "0.00",
                                    subtotal: "0.00",
                                    vat: {
                                        vat_rate: 0,
                                        vat_value: 0
                                    },
                                    subtotal_with_taxes: "0.00",
                                    measurement_unit: "куб.м",
                                    excise: {
                                        excise_rate: 0,
                                        excise_value: 0
                                    },
                                    catalog: {
                                        code: "70001",
                                        name: "Водоснабжение"
                                    },
                                    lgota_id: null,
                                    barcode: "",
                                    product_marks: {
                                        product_type: 0,
                                        kiz: [
                                            "kiz 1",
                                            "kiz 2"
                                        ],
                                        nom_upak: [
                                            "nom_upak 1",
                                            "nom_upak 2"
                                        ],
                                        ident_trans_upak: [
                                            "ident_trans_upak 1",
                                            "ident_trans_upak 2"
                                        ]
                                    }
                                }
                            ],
                            column_summary_values: {
                                column_subtotal: "",
                                column_subtotal_uzs: "",
                                column_vat_value: "",
                                column_vat_value_uzs: "",
                                column_subtotal_with_taxes: "",
                                column_subtotal_with_taxes_total: "",
                                column_subtotal_with_taxes_uzs: ""
                            }
                        },
                        id: 12345,
                        }
                    ]
                }
            ],
            checkboxes:{
                poterminalu: false,
                komissioner: false,
                odnostoronnaya: false,
                prouchitel: false,
                vichislenie: false,
                poslezapitoy: false,
                obratniy: false,
                podoverennosti: false
            },
            items: [
                'Стандартный',
                'Дополнительный',
                'Возмещение расходов',
                'Без оплаты',
                'Исправленный',
                'Исправленный (возмещение затрат)'
            ],
            menu1: false,
            menu2: false,
            date3: '',
            menu3: false,
            number: '',
            inn3: '',
            fio: '',
            status: 'Физическое лицо',
            universalvatinvoice: '',
            text:'',
            snackbar: false,
            innRules: [
                v => !!v || 'Inn is required',
                v => v.length == 9 || 'Inn mustbe equal 9 characters'
            ],
            onlyRequired: [
                v => !!v || 'This field is required',
            ]
        }
    },
    methods:{
        DataInAlert() {
            this.arr[0].invoices[0].head.file_name = "universal-vat-invoice_" + this.arr[0].invoices[0].head.sender.sender_info.INN + "_" + this.arr[0].invoices[0].head.receiver.receiver_info.INN + "_2022-01-20_FU-0001.xml"

            this.arr[0].invoices[0].document.column_summary_values.column_subtotal = this.arr[0].invoices[0].document.items[0].subtotal
            this.arr[0].invoices[0].document.column_summary_values.column_subtotal_uzs = this.arr[0].invoices[0].document.items[0].subtotal
            this.arr[0].invoices[0].document.column_summary_values.column_vat_value = this.arr[0].invoices[0].document.items[0].vat.vat_value
            this.arr[0].invoices[0].document.column_summary_values.column_vat_value_uzs = this.arr[0].invoices[0].document.items[0].vat.vat_value
            this.arr[0].invoices[0].document.column_summary_values.column_subtotal_with_taxes = this.arr[0].invoices[0].document.items[0].subtotal_with_taxes
            this.arr[0].invoices[0].document.column_summary_values.column_subtotal_with_taxes_total = this.arr[0].invoices[0].document.items[0].subtotal_with_taxes
            this.arr[0].invoices[0].document.column_summary_values.column_subtotal_with_taxes_uzs = this.arr[0].invoices[0].document.items[0].subtotal_with_taxes

            this.snackbar = true
            this.text = this.arr[0]
            this.$router.push({name: "Invoice", params: {data: this.text}})

            // alert(JSON.stringify(this.arr[0], null, 4));
        },
        // Invoice(){
        //     this.universalvatinvoice = JSON.stringify(this.head, null, 16) + JSON.stringify(this.document, null, 16)
        // },

    },
    // "file_name": "universal-vat-invoice_sender.sender_info.INN_receiver.receiver_info.INN_2022-01-20_FU-0001.xml",
}
</script>

<style>
.content{
    background: white;
    width: 100%;
    padding: 10px;
}
.input1{
    height: 30px;
}
.input2{
    height: 70px;
}
.input3{
    height: 20px;
}
.table1{
    padding: 10px 0;
}
th ,td{
    border: 1px solid #dddddd;
}
.section3{
    padding: 0 0 20px 0;
}
</style>