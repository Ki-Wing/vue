<template>
    <v-dialog max-width="500px">
        <v-card>
            <v-card-title class="text-h5 text-center">
                비밀번호 변경
            </v-card-title>
            <v-card-text>
                <v-form @submit.prevent="resetPassword">
                    <v-text-field label="Email" v-model="email" type="email" prepend-icon="mdi-email" required>
                    </v-text-field>
                    <v-text-field label="Password" v-model="asIsPassword" type="password" prepend-icon="mdi-lock" required>
                    </v-text-field>
                    <v-text-field label="newPassword" v-model="toBePassword" type="password" prepend-icon="mdi-lock" required>
                    </v-text-field>
                    <v-btn type="sunbmit" color="red" block>비밀번호 변경</v-btn>
                    <v-btn color="red" @click="closeModal" block>닫기</v-btn>
                </v-form>
            </v-card-text>
        </v-card>
    </v-dialog>
    </template>
    
    <script>
    import axios from 'axios';
    export default{
        data(){
            return{
                email:"",
                asIsPassword:"",
                toBePassword:"",
            }
        },
        methods:{
            async resetPassword(){
                const loginData = {
                    email: this.email,
                    asIsPassword : this.asIsPassword,
                    toBePassword: this.toBePassword
                };
                    //member/reset-password
                    // {body} -> body : {email:xxx, password:xxx}
                    // body -> {email:xxx, password:xxx}
            try {
                
                const response = await axios.patch(`${process.env.VUE_APP_API_BASE_URL}/member/reset-password`, loginData);
                console.log(response.data);
                alert('정상 변경 처리 되었습니다.')
            }catch(e){
                    console.log(e);
                    alert(e.response?.data?.error_message || "입력값을 확인해주세용");
                }
        },
            closeModal(){
                // this.emit은 vau에서 컴포넌트간의 이벤트를 전달하는 매커니즘
                // 자식컴포넌트에서 this.$emit을 호출하면 update:dialog라는 이벤트가 실행되고, false 부모 컴포넌트로 전달
                this.$emit('update:dialog', false);
            }
        }
    }
    </script>