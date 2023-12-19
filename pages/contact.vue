<template>
    <div class="contactPage mt-24 w-96">
        <div class="contact-form flex flex-col p-12 dark-box">

            <div class="mb-8">
                <h1>Address</h1>
                <h2>Alcon Molina 51</h2>
                <h1>City</h1>
                <h2>Totana</h2>
            </div>

            <h1>Contact Us</h1>
            <form @submit.prevent="submitForm" class="flex flex-col">
                <label for="name">Name:</label>
                <input type="text" v-model="name" required />

                <!-- <InputField></InputField> -->

                <label for="email">Email:</label>
                <input type="email" v-model="email" required />

                <label for="message">Message:</label>
                <textarea v-model="message" required></textarea>

                <ShineButton class="self-center mt-8">Send Email</ShineButton>
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
            // Send email data to backend (you can use Axios or any other HTTP library)
            try {
                await this.$axios.post('/api/sendEmail', {
                    name: this.name,
                    email: this.email,
                    message: this.message,
                });

                // Optionally, you can display a success message or redirect the user
                console.log('Email sent successfully!');
            } catch (error) {
                console.error('Error sending email:', error);
                // Handle error, display an error message, or redirect the user
            }
        },
    },
};
</script>

<style>

    .contactPage{

        h1 {
            font-weight: 700;
            color: blanchedalmond;
            text-decoration: underline;
        }

        .contact-form {
            input, textarea {
                padding: 2px 5px 3px 5px;
                color: black;
            }
        }
    }

</style>
  