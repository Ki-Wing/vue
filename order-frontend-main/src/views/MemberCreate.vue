<template>
    <v-container>
        <v-row justify="center">   
            <!-- 화면 크기가 small 이상일때(스마트폰, 태블릿 등) : sm
            화면 크기가 medium 이상일때 : md-->
            <v-col cols="12" sm="6" md="8">
                <v-card>
                    <v-card-title class="text-h5 text-center">
                        회원가입
                    </v-card-title>
                    <v-card-text>
                        <v-form @submit.prevent="memberCreate">
                            <v-text-field label="name" v-model="name" prepend-icon="mdi-account" required>

                            </v-text-field>
                            <v-text-field label="email" v-model="email" type="email"  prepend-icon="mdi-email" required>

                            </v-text-field>
                            <v-text-field label="password" v-model="password"  type="password"  prepend-icon="mdi-lock" required>

                            </v-text-field>
                            <v-text-field label="city" v-model="city"  prepend-icon="mdi-city" >

                            </v-text-field>                            
                            <v-text-field label="street" v-model="street"  prepend-icon="mdi-home" >

                            </v-text-field>
                            <v-text-field label="zipcode" v-model="zipcode" required  prepend-icon="mdi-mailbox" >

                            </v-text-field>

                                <!-- block은 부모컨테이너 너비만큼 꽉 채우는 것 -->
                                <v-btn block type="submit" color="red">등록</v-btn>

                        </v-form>
                    </v-card-text>
                </v-card>
            </v-col>
        </v-row>
    </v-container>


</template>

<script>
import axios from 'axios';
export default{
    data(){
        return{
            name:"",
            email:"",
            password:"",
            city:"",
            street:"",
            zipcode:""
        }
    },
    methods:{
        async memberCreate(){
            try{
                const registerData = {
                    name: this.name,
                    email: this.email,
                    password : this.password,
                    address:{
                        city: this.city,
                        street: this.street,
                        zipcode: this.zipcode
                    }
                }
                await axios.post(`${process.env.VUE_APP_API_BASE_URL}/member/create`,registerData);
                this.$router.push("/product/manage");

                }catch(e){
                    const error_message = e.response.data.error_message;
                    console.log(error_message);
                    alert(error_message);
                }
            }
        }

};
</script>