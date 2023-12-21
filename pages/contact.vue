<template>
    <div class="contact-page mt-24 w-96">
        <div class="contact-form flex flex-col p-12 dark-box">


            <h1 class="header">
                Our address
            </h1>

            <div class="mb-8">
                <h1>Address</h1>
                <h2>Alcon Molina 51</h2>
                <h1>City</h1>
                <h2>Totana</h2>
                <h1>Email</h1>
                <h2>office@crashapp.com</h2>
            </div>

            <h1 class="header">
                Contact Us
            </h1>

            <form @submit.prevent="submitForm" class="flex flex-col mt-2">

                <InputField v-model="name" label="Name" :requiredField="true" :inputType="'text'" />
                <InputField v-model="email" label="Email" :requiredField="true" :inputType="'email'" />
                <InputField v-model="message" label="Message" :requiredField="true" :isTextArea="true" />

                <ShineButton class="self-center">Send Email</ShineButton>
            </form>
        </div>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            name: '',
            email: '',
            message: '',
        };
    },

    methods: {

        async submitForm() {
            try {
                await this.$axios.post('/api/sendEmail', {
                    name: this.name,
                    email: this.email,
                    message: this.message,
                });

                console.log('Email sent successfully!');
            } catch (error) {
                console.error('Error sending email:', error);
            }
        },
    },
};
</script>

<style lang="scss">
.contact-page {

    .contact-form {
        .header {
            font-size: 30px;
            text-align: center;
            width: 100%;
            margin-bottom: 20px;
            border: 2px solid white;
            border-radius: 15px;
            padding: 10px 0 15px 0;
            background-color: rgba(1, 1, 1, 0.2);
        }
    }

    h1 {
        font-weight: 700;
        color: blanchedalmond;
        text-decoration: underline;
    }

}
</style>
  