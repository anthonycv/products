<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">Registro</div>
                    <div class="card-body">
                        <div class="form-group row">
                            <label for="name" class="col-md-4 col-form-label text-md-right">Name</label>
                            <div class="col-md-6">
                                <input v-model="name" id="name" type="text" class="form-control" name="name" required
                                       autocomplete="name" autofocus>
                                <span v-if="nameAlert" class="invalid-feedback" role="alert"
                                      style="display: block !important;">
                                        <strong>{{ nameError }}</strong>
                                    </span>
                            </div>
                        </div>

                        <div class="form-group row">
                            <label for="email" class="col-md-4 col-form-label text-md-right">Email</label>
                            <div class="col-md-6">
                                <input v-model="email" id="email" type="email" class="form-control" name="email"
                                       required
                                       autocomplete="email">
                                <span v-if="emailAlert" class="invalid-feedback" role="alert"
                                      style="display: block !important;">
                                        <strong>{{ emailError }}</strong>
                                    </span>
                            </div>
                        </div>

                        <div class="form-group row">
                            <label for="password" class="col-md-4 col-form-label text-md-right">Password</label>
                            <div class="col-md-6">
                                <input v-model="password" id="password" type="password" class="form-control"
                                       name="password" required
                                       autocomplete="new-password">
                                <span v-if="passwordAlert" class="invalid-feedback" role="alert"
                                      style="display: block !important;">
                                        <strong><span>{{ passwordError }}</span></strong>
                                    </span>
                            </div>
                        </div>

                        <div class="form-group row">
                            <label for="password-confirm" class="col-md-4 col-form-label text-md-right">Password
                                confirm</label>

                            <div class="col-md-6">
                                <input v-model="passwordConfirm" id="password-confirm" type="password"
                                       class="form-control"
                                       name="password_confirmation" required autocomplete="new-password">
                            </div>
                        </div>

                        <div class="form-group row mb-0">
                            <div class="col-md-6 offset-md-4">
                                <button @click="register" type="submit" class="btn btn-primary">
                                    Registrar
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                name: '',
                email: '',
                password: '',
                passwordConfirm: '',
                nameError: '',
                emailError: '',
                passwordError: '',
                nameAlert: false,
                passwordAlert: false,
                emailAlert: false,
            }
        },
        mounted() {

        },
        methods: {
            register() {
                this.nameAlert = false;
                this.passwordAlert = false;
                this.emailAlert = false;
                if(this.password !== this.passwordConfirm){
                    this.passwordAlert = true;
                    this.passwordError = 'Password and confirm password does not match.';
                    return false;
                }
                const newUser = {
                    name: this.name,
                    email: this.email,
                    password: this.password
                };
                axios.post('/api/auth/register', newUser).then((res) => {
                    window.location.href = '/login';
                }).catch((err) => {
                    if (typeof err.response.data.errorValidate !== 'undefined') {
                        const errorValidate = err.response.data.errorValidate;
                        console.log(errorValidate);
                        for (const index in errorValidate) {
                            this.[index + 'Error'] = errorValidate[index][0];
                            this.[index + 'Alert'] = true;
                        }
                    }else{
                        console.log(err.response.data);
                    }
                });
            }
        }
    }
</script>
