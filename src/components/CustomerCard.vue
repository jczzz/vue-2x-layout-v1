<template>
			<div  class="card">
				<div class="card-image">
                    <figure class="image is-4by3">
                      <img
                        :src="url"
                        :alt="customer.name">
                    </figure>
                  </div>
				<div class="card-content">
                    <div class="media">
                      <div class="media-content overflow-content">
						<b-card-title style="color:#202223;
											font-family: Rubik;
											font-style: normal;
											font-weight: 500;
											font-size: 30px;
											line-height: 28px;"
                        >{{customer.name}}</b-card-title>
						<b-card-sub-title class="mb-2" style="color:#909090, 100%">{{`@`+customer.username}}</b-card-sub-title>
						<b-card-text style="color: #51C5FF;">
								{{`"`+customer.company.catchPhrase+`"`}}
							</b-card-text>

						<b-card-text>
							<p >
								<span >
									<i class="far fa-envelope">&nbsp;&nbsp;</i>
								</span>
								<span >
									{{customer.email}}
								</span>
							</p>
							<p > 
								<span >
									<i class="fas fa-map-marked">&nbsp;&nbsp;</i>
								</span>
								<span >
									{{customer.address.street+', '
									+customer.address.suite+', '
									+customer.address.city+', '
									+customer.address.zipcode+', '
									+customer.address.geo.lat+', '
									+customer.address.geo.lng}}
								</span>
							</p>
							<p>
								<span>
									<i class="fas fa-phone">&nbsp;&nbsp;</i>
								</span>
								<span>
									{{customer.phone}}
								</span>
							</p>
							<p>
								<span>
									<i class="fab fa-internet-explorer">&nbsp;&nbsp;</i>
								</span>
								<span>
									{{customer.website}}
								</span>
							</p>
							<p>
								<span>
									<i class="fas fa-briefcase">&nbsp;&nbsp;</i>
								</span>
								<span>
									{{customer.company.name}}
								</span>
							</p>
							<p>
								<span>
									<i class="fas fa-user-tie">&nbsp;&nbsp;</i>
								</span>
								<span>
									{{customer.company.bs}}
								</span>
							</p>
						</b-card-text>

                      </div>
                    </div>
                  </div>
			</div>
</template>
<script>
export default {
    name: 'CustomerCard',
    props: {
        customer: {
        type: Object,
        required: true,
        },
		url : {
			type:String
		}
    }
    
}
</script>
<style lang="scss" scoped>

</style>