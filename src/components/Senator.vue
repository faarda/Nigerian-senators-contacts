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
            return encodeURI("Dear senator, I am  a concerned citizen of your constituent, and I'll like to express my displeasure about SARS. The members of this squad who are supposed to protect us against armed robbery are killing, extorting and harassing us everyday. We are scared to move freely and we need your help. I urge you, distinguished, to use your office to protect the lives of Nigerian youth and the future of Nigeria. We are counting on you to do the right thing. We are counting on you to help us #ENDSARS. Thanks Senator!");
        },
        subject(){
            return "END SARS";
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
