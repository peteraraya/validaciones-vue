<template>
    <div class="mt-5">
        <h1>Vuildate</h1>
        <form @submit.prevent="submit">
                <input type="email" placeholder="Ingrese un email " class="form-control my-3"
                v-model.lazy="$v.email.$model" 
                :class="{'is-invalid': $v.email.$error}">
                        <p class='text-danger' v-if="!$v.email.email">Este email es incorrecto</p>
                        <p class="text-danger" v-if="!$v.email.required">Campo requerido</p>

                        <!-- <p>{{ $v.email }}</p> -->

                <input  type="password" placeholder="Ingrese un contraseña " class="form-control my-3"
                        v-model="$v.password.$model"
                        :class="{'is-invalid': $v.password.$error}"
                        >
                        <p class='text-danger' v-if="!$v.password.minLength">Minimo 6 caracteres</p>
               
                <input  type="password" placeholder="Repita contraseña" class="form-control my-3"
                        v-model="$v.repeatPassword.$model"
                        :class="{'is-invalid': $v.repeatPassword.$error}"
                        >
                        <p class='text-danger' v-if="!$v.repeatPassword.sameAsPassword">Las contraseñas no son iguales</p>
                        <!-- <p>{{ $v.repeatPassword }}</p> -->


                <button type="submit" 
                        :disabled="$v.$invalid"
                        class="btn btn-primary btn-block">Enviar</button>

                <p> {{$v.$invalid}}</p>
                <p>{{$v}}</p>
        </form>
    </div>
</template>

<script>
// importamos todas las utilidades que nos ofrece vuelidate
import { required, email, sameAs, minLength } from 'vuelidate/lib/validators'
export default {

    name: 'Validaciones',
    data(){
        return{
            email: '',
            password: '',
            repeatPassword: ''
        }
    },
    validations:{
        email:{required,email},
        password:{
            required,
            minLength: minLength(6) // minimo 6 caracteres
        },
        repeatPassword:{
            sameAsPassword: sameAs('password') // toma como parametro la contreaseña que nosotros queremos comparar
        }
    },
    methods:{
        submit(){
                console.log('submit');
                this.$v.$touch();
                if(this.$v.$invalid){
                    // this.submitStatus = 'Error'
                    console.log('se generó un error');
                } else{
                    // // do your submit logic here
                    // // this.submitStatus = 'Pending'
                    // setTimeout(()=>{
                    //     // this.submitStatus = 'OK'
                    // },500)
                    console.log('Todos los campos correctos');
                    console.log('Enviando información ....'+ this.$v.email.$model + ' '+
                                                             this.$v.password.$model );
                    
                }
            }
        }
    
};
</script>

