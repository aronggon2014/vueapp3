<template>
  <v-container>
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-row>
        <!--  -->
        <v-col cols="6">
          <v-text-field
            v-model="name"
            :counter="30"
            :rules="nameRules"
            label="ชื่อ"
            required
          ></v-text-field
        ></v-col>
        <!-- นามสกุล -->
        <v-col cols="6">
          <v-text-field
            v-model="lastname"
            :counter="30"
            :rules="lastnameRules"
            label="นานสกุล"
            required
          ></v-text-field
        ></v-col>
      </v-row>
      <v-row>
        <v-col cols="6"
          ><v-text-field
            v-model="email"
            :rules="emailRules"
            counter="50"
            label="อีเมล"
            required
          ></v-text-field
        ></v-col>
        <v-col cols="6"
          ><v-text-field
            v-model="tel"
            :rules="telRules"
            :counter="10"
            label="เบอร์โทรศัพท์"
            required
          ></v-text-field
        ></v-col>
      </v-row>
      <v-row>
        <v-col clos="2"
          ><v-text-field
            v-model="a_number"
            :rules="addressRules"
            :counter="20"
            label="เลขที่อยู่"
            required
          ></v-text-field
        ></v-col>
        <v-col clos="2"
          ><v-text-field
            v-model="a_group"
            :rules="addressRules"
            :counter="20"
            label="หมู่"
            required
          ></v-text-field
        ></v-col>
        <v-col clos="4"
          ><v-text-field
            v-model="a_road"
            :rules="addressRules"
            :counter="20"
            label="ถนน"
            required
          ></v-text-field
        ></v-col>
        <v-col clos="4"
          ><v-text-field
            v-model="a_lane"
            :rules="addressRules"
            :counter="20"
            label="ซอย"
            required
          ></v-text-field
        ></v-col>
      </v-row>
      <v-row>
        <v-col clos="4"
          ><v-text-field
            v-model="a_subdis"
            :rules="addressRules"
            :counter="20"
            label="ตำบล"
            required
          ></v-text-field
        ></v-col>
        <v-col clos="4"
          ><v-text-field
            v-model="a_dis"
            :rules="addressRules"
            :counter="20"
            label="อำเภท"
            required
          ></v-text-field
        ></v-col>
        <v-col clos="4"
          ><v-text-field
            v-model="a_province"
            :rules="addressRules"
            :counter="20"
            label="จังหวัด"
            required
          ></v-text-field
        ></v-col>
      </v-row>
      <v-select
        v-model="select"
        :items="sex"
        :rules="[v => !!v || 'กรุณาเลือกเพศ']"
        label="เพศ"
        required
      ></v-select>
      <v-checkbox
        v-model="checkbox"
        :rules="checkboxRules"
        label="ยอมรับเงื่อนไข"
        required
      ></v-checkbox>
      <v-btn :disabled="!valid" color="success" class="mr-4" @click="validate">
        สมัครสมาชิก
      </v-btn>
      <v-btn color="error" class="mr-4" @click="reset">
        เคลียร์
      </v-btn>
      <v-row>
        <v-col cols="12">
          <!-- ตารางแสดงข้อมูล -->
          <v-card>
            <v-card-title>
              ข้อมูลลูกค้า
              <v-spacer></v-spacer>
              <v-text-field
                v-model="search"
                append-icon="mdi-magnify"
                label="Search"
                single-line
                hide-details
              ></v-text-field>
            </v-card-title>
            <v-data-table
              :headers="headers"
              :items="desserts"
              :search="search"
            ></v-data-table>
          </v-card>
        </v-col>
      </v-row>
      <!-- <v-btn
      color="warning"
      @click="resetValidation"
    >
      เคลียร์การตรวจสอบ
    </v-btn> -->
    </v-form>
  </v-container>
</template>
<script>
import axios from 'axios';
export default {
  data: () => ({
    valid: false,
    name: "",
    nameRules: [
      v => !!v || "กรุณากรอกชื่อ",
      v => (v && v.length <= 30) || "ชื่อต้องมีขนาดไม่เกิน 30 ตัวอักษร"
    ],
    lastname: "",
    lastnameRules: [
      v => !!v || "กรุณากรอกนามสกุล",
      v => (v && v.length <= 30) || "นามสกุลต้องมีขนาดไม่เกิน 30 ตัวอักษร"
    ],
    email: "",
    emailRules: [
      v => !!v || "กรุณากรอก อีเมล",
      v => /.+@.+\..+/.test(v) || "กรอกอีเมลให้ถูกต้อง",
      v => (v && v.length <= 50) || "อีเมลต้องมีความยังไม่เกิน 50 ตัวอักษร"
    ],
    tel: "",
    telRules: [
      v => !!v || "กรุณากรอกเบอร์โทรศัทพ์",
      v => (v && v.length <= 10) || "ต้องมีความยาวไม่เกิน 10 หลัก"
    ],
    checkboxRules: [v => !!v || "คุณต้องกรอกยอมรับเงื่อนนไขก่อนสมัครสมาชิก"],
    select: null,
    items: ["Item 1", "Item 2", "Item 3", "Item 4"],
    sex: ["ชาย", "หญิง"],
    checkbox: false,
    a_number: "",
    a_group: "",
    a_road: "",
    a_lane: "",
    a_subdis: "",
    a_dis: "",
    a_province: "",
    addressRules: [
      v => !!v || "กรุณากรอกข้อมูล",
      v => (v && v.length <= 20) || "ต้องมีความยังไม่เกิน 20 ตัวอักษร"
    ],
    search: "",
    headers: [ {
        text: "ชื่อ - นามสกุล",
        value: "fullname"},
      { text: "เบอณ์โทรศัทพ์", value: "tel" },
      { text: "อีเมล", value: "email" },
      { text: "เพศ", value: "sex" },
      { text: "ที่อยู่", value: "address" }
    ],
    desserts: []
  }),
  methods: {
    validate() {
      if (this.$refs.form.validate()) {
        //   console.log(this.name);
        //   console.log(this.lastname);
        //   console.log(this.email);
        //   console.log(this.tel);
        //   console.log(this.select);
        //   console.log(this.a_number);
        //   console.log(this.a_group);
        //   console.log(this.a_lane);
        //   console.log(this.a_road);
        //   console.log(this.a_subdis);
        //   console.log(this.a_dis);
        //   console.log(this.a_province);
      // // axios.get('http://localhost:3000/api/students/show').then((res)=>{
      //   console.log(res)
      // });

      axios.post('http://localhost:3000/api/customers/',{
            "c_name": this.name,
            "c_lastname": this.lastname,
            "c_email": this.email,
            "c_tel": this.tel,
            "c_num": this.a_number,
            "c_mu": this.a_group,
            "c_tanon": this.a_road,
            "c_soi": this.a_lane,
            "c_tumbon": this.a_subdis,
            "c_amphor": this.a_dis,
            "c_jung":this.a_province,
            "c_sex": this.select
      }).then((res)=>{
        console.log(res)
      });


        this.desserts.push({
            fullname:`${this.name}${this.lastname}`,
            tel:`${this.tel}`,
            email:`${this.email}`,
            sex:`${this.select}`,
            address:`${this.a_number}ม.${this.a_group}ถ.${this.a_road}ซ.${this.a_lane}ต.${this.a_subdis}อ.${this.a_dis}จ.${this.a_province}`,
        });
      }
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    }
  }
};
</script>
<style></style>