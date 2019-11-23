<template>
    <div class="div senator">
        <div class="senator-img">
            <img :src="`/senators/${senator.id}.jpeg`" alt="">
        </div>
        <div class="details">
            <div class="name">
                <h3>{{senator.name}}</h3>
                <span class="district">{{senator.state}} state</span>
            </div>
            <div class="contacts">
                <p>Email: 
                    <a :href="`mailto:${senator.email}?subject=${subject}&body=${message}`">{{senator.email}}</a>
                </p>
                <p>Phone: 
                    <a :href="`sms:${senator.phone}&body=${message}`" v-if="typeof senator.phone !== 'undefined' && senator.phone !== 'No Phone number'">{{senator.phone}}</a>
                    <span v-else>No phone number</span>
                </p>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    props:{
        senator: Object,
        id: Number
    },
    computed: {
        message(){
            return "Dear senator%0D%0A I am  a concerned citizen of your constituent, and I'll like to express my displeasure with the two bills currently in motion. %0D%0A These bills are attempts to infringe on the basic human right of freedom to speech as Nigerians, and I believe it has far reaching consequences on the future of our dear nation.%0D%0A I urge you, distinguished, to speak and vote against these bills for the sake of the future of Nigeria.%0D%0A I know you are a person of integrity and I trust you'll do the right thing. %0D%0A Thanks Senator!";
        },
        subject(){
            return "Anti social media bill";
        }
    }
}
</script>

<style>

</style>
