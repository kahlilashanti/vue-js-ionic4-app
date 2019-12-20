<template>
    <ion-grid>
        <form @submit="onSubmit">
            <ion-col>
                <ion-i>
                    <ion-label>ZipCode</ion-label>
                    <ion-input :value="zip" @input="zip=$event.target.value" placeholder="Enter US Zip Code" name="zip"></ion-input>
                </ion-i>
            </ion-col>
            <ion-col>
                <ion-button type="submit" color="primary" expand="block">Find</ion-button>
            </ion-col>
        </form>
    </ion-grid>
</template>

<script>
export default {
    name: "ZipSearch",
    data(){
        return{
            zip: ""
        };
    },
    methods: {
        onSubmit(e){
            e.preventDefault();
            //Zip regex
            const isValidZip = /(^\d{5}$)|(^\d{5}-\d{4}$)/.test(this.zip);
            //test for valid zip
            if(!isValidZip){
                this.showAlert();
            } else {
                console.log("thanks")
            }
        },
        showAlert(){
            return this.$ionic.alertController
            .create({
                header: "Enter ZipCode",
                message: "Please enter a valid US Zip Code...",
                buttons: ["OK"]
            })
            .then(a => a.present())
        }
    }
}
</script>

