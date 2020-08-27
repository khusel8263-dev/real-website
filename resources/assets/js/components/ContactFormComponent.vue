<template>

    <form @submit.prevent="submit">        
        <div v-if="success" class="alert alert-success mt-3">
            Таны захиа амжилттай илгээгдлээ!
        </div>
        <input v-model="contact.name" v-bind:class="{'required-error': errors && errors.name}" type="text" name="name" id="name" placeholder="Таны нэр*" class="input-bg">
                
        <input v-model="contact.email" v-bind:class="{'required-error': errors && errors.email}" type="text" name="email" id="email" placeholder="И-мэйл хаяг*" class="input-bg">
                
        <input v-model="contact.subject" type="text" name="subject" id="subject" placeholder="Агуулга" class="input-bg">
        
        <textarea v-model="contact.message" v-bind:class="{'required-error': errors && errors.message}" name="message" id="comment" placeholder="Таны захиа*" class="input-bg"></textarea>                                    
        
        <button id="contact-us-button" type="submit" class="btn btn-small border-radius-4 btn-black">Илгээх</button>
    </form>

</template>

<script>
    export default {
        data() {
            return {
                contact: {},
                success: false,
                errors: {},
            }
        },
        methods: {
            submit() {             
                this.success = false;
                this.errors = {};
                axios.post('/contact', this.contact)
                .then(response => {
                    this.contact = {};
                    this.success = true;
                })
                .catch(error => {
                    if (error.response.status === 422) {
                    this.errors = error.response.data.errors || {};
                    }
                });
            },
        },
    }
</script>