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
				<p v-if="OS === 'iOS'">Phone: 
                    <a :href="`sms:${senator.phone}&body=${message}`" v-if="typeof senator.phone !== 'undefined' && senator.phone !== 'No Phone number'">{{senator.phone}}</a>
                    <span v-else>No phone number</span>
                </p>
                <p v-else>Phone: 
                    <a :href="`sms:${senator.phone}?body=${message}`" v-if="typeof senator.phone !== 'undefined' && senator.phone !== 'No Phone number'">{{senator.phone}}</a>
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
            return encodeURI("Dear senator, I am  a concerned citizen of your constituent, and I'll like to express my displeasure with the two bills currently in motion. These bills are attempts to infringe on the basic human right of freedom to speech as Nigerians, and I believe it has far reaching consequences on the future of our dear nation. I urge you, distinguished, to speak and vote against these bills for the sake of the future of Nigeria.I know you are a person of integrity and I trust you'll do the right thing. Thanks Senator!");
        },
        subject(){
            return "Anti social media bill";
		},
		OS() {
			var userAgent = navigator.userAgent || navigator.vendor || window.opera;

				// Windows Phone must come first because its UA also contains "Android"
				if (/windows phone/i.test(userAgent)) {
					return "Windows Phone";
				}

				if (/android/i.test(userAgent)) {
					return "Android";
				}

				// iOS detection from: http://stackoverflow.com/a/9039885/177710
				if (/iPad|iPhone|iPod/.test(userAgent) && !window.MSStream) {
					return "iOS";
				}

				return "unknown";
			}
	},
	mounted(){
		console.log(this.message);
	}
}
</script>

<style>

</style>
